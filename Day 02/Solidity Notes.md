
[Solidity-journey /Day 02/Solidity Notes] - #02


**SPDX License:** 
- SPDX = Software Package Data Exchange 
- Included in bytecode metadata for machine readability 

**Pragmas:** 

- Syntax - pragma solidity x.y.z;
- Example - pragma solidity ^0.8.3; 
     - allows version form 0.8.3 to <0.9.0 (called floating pragmas )
 - you can use combination like >=0.8.0 <0.8.3

**NatSpec tags:** 

- @title - contract/interface title 
- @author - Author 
- @notice - End-user explanation 
- @dev - Developer notes 
- @param - for parameters 
- @return - for return values 
- @inheritance - inherit doc from base 

**Function visibility:** 

- Public - accessible everywhere 
- External - calldata from outside (use this.function() for internal calls)
- Internal - only within contract or derived contract 
- Private - only within declaring contract 