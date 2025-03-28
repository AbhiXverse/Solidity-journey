
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


1. Value types (copied when used) - 
```
bool, int, uint, address, contract, byte1-32 ,enum, function
```
- Always passes by value (copied on use)

2. Reference type (point to data)
```
array, struct, mapping, string, bytes
```
- changes made via one reference affect all   



Default Values: 

- Uninitialized variables = default value (zero state)
- e.g:
```
bool            -> false 
uint/int        -> 0 
address         -> 0x0
enum            -> first member 
string/byte/array -> empty
```



Scoping Rules in Solidity: 

1. Variables inside { } block are only visible there 
    - e.g: 
```
function demo() public {
     uint x = 5;   // x is only available inside this function 
}

//  Outside this function, x does not exist 
```
So, if you declare a variable inside a function or a block { }, you can't use it outside that block  


2. For-loop variables only exist inside the loop 
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


- Function/Modifiers parameters are only available inside that function
    - e.g: 
```
function add(uint a, uint b) public returns (uint) {
     return a + b;   // a and b are visible here 
}
// you cannot access a or b outside this function 
```
parameters like a and b are created when the function is called and go away after it finishes


- State variables and functions are visible across the whole contract  
    - e.g: 
``
    contract Mycontract { 
        uint public number = 10;     // state variables 

        function get() public view returns (uint) {
            return number;    // we can access 'number' from anywhere inside the contract 
        }
         function set() public {
              // number is still available here 
        }
     }
```
state variables (declare outside any function) and functions are visible everywhere in the contract - even before they are declared in the code