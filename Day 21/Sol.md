
**Contract type:**

- every contract defines its own type
- can convert contract to address
- only external / public functions and variables are accessibles from outside 

**Data types:**

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


**Data Locations:** 

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
