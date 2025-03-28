
[Solidity-journey /Day 09/Solidity Notes] - 08


Boolean Type:

- Declared using - bool 
- Values - true, false 
- Operators - ! (not), && (and), | | (or), == (equal ), != (not equal)
- && and | | use short-circuit logic (stop if result is known early) 
  e.g: 
```
function sendToken (address user) public {
     if (user != address (0) && balance [user] > 0) {
     }
}
```
if the user is the zero address (invalid), solidity doesn't even check the balance


Integers Types: 

- Signed (int) & Unsigned (uint) of various sizes - int8 to int256, uint8 to uint256 
- int and uint are short form for the 256-bit version 
- Operators:
    - Comparison: <,  >,  <=,  >=,  == ,  !=
    - Bitwise: &,  |,  ^,  ~
    - Shifts: << ,  >>
    - Arithmetic: +,  -,  * ,  / ,  %,  **
- Checked and Unchecked Math: 
    - By default - Checked -> erros on overflow/ underflow
    - Use unchecked {} -> to disable safety checks (faster, but riskier)


Address Types:

- address -> 20-byte Ethereum address 
- address payable -> can be used whenever address is expected 


Transfer vs Send: 

- transfer() -
    - sends Ether, reverts the failure 
    - fixed 2300 gas 
    - safe and simple to use 
- send() - 
     - returns false on failure (doesn't revert) 
     - must manually check the return value 


Call/ Delegatecall / Staticcall:

- call():
    - low-level call , forwards all gas 
    - use with encoded data 
    - can send Ether 
- delegatecall() - 
    - uses target contract's code but current contract's state 
    - used for libraries 
- staticcall() - 
     - Same as call() but doesn't allow state changes 


Contract type:

- every contract defines its own type
- can convert contract to address
- only external / public functions and variables are accessibles from outside 
