# Collaboration Plan

## User stories

### Communal organization

Bartolomeu, Maria and Carlos are village leaders at the Balaio Indigenous Territory and are collaborating with Naiara, who lives in Brasilia, on a project to promote food-sovereignty within their communities. Bartolomeu lives at the Balaio village, the largest of the territory and the only one that has access to Internet thru a government satellite connection. Maria and Carlos live on villages that are 20Km away from Balaio village thru a very badly maintained dirt road, which makes it hard for them to get together and collaborate on the different parts of the project.

In 2021 a project was executed to connect the 3 villages using LoRa communication, which only worked regionally, and also added large solar setups to support an Intranet server to provide targeted educational content for all villagers.

Jonas, Jacinta and Cleide are also part of the territory, and leaders of much smaller villages, and the project didn't have enough funding to support their communities, so they are mostly left out of organizational processes because of that. Like most indigenous peoples in the territory they live of the land, planting, hunting and gathering, and have very little financial means that come thru state social assistance, which are not enough to pool enough resources to buy the equipment themselves.

Alexandre was very interested in the LoRa project and learned how to setup the all hardware, but he never had access to a computer so wouldn't know how to install the software necessary to setup new nodes, even if the other villages could buy the equipment.

**Requirements:**

- Inter-territory communication
- Outside connectivity with Brasilia (major city with collaborators)
- More nodes that are financially acessible
- Work model for scaling self-deployment

### Keeping in touch with family

Maria lives in Yamirim, a small village in the Amazon, where she works and lives, while her daughter lives in a city several hundreds km away. Like most other people in her village Maria has a smartphone although there is no cell phone or internet coverage where she spends most of her time. There is Internet access in the neighboring village Balaio, but it is located 15 km away and the road to get there is impractical and the bus to go there only passes 2 times per week.

Maria would love to keep in touch with her daughter more often, mostly through audio messages but sometimes also text. Maria knows how to read and write Portuguese, although she would prefer audio communication, and knows how to use a smartphone. Because there is no Internet connection in her village it would be more convenient for her to install applications on her smartphone from a local repository rather than from an official App Store.

Life in the village is organized around the Sun with most activity happening when the Sun is shining, which is around 12h per day. Outside of work activities, often in the forest a few kms around the village, Maria spends time interacting with other villagers, often during random encounters. As developers of technical solutions, we anticipate that deploying technologies for remote connections may affect the social dynamics in Maria's village as users may prefer to spend time remotely over local interactions; this should eventually be confirmed with Maria and other villagers and let them decide whether they would be ok with such changes or not. In the meantime, it seems to us for the moment that accepting intermittent connectivity would make the insfrastructure cheaper and limit the potential negative effects of introducing new communication infrastructure.

**Requirements:**

    - Bridge to a node with Internet connection
    - Mobile application with audio
    - Easy to use interface for oral-cultures
    - Easy way to discover and install the app
    - Intermitent nodes as to not affect social dynamics and lower the costs of infrastructure.

### Emergency communication in the jungle

André is a fisherman and hunter who lives in the Balaio village. Like all families in the Balaio Territory, his family depends on hunting and gathering from the forest and rivers to survive. And like many from his generation, he can't read of write.

He's out almost everyday fishing, hunting or gathering fruits from the forest, sometimes for days in a roll for larger hunting expeditions. Despite him being very experienced, the Amazon jungle has many dangers and his family is often worried about him, as he has no way to communicate if something happens. There's no cellphone coverage in the jungle, walkie-talkies don't penetrate more then a few meters, and HF radios aren't light enough to be carried. If he's alone and a snake bites him he may not be able to reach his village.

**Requirements:**

- Mobile nodes that connect and draw energy from phones

## Research problems


## Potential bachelor thesis

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

### Userful links:
- [Meshtastic Android](https://github.com/meshtastic/Meshtastic-Android)
- [geeksville-androidlib](https://github.com/meshtastic/geeksville-androidlib)
- [Meshtastic Python](https://github.com/meshtastic/Meshtastic-python)
- [Kotlin codec2 wrapper](https://github.com/masterjefferson/kodec2)
- [SSB DB2](https://github.com/ssbc/ssb-db2)

## Future work
- Minize packet sizes by indexing identities on every pub server and only send first 4 characters
