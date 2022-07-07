# Collaboration Plan

## User stories

### Communal organization
- Inter-territory communication
- Outside connectivity with Brasilia (major city with collaborators)
- More nodes that are financially acessible

### Keeping in touch with family

Maria lives in Yamirim, a small village in the Amazon, where she works and live, while her daughter lives in a city several hundreds km away.  Like most other people in her village Maria has a smartphone although there is no cell phone or internet  coverage where she spends most of her time. There is Internet access in the neighbouring village Balaio, but it is located 15 km away and the road to get there is impractical and the bus to go there only passes 2 times per week.

Maria would love to keep in touch with her daugther more often, mostly through audio messages but sometimes also text. Maria knows how to read and write Portuguese, although she would prefer audio communication, and knows how to use a smartphone. Because there is no Internet connection in her village it would be more convenient for her to install applications on her smartphone from a local repository rather than from an official App Store.

Life in the village is organized around the Sun with most activity happening when the Sun is shining, which is around 12h per day. Outside of work activities, often in the forest a few kms around the village, Maria spends time interacting with other villagers, often during random encounters. As developers of technical solutions, we anticipate that deploying technologies for remote connections may affect the social dynamics in Maria's village as users may prefer to spend time remotely over local interactions; this should eventually be confirmed with Maria and other villagers and let them decide whether they would be ok with such changes or not. In the meantime, it seems to us for the moment that accepting intermittent connectivity would make the insfrastructure cheaper and limit the potential negative effects of introducing new communication infrastructure.

**Requirements:**

    - Bridge to a node with Internet connection
    - Mobile application with audio
    - Easy to use interface for oral-cultures
    - Easy way to discover and install the app
    - Intermitent nodes as to not affect social dynamics

### Emergency communication in the jungle
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
- Tremola: add voice recording and playback using Codec2 enconding
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
