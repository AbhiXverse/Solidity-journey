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
     - with time or very large numbers etc 
     - dfgd
     - 
