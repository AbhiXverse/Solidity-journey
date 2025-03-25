
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
    - Example 
        - PUSH1 0x06 -> Push 1-byte value 0x06 onto the stack 
        - POP -> Remove the top item from the stack 
        - DUP1 -> Duplicated