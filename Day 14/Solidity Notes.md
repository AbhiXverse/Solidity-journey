
[Solidity-journey /Day 14/Solidity - 101 Notes] - #13

**Scoping Rules in Solidity:** 

1. Variables inside { } block are only visible there -
    - e.g: 
```
function demo() public {
     uint256 x = 5;   // x is only available inside this function 
}

//  Outside this function, x does not exist 
```
So, if you declare a variable inside a function or a block { }, you can't use it outside that block  


2. For-loop variables only exist inside the loop  -
    - e.g: 
```
function loop() public {
     for (uint i = 0; i < 5; i++)  {
         // i is visible only inside this for loop
     }
         // i is not available here 
}
```
the loop variable i is temporary - only works inside the loop 


3. Function/Modifiers parameters are only available inside that function - 
    - e.g: 
```
function add(uint256 a, uint256 b) public returns (uint) {
     return a + b;   // a and b are visible here 
}
// you cannot access a or b outside this function 
```
parameters like a and b are created when the function is called and go away after it finishes


4. State variables and functions are visible across the whole contract  -
    - e.g: 
```
contract Mycontract { 
    uint256 public number = 10;     // state variables 

    function get() public view returns (uint256) {
        return number;    // we can access 'number' from anywhere inside the contract 
    }
    function set() public {
              // number is still available here 
    }
}
```
state variables (declare outside any function) and functions are visible everywhere in the contract - even before they are declared in the code