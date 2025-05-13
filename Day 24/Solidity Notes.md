[Solidity-journey /Day 24/Solidity - 101 Notes] - #19

**Arrays:** 

- Can be fixed-size (uint256[3] numbers;) or dynamic size (uint[] numbers;)
- Indices are zero-based 
- arrays can store mappings and structs 

**Array Methods:** 

1. .length -> tells how many items are in the array 
e.g: 
```
uint[] numbers = [10, 20, 30];
uint256 count = numbers.length;   // count = 3 
```

2. .push() -> ads an empty (zero) value at the end of the array 
e.g: 
```
uint[] numbers;
numbers.push( );     // adds a zero  :  numbers = [0]
```

3. .push(x) -> adds x to the end of the array 
e.g: 
```
uint[] numbers;
numbers.push(2);      // numbers = [2]
numbers.push(4);      // numbers = [2, 4]
```

4. .pop() -> removes the last item from the array 
e.g: 
```
uint[] numbers = [5, 10, 15];
numbers.pop();       // numbers = [5, 10]  (15 is removed)
```


**Special Array types:** 

1. bytes vs byte[ ] -
    - bytes is tightly packed and cheaper than byte[]
    - use bytes1 to bytes32 if possible to save gas 
    
2. string - 
    - Similar to bytes, but cannot be accessed by index or modified 
    - means e.g:
        - A string is used to store text (like name, message etc )
        - It's similar to bytes, but you cannot access or change individual characters using an index like mystring[0]
         e.g: 
```
string message = "Hello";

You can't do this:

bytes letter = message[0];     // this will give you an error 
           

but if you want to access characters, you can convert it to bytes:

bytes memory temp = bytes(message);
bytes1 leter = temp[0];       // Now this wiorks, gives you "H"
```

**Real Use case - String cannot be accessed by index** 

- For example I am building a form in a DApp, and I want to validate that the user's name start with a capital letter (e.g: "Abhi', not "abhi")
  code e.g: 
```
function checkcapital(string memory name) public pure returns (bool) {
     bytes memory temp = bytes(name);
     if (temp.length == 0) return false;
     return (temp[0] >= 0x41 && temp[0] <= 0x5A);     // checks if the letter comes in the range of A to Z (ASCII) (capital letters range 65(0x41) to 90(0x5A) )
}
```



**Memory Array:**

- Created using new T[ ] (size)
- Cannot be resized (no .push() or pop() available)
  e.g 
```
uint256;     // fixed size
```


**Array Slices:** 

- Represent a portion of an array 
- written as array [start:end], where :
    - start is included 
    - end is excluded 
e.g: 
```
uint256[] calldata numbers = [1, 2, 3, 4, 5] ;
uint256[] calldata slice = number[1 : 4];       // result [2, 3, 4]
```
