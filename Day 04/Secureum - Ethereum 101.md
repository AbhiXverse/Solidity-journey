[Secureum - Ethereum 101 - Day 04] - 03


Ethash (Ethereum's proof of Work Algorithm)

- Ethash is Ethereum's PoW algorithm (previously Dagger-Hashimoto) 
- It is memory-hard, making it ASIC-resistant and more GPU-friendly 

Ethereum Block Structure (Ethash)

- Each block consists of:
    - Block header 
    - Transactions 
    - ommers (uncle) block headers 
- Block header fields:
    - parentHash: 
        - Keccak-256 hash of the parent block's header 
    - ommersHash 
        - Keccak-256 hash of the ommers list 
    - beneficiary 
        - 160-bit address receiving transaction fees (miner reward)
    - stateRoot 
        - Root hash of the state trie (after all transaction) 
    - transactionRoot
        - Root hash of the receipts trie 
    - logsbloom 
        - Indicates how hash it is to mine this block 
    - number 
        - Block number (0 for genesis block) 
    - gasLimit 
        - Max gas allowed in this block 
    - gasused 
        - Total gas consumed by transactions in the block 
    - timestamp 
        - unix timestamp of block creation 
    - extraData 
        - optional data (max 32 byte) 
    - mixHash
        - 256-bit hash proving required computation was performed 
    - nonce
        - 64-bit number that solves the PoW challenge 


Gas refund & miner fees:

- Unused gas is refunded to the sender 
- Used gas(x gasPrice) is paid to the beneficiary(miner)
- E.g:
    - Gas limit = 21,000, used = 15,000
    - Refund = 6000 x gasPrice 
    - Miner gets 15000 x gasPrice 


Ethereum Virtual Machine (EVM)

- Quasi Turning-complete: Computation is bounded by gas 
- Executes bytecode of smart contract 

Components:
- Stack:
    - Max 1024 elements 
    - 256-bit words 
    - Operated using PUSH, POP, DUP, SWAP 
```
	    - E.g: PUSH1 0x60, DUP1, SWAP1
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

Code Execution 
- Code is stored separately in virtual ROM 
- Not part of memory or storage, interacted with specific instructions 

Byte order 
- Big-endian format (means e.g 1234 ---> 12 34)(smallest to biggest)
    - Most significant byte (MSD) at lowest memory address 
    - Least significant byte (LSD) at highest memory address 

Ethereum instruction set: 

- Stop & Arithematic: 
    - ADD, MUL, SUB, STOP 
- Comparison & Bitwise logic: 
    - EQ, LT, AND, XOR, OR 
- SHA3:
    - it is for computing Keccak-256 hash 
- Block Info: 
    - BLOCKHASH, COINBASE, TIMESTAMP, DIFFICULTY, GASLIMIT 
- Environmental Info:
    - ADDRESS, ORIGIN, CALLER, CALLVALUE 
- Stack, Memory, Stroage, FLow: 
    - MLOAD, SSTORE, JUMP, JUMPI
- Push Operations 