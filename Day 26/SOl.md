
**Block and Transaction Properties:**

1. **Block Properties -** 
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


 2. **Transaction properties:** 
     - msg.data -> bytes calldata 
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
