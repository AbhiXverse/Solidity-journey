
[Solidity-journey /Day 13/Solidity - 101 Notes] - #12


**Solidity data types:** 


1. **Value types (copied when used) -** 
```
bool, int, uint, address, contract, byte1-32 ,enum, function
```
- Always passes by value (copied on use)
-  they are immutable 

2. **Reference type (point to data)**
```
array, struct, mapping, string, bytes
```
- changes made via one reference affect all  



**Default Values:** 

- Uninitialized variables = default value (zero state)
- e.g:
```
bool            -> false 
uint/int        -> 0 
address         -> 0x0
enum            -> first member 
string/byte/array -> empty
```
