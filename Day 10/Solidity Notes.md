
[Solidity-journey /Day 10/Solidity Notes] - 09


Data types:

- Fixed-sized arrays - 
    - types - byte1, byte2,.... to byte32 
    - hold 1 to 32 bytes 
    - Use bytes instead of byte[] to optimize storage and gas 

- Literals - 
    - Address literals:
        - A valid Ethereum address is a hexadecimal value passing the checksum test (EIP - 55)
        - if an invalid checksum is used, solidity throws an error
        - Addresses must be between 39 to 41 characters
    
    - Integers & Rational literals:
        - Integers liternals - only numbers (0-9), without a decimal point (e.g: 123)
        - Rational literals  - contains a decimal point (e.g: 12.34)
        - Scientific notations - numbers of exponential format (e.g: 1.2e3 -> 1200)
        - Underscores*() - used for readability (e.g: 1_00_00 is same as 10000)
    
    - String literals: 
        - Enclosed in single quotes('abhi') or double quotes ("abhi") 
        - Only printable ASCII characters allowed 
        - supports escape characters (e.g: \n for new line)
    
    - Unicode literals:
        - Prefixed with unicode, supporting UTF-8 encoding
        - e.g: unicode"hello(emoiji)" 
    
    - hexadecimal literals:
        - prefixed with hex, used for raw byte data 
        - e.g: hex"001122FF" is a sequence of raw bytes 


Data Locations: 

- Solidity has three data locations that determines how the data is stored and accessed 

1. memory: 
    - used for temporary data inside functions 
    - data disappears after functions execution 
    - e.g: function arguments and temporary variables 

2. storage:
    - used for state variables (persistant data stored in the contract)
    - e.g: 
```
uint256 public storedData;    // stored in blockchain permanently 
```

3. Calldata: 
    - similar to memory. but read-only 
    - used for external function arguments to optimize gas usage 
    - e.g: 
```
function examplefun (string calldata _data) external { }
```


Data Locations & Assignments:

- Storage <-> Memory - creates a copy 
    - e.g - this is like copying a photo from your phone to your laptop - changing one doesn't affect the other 

- Memory <-> Memory - creates a reference 
     - e.g - like giving someone access to your google docs. If one updates it, the other can sees the change too 

 - Storage <-> Storage - also create a reference 
     - e.g - same as the upper one - like google doc. where more then 1 person can able to work one a doc and everyone can sees the changes



Arrays: 

- Can be fixed-size (uint256[3] numbers;) or dynamic size (uint[] numbers;)
- Indices are zero-based 
- arrays can store mappings and structs 

Array Methods: 

1. .length -> tells how many items are in the array 
e.g: 
```
uint[] numbers = [10, 20, 30];
uint count = numbers.length;   // count = 3 
```

2. .push() -> ads an empty (zero) value at the end of the array 
e.g: 
```
uint[] numbers;
numbers.push( );    // adds a zero  :  numbers = [0]
```

3. .push(x) -> adds x to the end of the array 
e.g: 
uint[ nu]