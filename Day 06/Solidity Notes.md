[Solidity-journey /Day 06/Solidity - 101 Notes] - #06


**Contract Ownership & Security :-** 

- Assign a contract owner : 
    - Use a **constructor**, which runs only when the contract is deployed 
    - E.g : 
```
    contract Ownable {
    address public owner ;
 
    constructor () {
        owner = msg.sender; // Assigns contract deployer as the                                           owner 
        }
     }
```

**Modifiers (Adding extra logic to functions):-**

- Modifiers let you add reusable checks to functions 
- E.g : 
```
  modifier onlyowner( ) {
      require(msg.sender == owner, "Not the owner");
      _;
     }

	  function withdraw() public onlyowner {
	     payable(owner). transfer(address(this).balance); 
	     }
   }
```
here, only the contract owner can withdraw the Eth.