
[Solidity-journey /Day 08/Solidity Notes] - 07


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

- Value types 