
**Transfer vs Send:** 

- transfer() -
    - sends Ether, reverts the failure 
    - fixed 2300 gas 
    - safe and simple to use 
- send() - 
     - returns false on failure (doesn't revert) 
     - must manually check the return value 


**Call / Delegatecall / Staticcall:**

- call():
    - low-level call , forwards all gas 
    - use with encoded data 
    - can send Ether 
- delegatecall() - 
    - uses target contract's code but current contract's state 
    - used for libraries 
- staticcall() - 
     - Same as call() but doesn't allow state changes 