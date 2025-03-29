
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
    
    