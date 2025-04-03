
[Solidity-journey /Day 14/Uniswap working - Notes] - #1


What is Uniswap ? 

- Uniswap is a decentralized exchange (DEX) protocol on the Ethereum blockchain 
- It operates without trusted intermediaries (no centralized order book), ensuring decentralized, censorship resistance and security.


Core Concepts:

- Automated Market Maker (AMM) - 
    - Uniswap uses an AMM model instead of traditional order book for matching buyers and sellers

- Liquidity Pools:
    - A liquidity pool is a reserve of two ERC-20 tokens, managed by a Uniswap smart contract used for token swaps 



Constant Product Formula: 

- Uniswap's liquidity pools follow the Constant Product Formula - ```
```
X * Y = K
```
- X - Reserve of token A 
- Y - Reserve of token B 
- K - a constant value that must remains same or unchanged 

- Key point - when a trade occurs, the formula must hold so the product of the reserves (X * Y) stays equal to K 


Liquidity Providers (LPs): 

- How to become an LP: 
    - anyone can provide liquidity to a pool by depositing an equal value of two tokens (e.g: ETH or USDT) into the pool 

- Pool Tokens: 
    - In return, LPs receive pool token that represent their share in the pool 
    - these tokens track the LP's pro-rata share of the total pool 
    - LP's can r