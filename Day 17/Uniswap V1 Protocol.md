
[Solidity-journey /Day 16/Uniswap working - Notes] -  #3

- Uniswap V1  - In Depth & Simple Notes

    - launched - November 2018 at Devon 4 
    - Purpose - A decentralized protocol for swapping ERC-20 tokens on Ethereum 
    - Design - Fully permissionless and open-source, anyone can use it
    - Philosophy - Focused on simplicity, decentralized, censorship resistance and security 


Features - 
1. Supports for all ERC-20 tokens - 
    - Anyone can create a trading pair(exchanging contract) for any ERC-20 token 

2. ETH-Token pairs only - 
    - Every token is paired with ETH, not directly with other tokens 
    - e.g - to trade token A for token B, you go: Token A -> ETH -> Token B

3. Liquidity Pools(LPs) - 
    - Users can deposit both ETH and a token into a pool 
    - In return, they get LP tokens that their share in the pool 

4. Automated Market Making - 
    - Uses the constant Product formula - X * Y = K 
    - X = ETH reserve , Y = Token reserve and K = constant 
    - guarantees that the product of ETH and token reserves remains the same after a trade 
    - larger trades cause more price slippage 

5. Fees - 
    - 0.3% fee on each trade 
    - collected fees stay in the pool and go to liquidity providers when they remove liquidity

6. Fully On-chain - 
    - All interactions happen on Ethereum 
    - Anyone can access it via smart contracts


Step-by-Step Working - 

1. Exchange contracts - 
    - One exchanges contract per token
    - create using the Uniswap factory contract 
    - stores reserves of ETH and ERC-20 token 

- Liquidity Provision - 
    - You deposit equal values of ETH and a token 
    - In return, you receive pool tokens 
    - Later, you can burn those tokens to get your share of the pool 

- Trading Process - 
    - You send ETH or token to the contract 
    - Based on reserves, it calculation how much of the other asset you'll get 
    - Swaps tokens using the constant product formula 

- Token to Token Trade - 
    - Since there are only ETH-token pairs, it uses ETH as a bridge 
    - E.g - to trade DAI for USDC 
        - DAI -> ETH -> USDC (2 transaction bundled into 1)

- Limit Order-Like Behaviour 
    - Users can set min/max bounds fir how much they're willing to receive/spend 
    - helps prevent unexpected slippage 

- Gas Optimization - 
    - At the time, Uniswap V1 had one of the lowest gas fees among DEXs





Now what are the limitation of Uniswap V1 lets see - 
- Only ETH pairs - could not directly trade between two tokens 
- High slippage for large trades - because of the formula used 
- No fee customization - always 0.3% (not adjustable) 
- No flasg