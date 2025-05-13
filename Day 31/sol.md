
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

