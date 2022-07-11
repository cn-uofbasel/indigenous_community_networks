# Technical requirements

## Additions needed

### Devices

We have 4 types of devices:
1. End-user phones connected to Wi-Fi
   1. Tremola
      1. with normal SSB **OR** module to convert to TinySSB
      2. module to connect to Meshtastic through serial (device of type 3)
   2. possibility to use manyverse ?
2. SSB pub (Raspberry Pi)
   1. Translate to TinySSB (?)
   2. store everything in memory
   3. Act as a WiFi hotspot
   4. module to connect to Meshtastic through serial (device of type 3)
3. Edge nodes
   1. 
4. Intermediary nodes (repeaters)

Addition needed

1. Emergency packet type
   1. Each node keeps a cache of the latest emergency messages
   2. To ensure that all caches are up-to-date, a node sends the 8 (?) leading 
      bytes of the 
      hash of all cached 
      emergency messages (like a demux)
      1. this is the only packet that is not 120 bytes long
      2. if the received data corresponds to its cache of emergency messages, nothing is 
         done
      3. else, a pull request is made (How ?)
      4. The messages are sorted with ScuttleSort
   3. On the edge nodes: translate SSB packets to TinySSB
   4. For emergencies: have a way to connect directly to the intermediary nodes with the 
      help of a LoRa device, connected with serial


## Use cases

### Use case 1: 

If one person is in the jungle, he can connect to the mesh using a phone and a LoRa 
device A for emergencies. After the connexion to a (any) node of the mesh is set, he 
pulls the last entries for a given feed. 
 - the closest edge node B in the mesh is chosen (hop count? possible with Meshtastic)
 - the pull request is sent to B
 - B sends a broadcast message with the feed id and the sequence number of the last 
   message he has
 - B returns to A all messages A doesn't have
 - Edge node C receives B's broadcast. If he has newer messages, he sends it to A 
   directly (he will broadcast it to the rest of the mesh as normal)

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

A person or group in the jungle will want to connect to the mesh from time to time to 
check if anybody nearby needs emergency help. They connect to the mesh as in use-case 2.
- When a mesh node accept a new connexion, it sends the feed id and sequence number of 
  the last entry it has. This is cached in each node
- If the last emergency message is the same for both, there is only a pop-up announcing it
- If the mesh node has newer packets, it sends it automatically to the user
- If the mesh node doesn't have all the packets that the user needs, only the 
  cached messages are sent. Cache should be enough.

### Use case 4: Pull request

An intermittent node, which is a pub node for a village that is not always connected 
to the mesh or a node whose connection went down, comes back online.
1. For each feed on the local storage, we construct a message with:
   1. 4 (5?) leading bytes of the public key
   2. 4 bytes sequence number
3. This message is sent to the closest edge node (it is not an SSB message)
4. The node receiving this messages checks, for each feed, if the sequence number 
   matches the one in its database and sends the missing data if applicable.

#### Questions

1. Should we use SSB or TinySSB for Tremola:
   1. using SSB is easier (no adaptation needed) 
   2. it makes it compatible with existing clients
   BUT
   3. Using TinySSB takes less storage
   4. No conversion needed (easier to code for the RaspberryPi pub)
2. Do we give the possibility to use Manyverse?
3. As everything is broadcasted, each end node has eventually the same copy. Use case: an 
   edge node goes online only a few hours a day. When he goes back online, hw does a 
   pull request (use case 4).
   Do we want the answering node to check if there's a feed missing in its database 
   and send that too? It might make the response much longer. But after a few days / 
   weeks, only few new identities should be created. Also, it will help with the 
   discovery protocol to have an up-to-date list of all existing feeds.
4. Is it okay to have the "about" messages public and to have access to all peers in 
   the "contact" list? This would greatly simplify the discovery protocol. We would use a 
   private Room with Community mode to secure access from the Internet.