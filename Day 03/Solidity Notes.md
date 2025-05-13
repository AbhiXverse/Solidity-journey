[Solidity-journey /Day 03/Solidity Notes] - #03


- **View & Pure functions**: They don't cost gas 
     - View reads blockchain data
     - Pure only returns values without reading blockchain data 
     - If a gas-costing functions calls a pure function, it will cost gas
 - Structs: Use struct to create custom data types 
 - Strings: Special type in solidity; must specify memory or calldata 
 - Mapping: Stores key-value pairs.
 - Data storage locations: Only special types like strings, structs, tuples need memory or calldata 

**Inheritance & Function Modifiers :-**

- Inheritance: 
    - Use the **is** keyword - like a contract can use the **is** keyword to inherit functions and variables from another contract 
- Overriding: 
     - Parent function must have **virtual** at the end 
     - Child function must have **override** at the end 