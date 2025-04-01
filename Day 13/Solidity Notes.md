
[Solidity-journey /Day 13/Solidity Notes] - #12


ABI (Application binary interface) Encoding/decoding 

- What is ABI ? 
    -  this is a standard where you can interact between smart contracts and external actors (e.g - other contracts, applications)

- Encoding/ Decoding: 
    - Encoding - Converts data (like number, adresses etc) into a format suitable for EVM 
    - Decoding - converts raw transaction data back  into human readable format 

- Tools: 
    - web3.js, ether.js and solidity libraries help interact with ABI 


Data Location 

- Storage:
    - Persistent state - variables stored here cost gas to modify 
    - data is kept on-chain 
    - e.g - state variables inside contracts 
     e.g 
```
contract StorageEg {
    uint256 public storedNumber;        // stored in storage (persistent)
      
      function setNumber(uint256 _num) public {
          storedNUmber = _num;       // writing in storage (costs gas)
    }
}
```

- Memory:
     - Temporary data - used for computation 
     - faster than storage, but volatile (lost after function call)
     - e.g - variables declared inside functions
     e.g 
```
contract MemoryEg {
     function getMemory() public pure returns (string memory) {
         string memory tempstring = "Hello Abhi";   // Stored in memory   
         return tempstring;                         // Existed only diring function execution 
    }
}
```

 - Stack:
     - Temporary as well but high speed storage 
     - stores simple values and function return values 
      e.g:
```
contract StackEg {
    function addNumber() public pure returns (uint) {
        uint256 a = 10;      // stored in stack 
        uint256 b = 20;      // stored in stack 
        uint sum = a + b;    // stored in stack 
        return sum;          // the result is also stroed in stacl but temporarily 
    }
}
```


Literals: 

- Literals types refers to fixed values in solidity (like numbers )