# Requirements #

- [x] (7 points) You will need a README.md which contains the following (most goes to
   the protocol):
    - [x] A short screencast where you show your project in action and explain everything
   we need to know about it. (if you do not include a screencast you might loose
   more points if we cannot see some of your features)
    - [x] Explain your project and which requirements you were able to fulfill.
    - [x] Explain your protocol.  
- [x] (3 point) Project is well structured and easy to understand.
- [x] (3 points) We want to run the leader node through "gradle leader" with some default
   port that is set for us, so the client can easily connect to the leader.
- [x] (4 points) We want to start at least two separate nodes through gradle. It is ok to
   use something like "gradle runNode" with arguments you see fit. The node should
   then connect to the leader correctly (let us know in your README.md in which
   order we will have to start what). It is up to you to treat the nodes as servers or
   as clients to the leader – there are pros and cons to each. You can choose what you
   like best.
- [x] (3 points) Nodes need to start with initial book list. You can give a book list as txt
   as well as argument (make sure you have example txts or whatever you decide on
   in your repo), so that each node can potentially have a different book list. See the
   node as a specific "library". Please provide a list of possible books in your README
   so we know what requests we can enter.
- [x] (2 points) The client should start through "gradle client", connecting to the leader
   node. The client is the program that accepts user input.
- [x] (2 points) Leader will ask the Client for their clientID, which should be provided by
   the Client. It is ok to assume that the clientID is entered by the user or that the
   clientID is given when the Client is started as argument.
- [x] (3 points) Client will then have the choice between borrowing a book or returning a
   book. This should be a client side choice followed by the book name.
- [x] (2 points) The leader receives the request from the Client and has to handle the
   communication to the nodes/libraries.
- [x] Borrow (15 points):
    - [x] If the client wants a book they enter the book name and the request is sent to
    the leader.
    - [x] The leader will send the request to all nodes and ask if the book is available.
    - [x] If one node has the book available (so it is in their list and not borrowed yet)
      they will tell the leader in their response. If they book is available the node
      should "mark" the book as pending, to make sure a "double" booking with two
      requests at the same time cannot happen.
    - [x] The leader will then decide which node should be used to borrow (if one of
      them had the book available). The leader should then tell every node if the
      book should be borrowed or not from that particular node.
    - [x] Nodes will then either mark the book as borrowed or release the "pre-marking"
      to free the book. The node also needs to save who (clientID) borrowed the
      book.
- [x] Return (15 points):
    - [x] The client can return a book by choosing return and then entering the book
    name.
    - [x] The request will be sent to the leader.
    - [x] The leader will then send this "return" to the nodes and the node will check if
      this client borrowed this book and let the leader know what happened.
    - [x] If the client borrowed the book then it will be released, if the client did not
      borrow the book then nothing will change. The leader should of course inform
      the client about what the outcome is.
- [x] (3 points) You should make sure that when a node crashes the whole system does
    not go down. If the leader crashes then of course a restart might be needed but the
    data should be persistent.
- [x] (6 points) If a restart is needed, the first thing the leader should do is check in
    with the nodes and verify their records, to make sure that the borrowed books and
    who borrowed them is consistent. This means the leader and the nodes should keep
    records.
- [x] (6 points) This gets interesting if more than one client can interact with the leader
    and make requests. The system will need to make sure it handles them correctly
    and the order of transactions is still correct.