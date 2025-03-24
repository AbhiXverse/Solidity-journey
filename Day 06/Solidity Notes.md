[Solidity-journey /Day 06/Solidity Notes] - 06

Understanding different integers sizes in Solidity 

- Solidity has different type of unsigned integers like uint8, uint16, uint32, uint64 up to uint256 

1. uint8 (0 to 255) 
    - Best for very small numbers like simple counters 
    - use when you're sure the value won't go above 255 and want to save storage 
    - e.g: Day , hour etc 
    
2. uint16 (0 to 65,535)
    - best for medium size numbers 
    - use when you're sure that values are within this range and want to save space 
    - e.g: Year, percentage values, item counts etc 

3. uint32 (0 to ~18.4 quintillion)
    -  best for medium counters 
    -  use when you're sure that values are within this range and want to save space 
    - e.g: game score, short duration timers etc 

4. uint64 (0 to ~3.4x10^38)
     - best for time based values or huge numbers 
     - use when you deal with time or very large numbers 
     - e.g : unix timestamps, very large numbers etc 

5. uint256 ( 0 to ~1.16 x 10^77)
    - best for most use cases related to financial values 
    - use for almost all financial values
    - e.g: token balances, Ether values, hash results etc 


Note : 
- Beginner tips: 

    - Start with uint256 - its the safest and most common 
    - default to uint256 for most cases like - Token amounts, ETH/Wei values, any financial calculations, IDs or unique identifiers 
    - Only use smaller sizes when you're absolutely sure about the max value 
    - Since - Solidity 0.8.0, overflow checks are automatic for all sizes but yeah choosing the right size based on the situation helps to reduce gas costs 
