
[Solidity-journey /Day 09/Solidity Notes] - 08


Boolean Type:

- Declared using - bool 
- Values - true, false 
- Operators - ! (not), && (and), | | (or), == (equal ), != (not equal)
- && and | | use short-circuit logic (stop if result is known early) 
  e.g: 
function sendToken (address user) public {
     if (user != address (0) && balance [user] > 0 )
}