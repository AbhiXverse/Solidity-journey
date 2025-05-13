

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





Data types:

- Fixed-sized arrays - 
    - types - byte1, byte2,.... to byte32 
    - hold 1 to 32 bytes 
    - Use bytes instead of byte[] to optimize storage and gas 

- Literals - 
    - Address literals:
        - A valid Ethereum address is a hexadecimal value passing the checksum test (EIP - 55)
        - if an invalid checksum is used, solidity throws an error
        - Addresses must be between 39 to 41 characters
    
    - Integers & Rational literals:
        - Integers liternals - only numbers (0-9), without a decimal point (e.g: 123)
        - Rational literals  - contains a decimal point (e.g: 12.34)
        - Scientific notations - numbers of exponential format (e.g: 1.2e3 -> 1200)
        - Underscores*() - used for readability (e.g: 1_00_00 is same as 10000)
    
    - String literals: 
        - Enclosed in single quotes('abhi') or double quotes ("abhi") 
        - Only printable ASCII characters allowed 
        - supports escape characters (e.g: \n for new line)
    
    - Unicode literals:
        - Prefixed with unicode, supporting UTF-8 encoding
        - e.g: unicode"hello(emoiji)" 
    
    - hexadecimal literals:
        - prefixed with hex, used for raw byte data 
        - e.g: hex"001122FF" is a sequence of raw bytes 


Data Locations: 

- Solidity has three data locations that determines how the data is stored and accessed 

1. memory: 
    - used for temporary data inside functions 
    - data disappears after functions execution 
    - e.g: function arguments and temporary variables 

2. storage:
    - used for state variables (persistant data stored in the contract)
    - e.g: 
```
uint256 public storedData;    // stored in blockchain permanently 
```

3. Calldata: 
    - similar to memory. but read-only 
    - used for external function arguments to optimize gas usage 
    - e.g: 
```
function examplefun (string calldata _data) external { }
```


Data Locations & Assignments:

- Storage <-> Memory - creates a copy 
    - e.g - this is like copying a photo from your phone to your laptop - changing one doesn't affect the other 

- Memory <-> Memory - creates a reference 
     - e.g - like giving someone access to your google docs. If one updates it, the other can sees the change too 

 - Storage <-> Storage - also create a reference 
     - e.g - same as the upper one - like google doc. where more then 1 person can able to work one a doc and everyone can sees the changes



Arrays: 

- Can be fixed-size (uint256[3] numbers;) or dynamic size (uint[] numbers;)
- Indices are zero-based 
- arrays can store mappings and structs 

Array Methods: 

1. .length -> tells how many items are in the array 
e.g: 
```
uint[] numbers = [10, 20, 30];
uint256 count = numbers.length;   // count = 3 
```

2. .push() -> ads an empty (zero) value at the end of the array 
e.g: 
```
uint[] numbers;
numbers.push( );     // adds a zero  :  numbers = [0]
```

3. .push(x) -> adds x to the end of the array 
e.g: 
```
uint[] numbers;
numbers.push(2);      // numbers = [2]
numbers.push(4);      // numbers = [2, 4]
```

4. .pop() -> removes the last item from the array 
e.g: 
```
uint[] numbers = [5, 10, 15];
numbers.pop();       // numbers = [5, 10]  (15 is removed)
```



Special Array types: 

1. bytes vs byte[ ] -
    - bytes is tightly packed and cheaper than byte[]
    - use bytes1 to bytes32 if possible to save gas 
2. string - 
    - Similar to bytes, but cannot be accessed by index or modified 
    - means e.g:
        - A string is used to store text (like name, message etc )
        - It's similar to bytes, but you cannot access or change individual characters using an index like mystring[0]
         e.g: 
```
string message = "Hello";

You can't do this:

bytes letter = message[0];     // this will give you an error 
           

but if you want to access characters, you can convert it to bytes:

bytes memory temp = bytes(message);
bytes1 leter = temp[0];       // Now this wiorks, gives you "H"
```

Real Use case - String cannot be accessed by index 

- For example I am building a form in a DApp, and I want to validate that the user's name start with a capital letter (e.g: "Abhi', not "abhi")
  code e.g: 
```
function checkcapital(string memory name) public pure returns (bool) {
     bytes memory temp = bytes(name);
     if (temp.length == 0) return false;
     return (temp[0] >= 0x41 && temp[0] <= 0x5A);     // checks if the letter comes in the range of A to Z (ASCII) (capital letters range 65(0x41) to 90(0x5A) )
}
```



Memory Array:

- Created using new T[ ] (size)
- Cannot be resized (no .push() or pop() available)
  e.g 
```
uint256;     // fixed size
```


Array Slices: 

- Represent a portion of an array 
- written as array [start:end], where :
    - start is included 
    - end is excluded 
e.g: 
```
uint256[] calldata numbers = [1, 2, 3, 4, 5] ;
uint256[] calldata slice = number[1 : 4];       // result [2, 3, 4]
```



Struct Type:

- Custom data structures combining multiple values 
- can obtain arrays and mappings but not themselves 
  e.g: 
```
struct Car {
     string model;
     uint256 year;
}
```



Mapping Types:

- Key-value pairs
  e.g 
```
mapping(keyType  =>  ValueType) variablename;
```
- key can be primitive type (uint, bytes, address) 
- Value can be anything, including arrays and structs 
- Mapping are not iterable 
e.g 
```
mapping (address => uint256) public balances;
```



Block and Transaction Properties:

1. Block Properties - 
    - Blockhash (uint blockNumber) -> bytes32
        - returns the hash of a specific block 
        - works only for the last 256 blocks, excluding the current block 
        - older block hashes return 0 due to scalability reasons 
    
    - block.chainid -> uint 
        - returns the current chain ID (helps prevent replay attacks across different chains) 
    
    - block.coinbase -> address payable 
        - returns the address of the miner (validator) who produced the block 
        
    - block.difficulty -> uint 
        - represents the difficulty level of mining the current block
        - In proof-of-stake (PoS) ethereum, this is replaced by **prevrandao** (used for randomness)
    
    - block.gaslimit -> uint 
        - maximum amount of gas allowed in the current block 
        - set by miners/validators and varies form the block to block 
    
    - block.number -> uint 
        - the block height i.e - the number of the current blokc in the blockchain 
    
    -  block.timestamp -> uint 
        - the timestamp of the block (in seconds since the Unix epoch)


    2. Transaction properties: 
        -  msg.data -> bytes calldata 
            - contains the entire calldata send with the transaction 
        
        - msg.sender -> address 
            - returns the address of the entity (EOA or contract) that initiated the current function call 
            - can change during external calls, so be safe when using it for authentication 
        
        - msg.value -> uint 
            - the amount of wei sent with the message
        
        - tx.gasprice -> address 
             - the gas price (in wei) that the sender agreed to apy per uint of gas 
        
         - gasleft() -> uint 
              - returns the remaining has of execution 
              - useful to prevent out-of-gas errors in loops or complex logics 
            
          - tx.origin -> address 
              - the original sender of the transaction  






ABI (Application binary interface) Encoding/decoding 

- What is ABI ? 
    -  this is a standard where you can interact between smart contracts and external actors (e.g - other contracts, applications)

- Encoding/ Decoding: 
    - Encoding - Converts data (like number, adresses etc) into a format suitable for EVM 
    - Decoding - converts raw transaction data back  into human readable format 

- Tools: 
    - web3.js, ether.js and solidity libraries help interact with ABI 


Data Location 

- Storage:
    - Persistent state - variables stored here cost gas to modify 
    - data is kept on-chain 
    - e.g - state variables inside contracts 
     e.g 
```
contract StorageEg {
    uint256 public storedNumber;        // stored in storage (persistent)
      
      function setNumber(uint256 _num) public {
          storedNUmber = _num;       // writing in storage (costs gas)
    }
}
```

- Memory:
     - Temporary data - used for computation 
     - faster than storage, but volatile (lost after function call)
     - e.g - variables declared inside functions
     e.g 
```
contract MemoryEg {
     function getMemory() public pure returns (string memory) {
         string memory tempstring = "Hello Abhi";   // Stored in memory   
         return tempstring;                         // Existed only diring function execution 
    }
}
```

 - Stack:
     - Temporary as well but high speed storage 
     - stores simple values and function return values 
      e.g:
```
contract StackEg {
    function addNumber() public pure returns (uint) {
        uint256 a = 10;      // stored in stack 
        uint256 b = 20;      // stored in stack 
        uint sum = a + b;    // stored in stack 
        return sum;          // the result is also stroed in stacl but temporarily 
    }
}
```


Literals: 

- Literals types refers to fixed values in solidity (like numbers )
- e.g -
    - uint256 = 5  (a literal value for a uint type)
    - "Abhi" (a string literal)


Conversion Rules: 

- Implicit conversion - 
    - solidity automatically converts between compatible types (e.g - smaller integer to larger integer)

- Explicit conversion - 
    -  we need to manually convert between types, this is also called as type casting (e.g - uint8(5))
        - converting between uint types (uint256 to uint8)
        - Address to byte conversion and vice versa 







Storage/Gas behavior of Arrays and Mapping: 

- Arrays: 
    - Storage arrays - dynamic arrays cost gas based on the size and type of data stored 
    - Memory arrays - no gas costs for storage cuz they are temporary 
    - fixed sized arrays - they are more efficient but less flexible 
    - gas cost increases with the size and number of elements in an array 

- Mappings: 
    - mappings do not have length property, you can't easily check how many entries exist 
    - gas cost depends on how many entries you add
    - keys are hashed, so access is quick and efficient 
    - mapping are more gas efficient then arrays cuz you don't need to go through every single item to find something 


Byte Arrays: 

- Arrays of bytes represent fixed length or dynamic byte arrays 
- efficient for representing raw data (e.g - hashes, encrypted data etc) 
- dynamic byte arrays(bytes) cost more in gas compared to fixed-size byte arrays(bytes32)


Enums:

- A custom type with a finite set of values
  e.g 
```
enum status {pending, completed, cancelled} 
```
- provides better readability 
- Enums are cheaper than strings for storing predefined states 
