[Solidity-journey /Day 05/Solidity Notes] - 05


Custom Errors: 

- Custom errors are a way to define specific messages in solidity 
- They help you give clear feedback when something goes wrong in your contract 
- Main benefit: They use less gas compared to writing error messages as string like "Insufficient Balance"

How to write it :- 
E.g:
```
error ErrorName(type param1, type param2);
```


Contract Example : 
- Custom error in a Coin contract:
```
contract Coin {

    address public minter;                        // only the deployer of this contract becomes the minter 


   mapping(address => uint) public balances;       // this keeps track of how many coins each address has

    
    event Sent(address from, address to, uint amount);    // event logs every successful coin transfer 

    constructor() {
        minter = msg.sender;                      // set contract deployer as minter
    }

    
    function mint(address receiver, uint amount) public {       // this fun. creates new coins and gives them to the receiver
        require(msg.sender == minter);                          // Only minter can mint coins 
        balances[receiver] += amount;                           // add new coins to the receiver's balance 
    }

    
    error InsufficientBalance(uint requested, uint available);   // custom error to show detailed info when balance is low 


    
    function send(address receiver, uint amount) public {              // this function lets anyone send their coins to someone else 
        if (amount > balances[msg.sender] 
          revert InsufficientBalance(amount, balances[msg.sender]));   // this make sure that sender has enough coins, if not then show the custom error message 
        balances[msg.sender] -= amount;                                // subtract the coins from sener 
        balances[receiver] += amount;                                  // add the coins to receiver
        emit Sent(msg.sender, receiver, amount);                       // trigger the sent event to show that a transfer happened
    }
}
```

 Custom error :-
```
error InsufficientBalance(uint requested, uint available);
```
- this error is used when someone tries to send more coins than they have 
- it takes two values: 
    - requested: how much the user wants to send 
    - available: how much they actually have 


How it is used in code: 
```
require (amount <= balance[msg.sender], InsufficientBalance(amount, balance[msg.sender]) );
```
- this line checks if the user has enough balance 
- if not, revert the transaction and show the custom error message with real values 
- this version is cheaper in gas 
- and it provides more info then just showing "insufficient balance"






