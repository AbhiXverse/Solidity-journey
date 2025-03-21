[Solidity-journey /Day 04/Solidity Notes] - 03

Contract Ownership & Security :- 

- Assign a contract owner : 
    - Use a **constructor**, which runs only when the contract is deployed 
    - E.g : 
```
    contract Ownable {
    address public owner ;
 
    constructor () {
        owner = msg.sender; // Assigns contract deployer as the                                  owner 
        }
     }
```

Modifiers (Adding extra logic to functions):-

- Modifiers let you 

  
