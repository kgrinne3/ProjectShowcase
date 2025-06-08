# Assignment 5 Activity 1 #
A basic Peer-to-Peer chat room with no leader. 

## Usage ##
All peers are run with the same command followed by varying arguments. 

The peer expects three (3) arguments: 
- Your desired username 
- Your port
- The port we will attempt to communicate with

The first peer started must enter its own port as the target.  

If no ports are included, defaults of `8000` are used for **both** `port` and `target`

`gradle runPeer -Pusername=KATIE -Pport=7000 -Ptarget=7000`

followed by additional peers:  

`gradle runPeer -Pusername=ZAC -Pport=8000 -Ptarget=7000`

`gradle runPeer -Pusername=SAM -Pport=9000 -Ptarget=8000`

`gradle runPeer -Pusername=ALEX -Pport=8888 -Ptarget=9000`


## Video Walkthrough ##
A short walkthrough can be found [here](https://youtu.be/zI7MOCaFqFA);

## Adding New Nodes ##
When PeerA connects to PeerB, PeerB will add PeerA to its list of peers, and then send PeerA a list of all 
entries that PeerB is aware of. Then PeerB forwards PeerA's connection message to the peers in the list so 
that those peers may add PeerA to their list of peers as well. PeerA will take the list of peers received 
from PeerB and add each one to its list of peers. This method of communication allows each peer to obtain 
the most recent copy of the peers list. 

## Removing Nodes ##
Similar to adding nodes, when PeerA notices that PeerB is no longer responding, PeerA will remove PeerB from 
the list of peers. After removing any and all uncommunicative peers, PeerA will forward the list of 
all peers removed from the peer list to all the remaining peers in the list. This allows each peer to 
be notified of the Peers that need to be removed from the list immediately as opposed to waiting for 
each Peer to discover the inactive peers themselves. 