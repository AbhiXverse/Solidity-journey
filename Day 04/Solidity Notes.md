[Solidity-journey /Day 04/Solidity Notes] - #04

Contract Ownership & Security :- 

- Assign a contract owner : 
    - Use a **constructor**, which runs only when the contract is deployed 
    - E.g : 
```
    contract Ownable {
    address public owner ;
 
    constructor () {
        owner = msg.sender; // Assigns contract deployer as the                                           owner 
        }
     }
```
Modifiers (Adding extra logic to functions):-

- Modifiers let you add reusable checks to functions 
- E.g : 
```
  modifier onlyowner( ) {
      require(msg.sender == owner, "Not the owner");
      _;
     }

	  function withdraw() public onlyowner {
	     payable(owner). transfer(address(this).balance); 
	     }
   }
```
here, only the contract owner can withdraw the Eth.

Constant & Immutable Variables :- 

- Constant:- Cannot be changed, written in All Caps
- Immutable :- Can be set once (e.g, in the constructor)
- E.g: 
```
  contract Example {
     uint256 public constant FEE - 1000;  // Never changes
     address public immutable i_owner;
     
  constructor() {
      i_owner = msg.sender;   // set only once 
      
  }  
}
```
why use them ?
- Stored in bytecode, not storage slots, so they save gas.


Receiving Eth without a function call :- 

- If someone sends Eth without calling a function, Solidity uses: 
    - receive() function - when Eth is sent without any data
    - fallback() function - when data is sent, but no matching function exists
    - E.g - 
```
   contract ReceiveExample {
      event Received(address sender, uint256 amount);
      
      receive() external payable {
          emit Receivced(msg.sender, msg.value);
      }
    }
```
this contract logs the sender and amount when it receives Eth.

Events & Logging :- 

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


Indexed vs. Non-indexed Event parameters :- 

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


Emit:

- Use emit to trigger an event
- e.g -
```
emit deposit(msg.sender, _id, msg.value);
```
this sends out a signal with the details so outside apps can know something happened in the contract