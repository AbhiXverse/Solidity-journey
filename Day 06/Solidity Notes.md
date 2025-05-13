[Solidity-journey /Day 06/Solidity - 101 Notes] - #06


**Contract Ownership & Security :-** 

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

**Modifiers (Adding extra logic to functions):-**

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











Understanding different integers sizes in Solidity 

- Solidity has different type of unsigned integers like uint8, uint16, uint32, uint64 up to uint256 

1. uint8 (0 to 255) 
    - Best for very small numbers like simple counters 
    - use when you're sure the value won't go above 255 and want to save storage 
    - e.g: Day , hour etc 
    
2. uint16 (0 to 65,535)
    - best for medium size numbers 
    - use when you're sure that values are within this range and want to save space 
    - e.g: Year, percentage values, item counts etc 

3. uint32 (0 to ~18.4 quintillion)
    -  best for medium counters 
    -  use when you're sure that values are within this range and want to save space 
    - e.g: game score, short duration timers etc 

4. uint64 (0 to ~3.4x10^38)
     - best for time based values or huge numbers 
     - use when you deal with time or very large numbers 
     - e.g : unix timestamps, very large numbers etc 

5. uint256 (0 to ~1.16 x 10^77)
    - best for most use cases related to financial values 
    - use for almost all financial values
    - e.g: token balances, Ether values, hash results etc 


Note : 
- Beginner tips: 

    - Start with uint256 - its the safest and most common 
    - default to uint256 for most cases like - Token amounts, ETH/Wei values, any financial calculations, IDs or unique identifiers 
    - Only use smaller sizes when you're absolutely sure about the max value 
    - Since - Solidity 0.8.0, overflow checks are automatic for all sizes but yeah choosing the right size based on the situation helps to reduce gas costs 
