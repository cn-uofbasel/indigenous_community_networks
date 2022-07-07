# Collaboration Plan

## User stories

### Communal organization
- Inter-territory communication
- Outside connectivity with Brasilia (major city with collaborators)
- More nodes that are financially acessible

### Keeping in touch with family
- Bridge to a node with Internet connection
- Mobile application with audio
- Easy to use interface for oral-cultures
- Easy way to discover and install the app
- Intermitend nodes as to not affect social dynamics

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
