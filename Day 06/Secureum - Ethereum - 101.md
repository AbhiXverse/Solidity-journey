
[Secureum - Ethereum 101 - Day 06] - 05

**Smart Contract in Ethereum :-**

- Smart contract are self-executing stored on the Ethereum blockchain.
- Smart contact can - 
     - Store and manage data 
     - Execute functions automatically when triggered by a transaction
     - Send and receive Ether 
     - Call other contracts 
 - Smart contract have their own address and cannot send transactions by themselves. 
 - Executed when an external transaction or another smart contract calls them.


**Ethereum Clients and Nodes :-** 

- Nodes: Computers running Ethereum software, storing blockchain data 
- Clients: Implementations of Ethereum protocol (e.g, Geth, OpenEtheruem)
- Nodes perform tasks like - 
     - Sharing transactions with others in the network 
     - Validating blocks 
     - storing blockchain history 
     


**Ethereum State & Merkle Patricia Tree :-** 

- Ethereum state is stored using a modified Merkle Patricia Tree (MPT).
- MPT ensures efficient storage and verification of Ehtereum's state. 
- Tree structure - 
     - Leaf nodes: Contains account data 
     - Intermediate nodes: Hashes of child nodes 
     - Root node: The top hash representing the entire state.



