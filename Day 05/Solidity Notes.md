[Solidity-journey /Day 05/Solidity - 101 Notes] - #05


**Sending Transaction & funds :-** 

- How transaction works: 
     - Every transaction in Ethereum is just an HTTP post request sent to a node (RPC provider)
         - RPC Provider:- RPC stands for **Remote Procedure Call** in Etheruem is like a gateway that allows your computer or application to interact with the Ethereum blockchain.
 - Only "payable" addresses can receiver funds.
 - Convert an address to payable :- e.g:
```
payable(msg.sender);
```

- Three ways to send funds : 
     - transfer 
     - send 
     - call 
 - Difference between transfer, send & call is :-
     - transfer: 
        - has a gas limit of 2300 to prevent reentrancy attacks 
        - auto-reverts if the transaction fails 
    - send:
        - also has gas limit 2300
        - returns false instead of reverting, so you must manually check if it worked 
    - call: 
        - more flexible, can send Eth and even call any function without needing the contract's ABI.
        - e.g:-
```
(bool success, bytes memory data) = payable(msg.sender).call{value: address(this). balance}(""); 
require(success, "Transfer failed");
```
