
[Secureum - Ethereum 101 - Day 09] - 07

**Ethereum Virtual Machine (EVM):**

- Quasi Turning-complete: Computation is bounded by gas 
- Executes bytecode of smart contract 

**Components**:
- Stack:
    - Max 1024 elements 
    - 256-bit words 
    - Operated using PUSH, POP, DUP, SWAP 
```
E.g: PUSH1 0x60, DUP1, SWAP1
```
- Memory: 
    - Byte-addressable 
    - Volatile 
    - Interacted using - MLOAD, MSTORE, MSTORE8
- Storage:
    - 256-bit key value store 
    - Non-volatile, part of blockchain state 
    - interacted using - SLOAD, SSTORE 
- Calldata: 
    - Read only, byte-addressable input data 
    - Interacted using: CALLDATASIZE, CALLDATALOAD, CALLDATACOPY 

**Code Execution** -
- Code is stored separately in virtual ROM 
- Not part of memory or storage, interacted with specific instructions 

Byte order 
- Big-endian format (means e.g 1234 ---> 12 34)(smallest to biggest)
    - Most significant byte (MSD) at lowest memory address 
    - Least significant byte (LSD) at highest memory address 