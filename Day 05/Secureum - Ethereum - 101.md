[Secureum - Ethereum 101 - Day 05] - 04

Cryptography in Ethereum:- 

- Two types of cryptography: 
    - Symmetric cryptography: Uses the same key for encryption and decryption. 
    - Asymmetric cryptography(Public-key cryptography): Uses two keys, a public key and a private key.
- Ethereum uses asymmetric cryptography for digital signatures 
  (not for encryption).
- Digital Signature Algorithm used: ECDSA (Elliptic Curve Digital Signature Algorithm).
- Elliptic Curve Cryptography (ECC): A method of public-key cryptography using mathematical properties of elliptic curves.
- Curve used: SECP-256K1 (same as Bitcoin).
- Keys -
    - Private key: A 256-bit random number, secret, used to generate the public key.
    - Public key: Generated from the private key and used to derive the Ethereum address.
- Ethereum addresses: Derived from the last 20 bytes of the Keccak-256 hash of the public key.

Ethereum Accounts:-

- Ethereum accounts store and manage funds and transaction. 
- Two types of accounts -
     1. Externally Owned Accounts (EOAs): Controlled by private keys
     2. Contract Accounts: Controlled by smart contract code
- Fields in an Ethereum accounts -
    - Nonce: Prevents duplicate transactions
    - Balance: Account of Ether held 
    - Contract code: Present only in contract accounts 
    - Storage: Stores contract data, initially empty

Transaction in Ethereum:- 

- A transaction is a signed message that changes Ethereum's state.
- Transaction are created by EOAs and broadcasted to the network .
- Components of a transaction: 
     - Nonce: Transaction count from the sender's account 
     - Gas price: Fee per gas uint (measured in Wei) 
     - Gas limit: Maximum gas allowed for the transaction
     - Recipient: Address receiving the transaction
     - Value: Amount of Ether being sent
     - Data: Extra information, mainly for smart contract 
     - v, r, s : Digital signature values verifying transaction authenticity
 - Types of transaction - 
     - Value transfer transactions: Sending Ether from one account to another 
     - Contract creation transactions: Deploying new smart contracts
     - Contract interaction transactions: Calling functions in deployed smart contracts
 - Transactions properties - 
     - Atomic: Either fully executes or fails (all - or - nothing)
     - Serial: Processed one after another 
     - Inclusion: Depends on network congestion and gas fees 
     - Order: Miners decide transaction order based on gas fees

Smart Contract in Ethereum 

- Smart contract are self-executing stored on the Ethereum blockchain.
- Smart contact can - 
     - Store and manage data 
     - Execute functions automatically when triggered by a transaction
     - Send and receive Ether 
     - Call other contracts 
 - Smart contract have their own address and cannot send transactions by themselves. 
 - Executed when an external transaction or another smart contract calls them.

Ethereum Clients and Nodes :- 

- Nodes: Computers running Ethereum software, storing blockchain data 
- Clients: Implementations of Ethereum protocol (e.g, Geth, OpenEtheruem)
- Nodes perform tasks like - 
     - Sharing transactions with others in the network 
     - Validating blocks 
     - storing blockchain history 

Ethereum State & Merkle Patricia Tree :- 

- Ethereum state is stored using a modified Merkle Patricia Tree (MPT).
- MPT ensures efficient storage and verification of Ehtereum's state. 
- Tree structure - 
     - Leaf nodes: Contains account data 
     - Intermediate nodes: Hashes of child nodes 
     - Root node: The top hash representing the entire state.






[]
Ethash (Ethereum's proof of Work Algorithm):

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




















6
Ethereum Virtual Machine (EVM):

- Quasi Turning-complete: Computation is bounded by gas 
- Executes bytecode of smart contract 

Components:
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
- Push Operations:
    - PUSH1 TO PUSH32 
- Duplication Operations
    - DUP1 to DUP16 
- Exchange Operations: 
    - SWAP1 to SWAP16
- Logging Operations:
    - LOG0 to LOG4
- System Operations:
    - CREATE, CALL, DELEGATECALL, SELFDESTRUCT, RETURN 