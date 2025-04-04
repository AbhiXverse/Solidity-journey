
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