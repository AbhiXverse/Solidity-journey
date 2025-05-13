



**Data Location** 

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
