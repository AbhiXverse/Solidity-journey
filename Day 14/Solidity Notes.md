
[Solidity-journey /Day 14/Solidity Notes] - #13


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
- 