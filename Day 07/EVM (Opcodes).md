
Opcodes: 

- Opcode stands for operation code 
- these are the low-level instructions the Ethereum Virtual Machine(EVM) understand 
- think of opcodes like tiny commands or steps that the EVM runs when executing your smart contract 
- every smart contract written in solidity is complied down to opcode so the EVM can execute them 


Why are Opcodes Important ?

- They are the building blocks of smart contracts on Ethereum 
- Knowing them helps in :
     - gas optimization 
     - debugging 
     - security auditing 
     - understand what your contract really does under the hood 


Categories of Opcodes : 

- Stack Operations: 
    - the EVM uses a stack (lat in , first out)
    - e.g: 
        - PUSH1 0x06 -> Push 1-byte value 0x06 onto the stack 
        - POP -> Remove the top item from the stack 
        - DUP1 -> Duplicate the top item 
    
- Memory Operations:
    - Temporary memory used only during the execution 
    - e.g:
        - MLOAD -> load data form memory 
        - MSTORE -> store data in memory 
        - MSTORE8 -> store 1-byte in memory 
    
- Storage Operations: 
    - Permanent storage (stored on blockchain)
    - e.g: 
        - SLOAD -> load from contract storage 
        - SSTORE -> write to contract storage 
    
- Arithematic Operations: 
    - Basic math operations 
    - e.g :
        - ADD, SUB, MUL, DIV
    
- Comparison Operations: 
    - Logic checks and bitwise operations 
    - e.g: 
         - LT, GT, EQ, ISZERO -> less than, equal etc 
         - AND, OR, XOR, NOT 
    
 - Control flow:
    -  Change how code is executed 
    - e.g: 
        - JUMP, JUMP1 -> jump to specific code positions 
        - STOP, RETURN, REVERT 
    
- External Calls: 
    - Interact with other contracts 
    - e.g: 
        - CALL, DELEGATECALL, STATICCALL 
    
- Logging: 
    - Emit logs (used in events)
    - e,g: 
        - LOG0. LOG1 upto LOG4 


Simple Working Example of Opcode: 

```
uint a = 2 + 3 ;
```
this complies to opcode like:

```
PUSH1 0x02 
PUSH2 0x03 
ADD
```
Explain : 
- Push 2 and 3 onto the stack 
- use ADD to get 5 
- and that's it!


Gas and Opcodes:

- Each opcode has a gas cost 
- e.g :
    - ADD = 3 gas 
    - SSTORE = up to 20,000 gas (because it writes to permanent storage)
- Tool -> [EVM code ](https://www.evm.codes/) (check gas of each opcode)


