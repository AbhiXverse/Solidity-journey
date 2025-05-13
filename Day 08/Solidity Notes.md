
[Solidity-journey /Day 08/Solidity - 101 Notes] - #07


**Constant & Immutable Variables :-** 

- Constant:- Cannot be changed, written in All Caps
- Immutable :- Can be set once (e.g, in the constructor)
- E.g: 
```
  contract Example {
     uint256 public constant FEE - 1000;  // Never changes
     address public immutable i_owner;
     
  constructor() {
      i_owner = msg.sender;   // set only once 
      
  }  
}
```
why use them ?
- Stored in bytecode, not storage slots, so they save gas.


**Receiving Eth without a function call :-** 

- If someone sends Eth without calling a function, Solidity uses: 
    - receive() function - when Eth is sent without any data
    - fallback() function - when data is sent, but no matching function exists
    - E.g - 
```
   contract ReceiveExample {
      event Received(address sender, uint256 amount);
      
      receive() external payable {
          emit Receivced(msg.sender, msg.value);
      }
    }
```
this contract logs the sender and amount when it receives Eth.