
[Solidity-journey /Day 16/Uniswap working - Notes] - #2 


Impact of the Constant product Formula 

- Bigger trade get worse price -  
     - If someone tries to trade a large amount, they get a bad rate. This helps keep prices stable 

 - Price changes faster with big trades - 
     - The bigger the trade, the faster the price moves. This stops people from doing trades that can change the price too much. 


Fees and Rewards for LPs: 

- Transaction fees - 
    - Uniswap applies a 0.30% fee each trade. This fees is added to the reserves of the liquidity pool
    - the fee is distributed to the LPs based on their shares of the pool 

- Fee structure - 
    - In the future, Uniswap may adjust the fee to 0.25%, with the remaining 0.05% reserved as a protocol fee  


Arbitrage and Price Adjustment: 

- divergences between Uniswap's token prices and external markets can create arbitrage opportunities 
- traders take advantage of price difference between Uniswap and other exchanges 


Benefits of Uniswap's Design: 

- No Middleman - No trusted intermediary is needed, ensuring decentralized and trustless trades 
- Permissionless - Anyone can create a liquidity pool, allowing for the exchanges of any pair of ERC-20 tokens 
- Security - Powered by smart contract on Ethereum, which are immutable and decentralized 