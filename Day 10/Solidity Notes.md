
[Solidity-journey /Day 10/Solidity - 101 Notes] - #09


**Custom Errors:** 

- Custom errors are a way to define specific messages in solidity 
- They help you give clear feedback when something goes wrong in your contract 
- Main benefit: They use less gas compared to writing error messages as string like "Insufficient Balance"

**How to write it :-** 
E.g:
```
error ErrorName(type param1, type param2);
```


**Contract Example :** 
- Custom error in a Coin contract:
```
contract Coin {

    address public minter;                        // only the deployer of this contract becomes the minter 


   mapping(address => uint256) public balances;       // this keeps track of how many coins each address has

    
    event Sent(address from, address to, uint amount);    // event logs every successful coin transfer 

    constructor() {
        minter = msg.sender;                      // set contract deployer as minter
    }

    
    function mint(address receiver, uint amount) public {       // this fun. creates new coins and gives them to the receiver
        require(msg.sender == minter);                          // Only minter can mint coins 
        balances[receiver] += amount;                           // add new coins to the receiver's balance 
    }

    
    error InsufficientBalance(uint256 requested, uint256 available);   // custom error to show detailed info when balance is low 


    
    function send(address receiver, uint256 amount) public {              // this function lets anyone send their coins to someone else 
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
error InsufficientBalance(uint256 requested, uint256 available);
```
- this error is used when someone tries to send more coins than they have 
- it takes two values: 
    - requested: how much the user wants to send 
    - available: how much they actually have 


**How it is used in code:** 
```
if (amount > balance[msg.sender] 
revert InsufficientBalance(amount, balance[msg.sender]));
```
- this line checks if the user has enough balance 
- if not, revert the transaction and show the custom error message with real values 
- this version is cheaper in gas 
- and it provides more info then just showing "insufficient balance"


**Note 1:-** 
- When using **custom errors** in solidity, you cannot pass that custom error directly to a require statement

- traditional require statement: you only pass the simple string message
e.g:
```
require(amount <= balance, "Insufficient balance");
```

- But with the custom errors: 
    - you need to use an **if** condition and then explicitly **revert** with your custom error:
      e.g: 
```
    if (amount > balance[msg.sender]) 
     revert InsufficientBalance (amount , balance[msg.sender]);
```



**Note 2 :-** 
- With Curly brackets in If condition:
  e.g : 
```
if (amount > balance) {
revert InsufficientBalance(amount, balance);
}
```
So, by using Curly bracket after the If condition, all the statements within the bracket are the part of the If condition 
and, 

- Without Curly bracket in If condition:
  e.g: 
```
if (amount > balance) 
revert InsufficientBalance (amount, balance);
```
So, in this only the next single statement is part of the If condition or only the first condition is controlled by the If condition. The second statement will always execute.