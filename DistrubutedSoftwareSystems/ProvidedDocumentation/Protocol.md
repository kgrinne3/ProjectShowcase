# Protocol #
<!-- TOC -->
* [Protocol](#protocol-)
  * [Leader Responses](#leader-responses-)
    * [Client Responses](#client-responses-)
      * [General](#general-)
      * [Specifics](#specifics-)
        * [Connected Signal](#connected-signal-)
        * [Menu Signal](#menu-signal-)
        * [Borrowed Signal](#borrowed-signal-)
        * [Returned Signal](#returned-signal-)
        * [Error Signal](#error-signal-)
    * [Node Responses](#node-responses-)
      * [General](#general--1)
      * [Specifics](#specifics--1)
        * [Connected Signal](#connected-signal--1)
        * [Exit Signal](#exit-signal-)
        * [Available Signal](#available-signal-)
        * [Release Signal](#release-signal-)
        * [Borrow Signal](#borrow-signal-)
        * [Return Signal](#return-signal-)
        * [Update Signal](#update-signal-)
        * [Listing Signal](#listing-signal-)
  * [Client Requests](#client-requests-)
    * [General](#general--2)
    * [Specifics](#specifics--2)
      * [Start Request](#start-request-)
      * [Login Request](#login-request-)
      * [Borrow Request](#borrow-request-)
      * [Return Request](#return-request-)
      * [Exit Request](#exit-request-)
  * [Node Requests](#node-requests-)
    * [General](#general--3)
    * [Specifics](#specifics--3)
      * [Connect Signal](#connect-signal-)
      * [Waiting Signal](#waiting-signal-)
      * [Error Signal](#error-signal--1)
      * [Available Result](#available-result-)
      * [Release Result](#release-result-)
      * [Borrow Result](#borrow-result-)
      * [Return Result](#return-result-)
      * [Update](#update-)
<!-- TOC -->

The system currently uses a basic JSON format for communication protocol.  
Messages are sent as a JSONObject containing named values.  
Any message, be it a request **or** a response, must _at the very least_ contain 
a `type` value, followed by several optional values. 

## Leader Responses ##
### Client Responses ###
#### General ####

        {
            "type" :        <String>,
            "value" :      <String>,
            "title" :       <String>, 
            "location" :    <String>
        }

#### Specifics ####
##### Connected Signal #####
Sent when client first connects, prompts the user to enter their ID number. 

        {
            "type" :        "greeting",
            "value" :      <String>
        }
##### Menu Signal #####
Send to prompt the client to select an action: Borrow, Return, or Quit.

        {
            "type" :        "menu",
            "value" :      <String>
        }

##### Borrowed Signal #####
Sent when a book has successfully been borrowed, notifies the user of the location to pick up their book. 

        {
            "type" :        "borrow",
            "value" :      <String>,
            "title" :       <String>, 
            "location" :    <String>
        }

##### Returned Signal #####
Sent when a book has successfully been returned, notifies the user of the location to drop off their book.

        {
            "type" :        "return",
            "value" :      <String>,
            "title" :       <String>, 
            "location" :    <String>
        }

##### Error Signal #####
Sent to user when an error has been encountered, such as not finding a user's borrowed listing.

        {
            "type" :        "error",
            "value" :      <String>
        }

### Node Responses ###
#### General ####

        {
            "type" :        <String>,
            "number" :      <int>,
            "location" :    <String>,
            "title" :       <String>, 
            "user" :        <int>
        }

#### Specifics ####
##### Connected Signal #####
        {
            "type" :        "connected",  
            "number" :      <int>,    --> ID number for this node
            "location" :    <String>  --> Location name for this node
        }
##### Exit Signal #####
Sent to nodes when leader is shutting down resources.   

        {
            "type" :        "exit"
        }
##### Available Signal #####
Sent to nodes to inquire is a given book is available. 

        {
            "type" :        "avail",
            "title" :       <String>  
        }
##### Release Signal #####
Sent to nodes to remove the given book from the pending list.

        {
            "type" :        "release",
            "title" :       <String>
        }

##### Borrow Signal #####
Sent to nodes to add the given book and user to the borrowed books listing.

        {
            "type" :        "borrow",
            "title" :       <String>, 
            "user" :        <int> --> ID #
        }

##### Return Signal #####
Sent to nodes to remove the given book and user from the borrowed books listing.

        {
            "type" :        "return",
            "title" :       <String>, 
            "user" :        <int> --> ID #
        }

##### Update Signal #####
Sent to nodes to receive the node's current borrowed books listing.

        {
            "type" :        "update"
        }

##### Listing Signal #####
Sent to nodes when the node borrowed book listing differs from the master list. The node will 
update the local list to reflect the master list. 

      {
          "type" :        "listing", 
          "location" :    <String>, 
          <int> :         <String> --> userID:title 
      }



---


## Client Requests ##
### General ###

        {
            "source" :      <String>,
            "type" :        <String>,
            "title" :       <String>, 
            "user" :        <int>,
            "id" :          <int>
        }

### Specifics ###
#### Start Request ####
Sent after connecting to the leader to initiate system.

        {
            "source" :      "user",
            "type" :        "start"
        }

#### Login Request ####
Sent to the leader after the user enters their ID number.

        {
            "source" :      "user",
            "type" :        "greeting",
            "id" :          <int>
        }

#### Borrow Request ####
Sent to the leader when the user has requested to borrow a book.

        {
            "source" :      "user",
            "type" :        "borrow",
            "title" :       <String>, 
            "user" :        <int>
        }

#### Return Request ####
Sent to the leader when the user has requested to return a book.

        {
            "source" :      "user",
            "type" :        "return",
            "title" :       <String>, 
            "user" :        <int>
        }

#### Exit Request ####
Sent to the leader when the user requests to quit.

        {
            "source" :      "user",
            "type" :        "exit"
        }


---

## Node Requests ##
### General ###

        {
            "source" :      <String>,
            "type" :        <String>,
            "port" :        <int>,
            "title" :       <String>, 
            "userID" :      <int>,
            "id" :          <int>,
            "location" :    <String>,
            "value" :       <String>/<boolean>
        }

### Specifics ###
#### Connect Signal ####
Sent to the leader upon first connection.

        {
            "source" :      "node",
            "type" :        "connection",
            "port" :        <int>
        }

#### Waiting Signal ####
Sent to the leader when the node is active and waiting instructions.

        {
            "source" :      "node",
            "type" :        "waiting",
            "id" :          <int>, --> NodeID
            "value" :       <String>
        }

#### Error Signal ####
Sent to the leader when the node encounters an error.

        {
            "source" :      "node",
            "type" :        "error",
            "id" :          <int>,      --> NodeID
            "value" :       <String>    --> Error msg
        }

#### Available Result ####
Sent to the leader after receiving an available signal, informs the leader if the book 
is available at this location.

        {
            "source" :      "node",
            "type" :        "avail"
            "title" :       <String>, 
            "id" :          <int>, --> NodeID
            "location" :    <String>,
            "value" :       <boolean>
        }

#### Release Result ####
Sent to the leader after receiving a release signal, notifies the leader if the book was 
successfully placed back into the available inventory. 

        {
            "source" :      "node",
            "type" :        "release",
            "title" :       <String>, 
            "id" :          <int>, --> NodeID
            "location" :    <String>,
            "value" :       <boolean>
        }

#### Borrow Result ####
Sent to the leader after receiving a borrow signal, notifies the leader if the book was 
successfully borrowed from this location. 

        {
            "source" :      "node",
            "type" :        "borrow",
            "title" :       <String>, 
            "userID" :      <int>, 
            "id" :          <int>, --> NodeID
            "location" :    <String>,
            "value" :       <boolean>
        }

#### Return Result ####
Sent to the leader after receiving a return signal, notifies the leader if the book was
successfully returned at this location.

        {
            "source" :      "node",
            "type" :        "return",
            "title" :       <String>, 
            "userID" :      <int>,
            "id" :          <int>, --> NodeID
            "location" :    <String>,
            "value" :       <boolean>
        }

#### Update ####
Sent to the leader after receiving an update signal, notified the leader of the current state of the 
borrowed books listing.

        {
            "source" :      "node",
            "type" :        "update",
            "location" :    <String>,
            <int> :         <String> --> UserID:title
        }
