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

    // Constructor code is only run when the contract
    // is created
    constructor() {
        minter = msg.sender;
    }

    // Sends an amount of newly created coins to an address
    // Can only be called by the contract creator
    function mint(address receiver, uint amount) public {
        require(msg.sender == minter);
        balances[receiver] += amount;
    }

    // Errors allow you to provide information about
    // why an operation failed. They are returned
    // to the caller of the function.
    error InsufficientBalance(uint requested, uint available);

    // Sends an amount of existing coins
    // from any caller to an address
    function send(address receiver, uint amount) public {
        require(amount <= balances[msg.sender], InsufficientBalance(amount, balances[msg.sender]));
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        emit Sent(msg.sender, receiver, amount);
    }
}
```









