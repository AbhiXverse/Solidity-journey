
Ethereum is "A Next-Generation Smart Contract and Decentralized Application"

Purpose 

- Ethereum is more than just a currency or payment network 
- It has a native currency called Ether (Eth)
- Ether is needed to run ay part of ethereum platform 
- It acts as a utility token for using the ethereum platform 

Programming language 

- Bitcoin uses a simple scripting language called Script
- This language is limited and only checks if a transaction is true or false 
- In Ethereum, it supports EVM (Ethereum Virtual Machine)
- EVM is designed to be a general-purpose computing platform 
- it is Turing complete, meaning it can handle any logic or computation 

What Ethereum can do?

- Can store any type of data, from simple numbers and text to complex structure like lists and mappings 
- Can execute any kind of logic, form the basic math to advanced algorithms 
- More flexible than Bitcoin's script because it is not limited in complexity 

How they track transactions ?

1. Bitcoin tracks transactions using a system called UTXO( Unspent Transaction Outputs)
    -  It only records the ownership of bitcoin and how it moves between users

2. Ethereum uses an account-based system instead of UTXO 
    - It tracks not only the Ether ownership but also the state of smart contract 
    - Transaction can change the state of contracts and interact with decentralized applications (Dapps)

Core Components 

- P2P Network - Runs on Ethereum mainnet, uses TCP port 30303, and follows the DEVp2p protocol.
- Transactions: Messages containing sender, recipient, value and data payload.
- State machine:
    -  Uses the Ethereum Virtual Machine (EVM) to process state changes.
    -  Executes smart contract written in Solidity or Vyper.
- Data Structures:
    -   Stores state in a database (LevelDB)
    -  Uses Merkle Patricia Tree for efficient transaction and state storage
- Economic Security:
    -  Previously used Ethash (PoW)
    -  Now secured by staking in PoS 
- Software Implementations 
    -  Go-Ethereum (Geth) - Most widely used 
    -  OpenEthereum - Deprecated, transitioning to Erigon (formerly Turbo-geth)
    - Other clients: Nethermind, Erigon, Turbo-geth
- 








