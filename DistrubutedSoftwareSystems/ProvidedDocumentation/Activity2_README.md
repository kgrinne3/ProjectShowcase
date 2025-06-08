# Assignment 5 Activity 2 #
Basic Distributed Library System

The leader acts as our server, while the nodes and the client act as clients to the leader.  
Nodes represent an individual library location, and the client represents the end user.  

A list of books known to the system can be found in the [BookList.md](BookList.md) file in the 
Activity2 root directory.

## Usage ##

### Leader Info ###
The leader must be started first for the system to operate, followed by the specified 
number of nodes. Optional arguments `port` and `nodes` may be included to override the 
default values if desired. If the optional arguments are not included, the leader will 
use port **8000** and will require **2** nodes before allowing client connections.  

### Node Info ###
At least one node must be run for the system to operate, as the leader will not accept 
client connections until at least the specified number of nodes is achieved. Optional 
arguments`port` and `file` containing the port to use and the filename of the node's 
inventory respectively. If the optional arguments are not included, default values of 
port **8000** and file **BookList1.json** will be used.  

_**PLEASE NOTE:** If more than one node is used, at least one node **must** specify 
a file other than BookList1.json to prevent both locations 'sharing' the inventory. 
If both Nodes use the same book list, Node 2's inventory will be adjusted to reflect 
changes that occurred at Node 1. **Best Practice** would be to specify the file for 
each node used._  

These files can be found in the `books` directory, and need only the filename (BookList1.json) when used
as an argument for a node. 

I have prepared four (4) different book lists with various states:  
- [BookList1](books/BookList1.json)  
This book list has the most variety, as all books have an available stock of ten (10) copies, 
with variations on the number of copies currently checked out.
- [BookList2](books/BookList2.json)  
This books list also provides more robust offerings with a varied number of total, available, and 
currently checked out copies. All books have at least five (5) or more copies available.
- [BookList3](books/BookList3.json)  
This book list gives all books a total number of ten (10) copies, with five (5) copies 
currently available and five (5) copies currently checked out.  
- [BookList4](books/BookList4.json)  
This book list is the most restrictive, as it gives all books a total number of five (5) 
copies, with only one (1) copy currently available and four (4) copies currently checked out.

### Client Info ###
Client is very user-friendly and will guide the user through program execution. Optional arguments 
of `host` and `port` may be included to override the defaults of `localhost` and `8000` respectively.


### Attributions ###
A copy of `JsonUtils`, found in both the example repository and starter code from 
previous assignments, is used in this project.  
A copy of `NetworkUtils`, also found in both the example repository and starter code from
previous assignments, is used in this project.  
A heavily modified version of `SocketInfo`, also found in both the example repository and starter code from
previous assignments, is used in this project.  

### Commands ###
Run the leader **FIRST** with:  
`gradle runLeader` to use the default port and number of nodes   
\
`gradle runLeader [-Pport=<port> -Pnodes=<numberOfNodes>]` to change the default values  

---

Run Nodes **NEXT** with:  
`gradle runNode -Pfile="BookList1.json"` to use the default port and BookList1  
\
`gradle runNode -Pfile="BookList2.json"` to use the default port and BookList2  
\
`gradle runNode -Pport<port> -Pfile=<filename>` to change the default values  

---

Run the Client **LAST** with:  
`gradle runClient` to use the default port  
\
`gradle runClient -Pport=<port>` to change the default values  


## Video Walkthrough ##
A short demo video can be found [here](https://youtu.be/zq-BVZHCXkg). 

## Requirements ##

I found it easier to work with the requirements in a separate file, which can be 
found [here](Requirements.md)

## Protocol ##

The protocol used is lengthy and is also defined in a separate file to aid in
readability, which can be found [here](Protocol.md) 