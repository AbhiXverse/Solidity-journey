[Solidity-journey /Day 05/Solidity - 101 Notes] - #05


**Sending Transaction & funds :-** 

- How transaction works: 
     - Every transaction in Ethereum is just an HTTP post request sent to a node (RPC provider)
         - RPC Provider:- RPC stands for **Remote Procedure Call** in Etheruem is like a gateway that allows your computer or application to interact with the Ethereum blockchain.
 - Only "payable" addresses can receiver funds.
 - Convert an address to payable :- e.g:
```
payable(msg.sender);
```

- Three ways to send funds : 
     - transfer 
     - send 
     - call 
 - Difference between transfer, send & call is :-
     - transfer: 
        - has a gas limit of 2300 to prevent reentrancy attacks 
        - auto-reverts if the transaction fails 
    - send:
        - also has gas limit 2300
        - returns false instead of reverting, so you must manually check if it worked 
    - call: 
        - more flexible, can send Eth and even call any function without needing the contract's ABI.
        - e.g:-
```
(bool success, bytes memory data) = payable(msg.sender).call{value: address(this). balance}(""); 
require(success, "Transfer failed");
```








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











Custom Errors: 

- Custom errors are a way to define specific messages in solidity 
- They help you give clear feedback when something goes wrong in your contract 
- Main benefit: They use less gas compared to writing error messages as string like "Insufficient Balance"

How to write it :- 
E.g:
```
error ErrorName(type param1, type param2);
```


Contract Example : 
- Custom error in a Coin contract:
```
contract Coin {

    address public minter;                        // only the deployer of this contract becomes the minter 


   mapping(address => uint256) public balances;       // this keeps track of how many coins each address has

    
    event Sent(address from, address to, uint amount);    // event logs every successful coin transfer 

    constructor() {
        minter = msg.sender;                      // set contract deployer as minter
    }

    
    function mint(address receiver, uint amount) public {       // this fun. creates new coins and gives them to the receiver
        require(msg.sender == minter);                          // Only minter can mint coins 
        balances[receiver] += amount;                           // add new coins to the receiver's balance 
    }

    
    error InsufficientBalance(uint256 requested, uint256 available);   // custom error to show detailed info when balance is low 


    
    function send(address receiver, uint256 amount) public {              // this function lets anyone send their coins to someone else 
        if (amount > balances[msg.sender] 
        revert InsufficientBalance(amount, balances[msg.sender]));   // this make sure that sender has enough coins, if not then show the custom error message 
        balances[msg.sender] -= amount;                                // subtract the coins from sener 
        balances[receiver] += amount;                                  // add the coins to receiver
        emit Sent(msg.sender, receiver, amount);                       // trigger the sent event to show that a transfer happened
    }
}
```

 Custom error :-
```
error InsufficientBalance(uint256 requested, uint256 available);
```
- this error is used when someone tries to send more coins than they have 
- it takes two values: 
    - requested: how much the user wants to send 
    - available: how much they actually have 


How it is used in code: 
```
if (amount > balance[msg.sender] 
revert InsufficientBalance(amount, balance[msg.sender]));
```
- this line checks if the user has enough balance 
- if not, revert the transaction and show the custom error message with real values 
- this version is cheaper in gas 
- and it provides more info then just showing "insufficient balance"


Note 1:- 
- When using **custom errors** in solidity, you cannot pass that custom error directly to a require statement

- traditional require statement: you only pass the simple string message
e.g:
```
require(amount <= balance, "Insufficient balance");
```

- But with the custom errors: 
    - you need to use an **if** condition and then explicitly **revert** with your custom error:
      e.g: 
```
    if (amount > balance[msg.sender]) 
     revert InsufficientBalance (amount , balance[msg.sender]);
```



Note 2 :- 
- With Curly brackets in If condition:
  e.g : 
```
if (amount > balance) {
revert InsufficientBalance(amount, balance);
}
```
So, by using Curly bracket after the If condition, all the statements within the bracket are the part of the If condition 
and, 

- Without Curly bracket in If condition:
  e.g: 
```
if (amount > balance) 
revert InsufficientBalance (amount, balance);
```
So, in this only the next single statement is part of the If condition or only the first condition is controlled by the If condition. The second statement will always execute.

