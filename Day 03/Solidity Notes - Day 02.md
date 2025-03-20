[Solidity-journey /Day 02/Solidity Notes] - 02


 - Contract Interface & Number Handling: 
 
     -  Interface are like a list of rules a contract must follow 
     - They only define function names but don't include the actual code.
     - When compiled, they generate an ABI (Application Binary Interface), which helps other contract or apps interact with them.
- Example of Interface: 
     - e.g:-  [interface MyInterface  { function getValue() external view returns (uint256);  }]
     - this only defines the function getValue(), but does not include any logic inside it.
 - No decimals in solidity: Only whole numbers exist. To store decimal values, you usually multiply by 10^18 (Eth's smallest unit Wei)

Sending Transaction & funds :- 

- How transaction works: 
     - Every transaction in Ethereum is just an HTTP post request sent to a node (RPC provider)
         - RPC Provider:- RPC stands for **Remote Procedure Call** in Etheruem is like a gateway that allows your computer or application to interact with the Ethereum blockchain.
 - Only "payable" addresses can receiver funds.
 - Convert an address to payable :- 
    -  e.g:  [ payable(msg.sender); ]

- Three ways to send funds : 
     - transfer 
     - send 
     - call 
 - Difference between transfer, send & call is :- 
     - transfer: 
        - has a gas limit of 2300 t oprevent reentrancy attacks 
        - auto-reverts if the transaction fails 
    - send:
        - also has gas limit 2300
        - returns false instead of reverting, so you must manually check if it worked 
    - call: 
        - more flexible, can send Eth and even call any function without neding the contract's ABI 
