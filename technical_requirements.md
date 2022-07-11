# Technical requirements

## Devices

We have 4 types of devices:
1. End-user phones connected to Wi-Fi
   1. Tremola
      1. with normal SSB **OR** module to convert to TinySSB
      2. module to connect to Meshtastic through serial (device of type 3)
      3. support of emergency messages in a custom chat
      4. sends audio messages coded with Codec 2
   2. possibility to use manyverse ?
2. SSB pub (Raspberry Pi)
   1. Translate to TinySSB (?)
   2. store everything in memory
   3. Act as a WiFi hotspot
   4. module to connect to Meshtastic through serial (device of type 3)
3. Edge nodes
   1. Run Meshtastic software with a few adjustments
   2. Connect SSB pubs or phones (in the jungle) to the mesh
4. Intermediary nodes (repeaters)
   1. Run Meshtastic software with a few adjustements (slightly different to edge nodes)
   2. Cache the latest emergency messages

## Additions needed

1. Emergency packet type
   1. Each node keeps a cache of the latest emergency messages
   2. To ensure that all caches are up-to-date, a node sends the 8 (?) leading 
      bytes of the hash of the string formed by the concatenation of all cached emergency 
      messages (like a dmux)
      1. if the received data corresponds to its cache of emergency messages, nothing is 
         done
      2. else, a pull request is made (How ?)
      3. The messages are sorted with ScuttleSort
   3. For emergencies: have a way to connect  a phone directly to the intermediary nodes 
      with the help of a LoRa device, connected with serial

## Use cases

### Use case 2: one person or group in the jungle needs emergency help

If one person or group in the jungle needs emergency help, he can connect to the mesh 
using a phone and a LoRa device connected with serial 
- LoRa device connects to the closest node in the mesh
- The user sends an "emergency" message
- The message is broadcast to everybody, unencrypted
- each connected peer receives a push notification with the emergency message
- All emergency messages can be read in the "emergency" conversation (common to each user)
- anybody can reply directly in the chat
- emergency messages are spread with high priority
- There is a possibility to send the GPS location as emergency message

### Use case 3: one person or group in the jungle checks if someone needs emergency help

A person or group in the jungle wants to connect to the mesh from time to time to 
check if anybody nearby needs emergency help. They connect to the mesh as in use-case 2.
- When a mesh node accept a new connexion, it sends the feed id and sequence number of 
  the last entries it has (how many?). This is cached in each node
- If the last emergency messages are the same for both, there is only a pop-up 
  announcing it.
- If the mesh node has newer packets, it sends it automatically to the user
- If the mesh node doesn't have all the packets that the user needs, only the 
  cached messages are sent. Cache should be enough.

### Use case 4: Pull request

An intermittent node, which is a pub node for a village that is not always connected 
to the mesh or a node whose connection went down, comes back online.
1. For each feed on the local storage, we construct a message with:
   1. 4 (5?) leading bytes of the public key
   2. 4 bytes sequence number (can we take only the least significant 2-3 bytes?)
2. This message is sent to the closest edge node (it is not an SSB message)
3. The node receiving this messages checks, for each feed, if the sequence number 
   matches the one in its database and sends the missing data if applicable.
4. We do not ask other nodes: if the node we ask is not up-to-date, the latest data 
   will spread throughout the network including the node coming back online.

## Questions

1. Should we use SSB or TinySSB for Tremola:
   1. using SSB is easier (no adaptation needed) 
   2. it makes it compatible with existing clients
   BUT
   3. Using TinySSB takes less storage
   4. No conversion needed (easier to code for the RaspberryPi pub)
2. Do we give the possibility to use Manyverse?
3. As everything is broadcast, each end node has eventually the same copy. Use case: an 
   edge node goes online only a few hours a day. When he goes back online, he does a 
   pull request (use case 4).
   Do we want the answering node to check if there's a feed missing in its database 
   and send that too? It might make the response much longer. But after a few days / 
   weeks, only few new identities should be created. Also, it will help with the 
   discovery protocol to have an up-to-date list of all existing feeds.
4. Is it okay to have the "about" messages public and to have access to all peers in 
   the "contact" list? This would greatly simplify the discovery protocol. We would use a 
   private Room with Community mode to secure access from the Internet.
   Otherwise, we can use the Look-up discovery protocol with shortname asking the edge 
   node we're connected to (1 hop is enough).