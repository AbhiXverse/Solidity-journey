
[Solidity-journey /Day 02/Solidity Notes]

- View & Pure functions: They don't cost gas 
     - View reads blockchain data
     - Pure only returns values without reading blockchain data 
     - If a gas-costing functions calls a pure function, it will cost gas
 - Structs: Use struct to create custom data types 
 - Strings: Special type in solidity; must specify memory or calldata 
 - Mapping: Stores key-value pairs.
 - Data storage locations: Only special types like strings, structs, tuples need memory or calldata 

Inheritance & Function Modifiers 

- Inheritance: 
    - Use the **is** keyword - like a contract can use the **is** keyword to inherit functions and variables from another contract 
- Overriding: 
     - Parent function must have **virtual** at the end 
     - Child function must have **override** at the end 

- Payment & Transactions 
    - Payable functions: Allow contract to receive Eth.
    - Checking payment value: Use **msg.value**, which represent the amount in Wei 
    - Require statement: Ensures conditions are met,
        - e.g:-  [require(msg.value > 1e18);      // Requires at least 1 Eth]
    - Nonce: Counts the number of transaction for an account

- Oracles & External data:
    - Oracles & chainlink: Help smart contract access real-world data
    - Smart contract can't directly - 
         - Connect to API 
         - Make external calls
         - Access off-chain data 
    - Oracles Problem: Smart contract must work in a predictable way, so they can't directly use things like random numbers or data from external APIs.