
[Solidity-journey /Day 11/Solidity Notes] - #10


Special Array types: 

1. bytes vs byte[] -
    - bytes is tightly packed and cheaper than byte[]
    - use bytes1 to bytes32 if possible to save gas 
2. string - 
    - Similar to bytes, but cannot be accessed by index or modified 
    - means e.g:
        - A string is used to store text (like name, message etc )
        - It's similar to bytes, but you cannot access or change individual character
    
    