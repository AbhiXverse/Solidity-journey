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


