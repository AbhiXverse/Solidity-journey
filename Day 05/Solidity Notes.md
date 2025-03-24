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

    // only the deployer of this contract becomes the minter 
    address public minter;  
    
    // this keeps track of how many coins each address has
    mapping(address => uint) public balances;

    // event logs every successful coin transfer 
    event Sent(address from, address to, uint amount);

    constructor() {
        minter = msg.sender;  // set contract deployer as minter
    }

    // this fun. creates new coins and gives them to the receiver
    function mint(address receiver, uint amount) public {
        require(msg.sender == minter); // Only minter can mint coins 
        balances[receiver] += amount; // add new coins to the receiver's balance 
    }

    // custom error to show detailed info when balance is low 
    error InsufficientBalance(uint requested, uint available);


    // tjhis function lets anyone send their coins to someone else 
    function send(address receiver, uint amount) public {
        require(amount <= balances[msg.sender], InsufficientBalance(amount, balances[msg.sender]));  // this make sure that sender has enough coins, if not then show the custom error message 
        balances[msg.sender] -= amount;  // subtract the coins from sener 
        balances[receiver] += amount;  // add the coins to receiver
        emit Sent(msg.sender, receiver, amount);  // 
    }
}
```









