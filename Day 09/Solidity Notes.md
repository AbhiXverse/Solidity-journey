
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


