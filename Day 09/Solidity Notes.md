
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





**Custom Errors:** 

- Custom errors are a way to define specific messages in solidity 
- They help you give clear feedback when something goes wrong in your contract 
- Main benefit: They use less gas compared to writing error messages as string like "Insufficient Balance"

**How to write it :-** 
E.g:
```
error ErrorName(type param1, type param2);
```


**Contract Example :** 
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


Struct: 

- Structs are custom data types that group different variables together 
- Useful for organizing realted data(like address + amount)
- Access struct members using a dot (.)  - e.g: s.user, s.amount


Enums:

- Used to define a list of constant values (like options)
- Improves readability 
- Values start from 0 to go up (0,1,2....)
- can be converted to/from integers 
- first value is the default 
- can have 1 to 256 members 


Constructor 

- Runs only once when the contract is deployed 
- Used to set initial values 
- Only one constructor is allowed per contract 
- Not part of the final deployed code 


Receive Function:

- Runs when the contract gets plain Ether (with empty calldata)
- Only one receive function allowed per contract 
- Can't take inputs or return anything 
- limited to 2300 gas (can't do much logic)
- can receive Ether via. **send()** or **.transfer()**
E.g: Syntax
```
receive( ) external payable {...}
```


Fallback Function:

- Used when - 
    - Call doesn't math any function 
    - or calldata is non-empty and no receive() is present
- It must be external, can be payable if you want to receive the Ether 
- also limited to 2300 gas if used for Ether receiving 
- e.g: 
```
fallback() external 

or 

fallback(byte calldata) external returns (bytes memory)
```



Solidity data types: 


1. Value types (copied when used) - 
```
bool, int, uint, address, contract, byte1-32 ,enum, function
```
- Always passes by value (copied on use)
-  they are immutable 

2. Reference type (point to data)
```
array, struct, mapping, string, bytes
```
- changes made via one reference affect all  



Default Values: 

- Uninitialized variables = default value (zero state)
- e.g:
```
bool            -> false 
uint/int        -> 0 
address         -> 0x0
enum            -> first member 
string/byte/array -> empty
```



Scoping Rules in Solidity: 

1. Variables inside { } block are only visible there 
    - e.g: 
```
function demo() public {
     uint256 x = 5;   // x is only available inside this function 
}

//  Outside this function, x does not exist 
```
So, if you declare a variable inside a function or a block { }, you can't use it outside that block  


2. For-loop variables only exist inside the loop 
    - e.g: 
```
function loop() public {
     for (uint i = 0; i < 5; i++)  {
         // i is visible only inside this for loop
     }
         // i is not available here 
}
```
the loop variable i is temporary - only works inside the loop 


3. Function/Modifiers parameters are only available inside that function
    - e.g: 
```
function add(uint256 a, uint256 b) public returns (uint) {
     return a + b;   // a and b are visible here 
}
// you cannot access a or b outside this function 
```
parameters like a and b are created when the function is called and go away after it finishes


4. State variables and functions are visible across the whole contract  
    - e.g: 
```
contract Mycontract { 
    uint256 public number = 10;     // state variables 

    function get() public view returns (uint256) {
        return number;    // we can access 'number' from anywhere inside the contract 
    }
    function set() public {
              // number is still available here 
    }
}
```
state variables (declare outside any function) and functions are visible everywhere in the contract - even before they are declared in the code




Boolean Type:

- Declared using - bool 
- Values - true, false 
- Operators - ! (not), && (and), | | (or), == (equal ), != (not equal)
- && and | | use short-circuit logic (stop if result is known early) 
  e.g: 
```
function sendToken (address user) public {
     if (user != address (0) && balance [user] > 0) {
     }
}
```
if the user is the zero address (invalid), solidity doesn't even check the balance


Integers Types: 

- Signed (int) & Unsigned (uint) of various sizes - int8 to int256, uint8 to uint256 
- int and uint are short form for the 256-bit version 
- Operators:
    - Comparison: <,  >,  <=,  >=,  == ,  !=
    - Bitwise: &,  |,  ^,  ~
    - Shifts: << ,  >>
    - Arithmetic: +,  -,  * ,  / ,  %,  **
- Checked and Unchecked Math: 
    - By default - Checked -> erros on overflow/ underflow
    - Use unchecked {} -> to disable safety checks (faster, but riskier)


Address Types:

- address -> 20-byte Ethereum address 
- address payable -> can be used whenever address is expected 


Transfer vs Send: 

- transfer() -
    - sends Ether, reverts the failure 
    - fixed 2300 gas 
    - safe and simple to use 
- send() - 
     - returns false on failure (doesn't revert) 
     - must manually check the return value 


Call / Delegatecall / Staticcall:

- call():
    - low-level call , forwards all gas 
    - use with encoded data 
    - can send Ether 
- delegatecall() - 
    - uses target contract's code but current contract's state 
    - used for libraries 
- staticcall() - 
     - Same as call() but doesn't allow state changes 


Contract type:

- every contract defines its own type
- can convert contract to address
- only external / public functions and variables are accessibles from outside 
