[Solidity-journey /Day 22/Solidity - 101 Notes] - #16

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
