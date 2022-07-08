# Collaboration Plan


## User stories: Balaio Indigenous Territory

![territory map](/imgs/balaio_final.jpg)

### Communal organization and initial results

![povo tukano](/imgs/povo-tukano-4.png)

Bartolomeu, Maria and Carlos are village leaders at the Balaio Indigenous Territory and are collaborating with Naiara, who lives in Brasilia, 2000 kms away, on a project to promote food-sovereignty within their communities. Bartolomeu lives at the Balaio village, the largest of the territory and the only one that has access to Internet through a government-provided satellite connection. Maria and Carlos live in villages that are 20Km away from Balaio village through a very badly maintained dirt road, which makes it hard for them to get together and collaborate on the different parts of the project.

In 2021, Luandro visited the village as part of a first meeting to initiate a project with Nova Era to bring Internet connectivity to the villages, with funding coming from third-parties. During that visit a spontaneous project to connect the 3 villages using LoRa communication was initiated, following informal conversations about the capabilities of using LoRa nodes. This project did succeed in showing a proof-of-concept of text communication for organization purposes. In addition, solar-powered nodes providing additional services such as educational content for children in the village were installed in all three villages. 

However, some initial requirements such as allowing all villages to connect to the Internet could not be achieved during that visit. Also, the LoRa node in Balaio failed in the field: there were no other redundant path for connectivity and therefore LoRa connectivity to Balaio was broken for the other two villages. Finally, there was no database to store messages when the receivers are not online at the time of sending, which limited the usefulness of the setup.

**Requirements (2nd Phase):**

- Finish Internet bridge to connect with Brasilia (major city with collaborators)
- Add redundant nodes to keep connectivity in the presence of failures
- Add support for storing messages in transit (Meshtastic DB prototyped, could also work with SSB)

### Extending connectivity to other villages

Jonas, Jacinta and Cleide are also part of the territory, and leaders of much smaller neighboring villages. Like most indigenous people in the territory, they live off the land, planting, hunting and gathering, and they receive financial assistance from the state, about 40 Euros per family per month. All three leaders are also interested in connecting to the existing infrastructure. Unfortunately, the 2021 project did not have enough funding to also connect their village and the total cost of ownership, partially driven by the larger solar infrastructure required to provided additional services, made replication of similar a similar setup out of reach for their local means. Because they do not have similar connectivity, they are mostly left out of organizational processes organized by the three other villages.

During the deployment of the initial project, Alexandre, a boy from one of the villages who has a keen interest for technology but never used a computer in his life, followed the installation crew for some of the setups, and learned how to setup all the hardware. However, he wouldn't know how to install the software  to setup new nodes, even if the other villages could buy the equipment.

**Requirements:**

    - Add additional connectivity between the different villages, including those that were not connected in the first phase, with additional nodes
    - Make nodes cheaper (by possibly accepting intermittent connectivity)
    - Figure out a process to provide ready-to-deploy hardware
    - Enable field updates of software (Meshstastic, Tremola, and Pub/ssb-servers)

### Keeping in touch with family

![povo tukano](/imgs/povo-tukano.png)

Maria lives in Yamirim, a small village in the Amazon, where she works and lives, while her daughter lives in a city several hundreds km away. Like most other people in her village, Maria has a smartphone although there is no cell phone or internet coverage. There is Internet access in the neighboring village Balaio, but it is located 15 km away and the road to get there is impractical and the bus to go there only passes 2 times per week.

Maria would love to keep in touch with her daughter more often, mostly through audio messages but sometimes also text. Maria knows how to read and write Portuguese, although she would prefer audio communication, and knows how to use a smartphone. Because there is no Internet connection in her village, it would be more convenient for her to install applications on her smartphone from a local repository rather than from an official App Store.

Experiences in deploying Internet to other indigenous villages have shown that Internet access encouraged addictive behaviour, around porn, games, and social media, and threatened the social fabric of villages. In reaction, the Guarani Mbya ethnic group, spread between 21 villages, even decided to block Internet access during some times of the day. This suggests that deployment of connectivity solutions should be done progressively to let the villagers assess the impact of more limited forms of communication before deploying high-bandwidth Internet access to every individual. Text and audio messages over an intermittent connectivity infrastructure seems like a good first step in enabling connectivity with remote family members without introducing unwanted social dynamics.

**Requirements:**

    - Bridge to a node with Internet connection, only for synchronizing SSB messages
    - Mobile application with audio
    - Easy to use interface for oral-cultures
    - Easy way to discover and install the app
    - Intermittent nodes as to not affect social dynamics.

### Emergency communication in the jungle

![povo tukano](/imgs/povo-tukano-3.png)


André is a fisherman and hunter who lives in the Balaio village. Like all families in the Balaio Territory, his family depends on hunting and gathering from the forest and rivers to survive. And like many from his generation, he can't read or write.

He's out almost everyday fishing, hunting or gathering fruits from the forest, sometimes for days in a roll for larger hunting expeditions. Despite him being very experienced, the Amazon jungle has many dangers and his family is often worried about him, as he has no way to communicate if something happens. There's no cellphone coverage in the jungle, walkie-talkies don't penetrate more then a few meters, and HF radios aren't light enough to be carried. If he's alone and a snake bites him he may not be able to reach his village.

**Requirements:**

- Mobile nodes that connect and draw energy from phones

## Research problems

To Discuss with CFT

## Potential bachelor thesis

To Discuss with CFT

## Collaboration process
- Meeting frequencies
- Collaboration tools

## Final deliverables
- SSB Pub with Meshtastic + TinySSB plugin
- Tremola recording audio messages encoded in Codec2
- Tremola using geedksville-androidlib to send LoRa messages
- Report of a reference deployment and reproduction
- Easy to follow video documentation on how to setup
- Have a work model for scaling for self-deployment

## Timeline

## Implementation approach
- Tremola: add TinySSB with packet format using side-chains
- Tremola: add voice recording and playback using Codec2 encoding
- Tremola: add Meshtastic: connect thru serial, send and receive LoRa packets
- NodeJs: add Meshtastic: connect thru serial, send and receive LoRa packets
- NodeJS: convert LoRa packets to and from TinySSB
- NodeJS: convert tinySSB messages to and from Classic SSB
- NodeJS: pull new messages from LoRa mesh in case user wasn't online when updates were sent
- NodeJS: have a queue of tinySSB packets to send thru LoRa 

### Useful links:

#### Libs
- [geeksville-androidlib](https://github.com/meshtastic/geeksville-androidlib)
- [Meshtastic Python](https://github.com/meshtastic/Meshtastic-python)
- [Kotlin codec2 wrapper](https://github.com/masterjefferson/kodec2)
- [SSB DB2](https://github.com/ssbc/ssb-db2)
- [Reticulum](https://github.com/markqvist/Reticulum/)

#### Interfaces
- [Huiom: audio-only ssb client](https://github.com/luandro/huiom)
- [Meshtastic Android](https://github.com/meshtastic/Meshtastic-Android)
- [Zello: walkie-talkie app](https://play.google.com/store/apps/details?id=com.loudtalks)

#### Posts
- [Report on first Balaio deployment](https://viewer.scuttlebot.io/%25klnREUIw9FHajWCwzzVDwZJPjfhU9hQo2faE659b3%2F0%3D.sha256)
- [Report on first LoRa experiment](https://viewer.scuttlebot.io/%25hMC%2FIx%2FmnDvk0KYGcvXGo%2FKt8UuegWYz6vB91RyhIKQ%3D.sha256)
- [Report on audio-only SSB app](https://viewer.scuttlebot.io/%25Uh6Qk%2F9ncyKFJWJXDOeLSU1CLIagXc%2BANyT999Ol5dw%3D.sha256)
- [Thread on first thoughts of Meshtastic and SSB integration](https://viewer.scuttlebot.io/%25tz%2F6ms3u5cN5y3pKtRhtCkC4eXp7ASnhj6KU1tnA6bA%3D.sha256)
- [TinySSB conceptualization](ssb:message/sha256/VhSjGE4713avLfYRSnrSH-WcASL7WMNFWnuxnDGMmWo=)
- Shadow Packets [1](ssb:message/sha256/VhSjGE4713avLfYRSnrSH-WcASL7WMNFWnuxnDGMmWo=), [2](ssb:message/sha256/VhSjGE4713avLfYRSnrSH-WcASL7WMNFWnuxnDGMmWo=) and [3](ssb:message/sha256/VhSjGE4713avLfYRSnrSH-WcASL7WMNFWnuxnDGMmWo=)
- [ScuttleSort](ssb:message/sha256/VhSjGE4713avLfYRSnrSH-WcASL7WMNFWnuxnDGMmWo=)

## Future work
- Minimize packet sizes by indexing identities on every pub server and only send first 4 characters
