
[[Solidity Notes]]

- View & Pure functions: They don't cost gas 
     - View reads blockchain data
     - Pure only returns values without reading blockchain data 
     - If a gas-costing functions calls a pure function, it will cost gas
 - Structs: Use struct to create custom data types 
 - Strings: Special type in solidity; must specify memory or calldata 
 - Mapping: Stores key-value pairs.
 - Data storage locations: Only special types like strings, structs, tuples need memory or calldata 
 - 

