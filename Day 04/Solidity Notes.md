[Solidity-journey /Day 04/Solidity Notes] - #04


- **Payment & Transactions** 
    - Payable functions: Allow contract to receive Eth.
    - Checking payment value: Use **msg.value**, which represent the amount in Wei 
    - Require statement: Ensures conditions are met,
        - e.g:-  [require(msg.value > 1e18);   // Requires at least 1 Eth]
    - Nonce: Counts the number of transaction for an account

- **Oracles & External data:**

    - Oracles & chainlink: Help smart contract access real-world data
    - Smart contract can't directly - 
         - Connect to API 
         - Make external calls
         - Access off-chain data 
    - Oracles Problem: Smart contract must work in a predictable way, so they can't directly use things like random numbers or data from external APIs.
    
 - Contract Interface & Number Handling: 
 
     -  Interface are like a list of rules a contract must follow 
     - They only define function names but don't include the actual code.
     - When compiled, they generate an ABI (Application Binary Interface), which helps other contract or apps interact with them.
- Example of Interface: 
```
interface MyInterface  {
function getValue() external view returns (uint256);
}
```
 - this only defines the function getValue(), but does not include any logic inside it.

 - No decimals in solidity: Only whole numbers exist. To store decimal values, you usually multiply by 10^18 (Eth's smallest unit Wei)