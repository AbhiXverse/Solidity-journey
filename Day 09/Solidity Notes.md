
[Solidity-journey /Day 09/Solidity - 101 Notes] - #08

**Events & Logging :-** 

- Events helps track changes in a contract without using storage (save gas)
- the frontend (or indexers like Chainlink/Thegraph) listens for events 
- Events are meant for off-chain applications
  E.g: 
```
  contract EventExample {
    event Deposit(address indexed user, uint256 amount);
    
    function deposit() public payable  {
       emit Deposit(msg.sender, msg.value) 
    }
 }
```
here, whenever someone sends Eth to this contract, it shows (logs) who sent it and how much they sent.


**Indexed vs. Non-indexed Event parameters :-** 

- Indexed Parameters :- 
    - Can have up to 3 indexed fields 
    - help in filtering/ searching events efficiently 
    - Indexing event parameters created searchable topics 

- Non-indexed parameters :- 
    -  Need the ABI to decode
  E.g: 
```
event Transfer(address indexed from, address indexed to, uint256 amount);
emit Transfer(msg.sender, receive, amount);
```
Here, the indexed keyword helps find transactions faster in blockchain explorers.


**Emit**:

- Use emit to trigger an event
- e.g -
```
emit deposit(msg.sender, _id, msg.value);
```
this sends out a signal with the details so outside apps can know something happened in the contract





