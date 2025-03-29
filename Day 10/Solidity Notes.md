
[Solidity-journey /Day 10/Solidity Notes] - 09


Data types:

- Fixed-sized arrays - 
    - types - byte1, byte2,.... to byte32 
    - hold 1 to 32 bytes 
    - byte[] wastes space due to pading - better to use bytes instead 
- Literals - 
    - Address literals 
        - A valid Ethereum address is a hexadecimal value passing the checksum test (EIP - 55)
        - if an invalid checksum is used
