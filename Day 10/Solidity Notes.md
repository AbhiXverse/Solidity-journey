
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