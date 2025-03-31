
[Solidity-journey /Day 12/Solidity Notes] - #11


Block and Transaction Properties:

1. Block Properties - 
    - Blockhash (uint blockNumber) -> bytes32
        - returns the hash of a specific block 
        - works only for the last 256 blocks, excluding the current block 
        - older block hashes return 0 due to scalability reasons 
    
    - block.chainid -> uint 
        - returns the current chain ID (helps prevent replay attacks across different chains) 
    
    - block.coinbase -> address payable 
        - returns the address of the miner (validator) who produced the block 
        
    - block.difficulty -> uint 
        - represents the difficulty level of mining the current block
        - In proof-of-stake (PoS) ethereum, this is replaced by **prevrandao** (used for randomness)
    
    - block.gaslimit -> uint 
        - maximum amount of gas allowed in the current block 
        - set by miners/validators and varies form the block to block 
    
    - block.number -> uint 
        - the block height i.e - the number of the current blokc in the blockchain 
    
    -  block.timestamp -> uint 
        - the timestamp of the block (in seconds since the Unix epoch)


    2. Transaction properties: 
        -  msg.data -> bytes calldata 
            - contains the entire calldata send with the transaction 
        
        - msg.sender -> address 
            - returns the address of the entity (EOA or contract) that initiated the current function call 
            - can change during external calls, so be safe when using it for authentication 
            - 
        - 
        
