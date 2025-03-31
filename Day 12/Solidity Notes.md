
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
