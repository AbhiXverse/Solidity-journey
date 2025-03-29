
[Solidity-journey /Day 11/Solidity Notes] - #10


Special Array types: 

1. bytes vs byte[] -
    - bytes is tightly packed and cheaper than byte[]
    - use bytes1 to bytes32 if possible to save gas 
2. string - 
    - Similar to bytes, but cannot be accessed by index or modified 
    - means e.g:
        - A string is used to store text (like name, message etc )
        - It's similar to bytes, but you cannot access or change individual characters using an index like mystring[0]
        - e.g: 
```
        string message = "Hello";

     You can't do this:
         bytes letter = message[0];
         // this will give you an error 

but if you want to access characters, you can convert it to bytes:

bytes memory temp = bytes(message);
bytes1 leter = temp[0];    // Now this wiorks, gives you "H"
```

Real Use case - String cannot be accessed by index 

- For example I am building a form in a DApp, and I want to validate that the user's name start with a capital letter (e.g: "Abhi', not "abhi")
code: 
```
function checkcapital(string memory name) public pure returns (bool) {
     bytes memory temp = bytes(name);
     if (temp.length == 0) return false;
     return (temp[0] >= 0x41 && temp[0] <= 0x5A);     // checks if the letter comes in the range of A to Z (ASCII) (capital letters range 65(0x41) to 90(0x5A) )
}
```



Memory Array:

- Created using new T[](size)
- Cannot be resized (no .push() or pop() available)
e.g 
```
uint256;     // fixed size
```


Struct Type:

- Custom data structures combining multiple values 
- can obtain arrays and mappings but not themselves 
e.g: 
```
struct Car {
     string model;
     uint256 year;
}
```


Mapping Types:

- Key-value pairs
e.g 
```
mapping(keyType  =>  ValueType) variablename;
```
- key can be primitive type (uint, bytes, address) 
- Value can be anything, including arrays and structs 
- Mapping are not iterable 
e.g 
```
mapping (address => uint256) public balances;
```
