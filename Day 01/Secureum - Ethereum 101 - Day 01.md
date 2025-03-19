
Ethereum is "A Next-Generation Smart Contract and Decentralized Application"

Purpose:

- Ethereum is more than just a currency or payment network.
- It has a native currency called Ether (Eth).
- Ether is needed to run ay part of ethereum platform.
- It acts as a utility token for using the ethereum platform.

Programming language:

- Bitcoin uses a simple scripting language called Script.
- This language is limited and only checks if a transaction is true or false.
- In Ethereum, it supports EVM (Ethereum Virtual Machine).
- EVM is designed to be a general-purpose computing platform. 
- It is Turing complete, meaning it can handle any logic or computation. 

What Ethereum can do?

- Can store any type of data, from simple numbers and text to complex structure like lists and mappings. 
- Can execute any kind of logic, form the basic math to advanced algorithms.
- More flexible than Bitcoin's script because it is not limited in complexity.

How they track transactions ?

1. Bitcoin tracks transactions using a system called UTXO( Unspent Transaction Outputs)
    -  It only records the ownership of bitcoin and how it moves between users.

2. Ethereum uses an account-based system instead of UTXO. 
    - It tracks not only the Ether ownership but also the state of smart contract.
    - Transaction can change the state of contracts and interact with decentralized applications (Dapps).

Core Components:

- P2P Network - Runs on Ethereum mainnet, uses TCP port 30303, and follows the DEVp2p protocol.
- Unlike traditional client-server models, Ethereum nodes interact as peers, exchanging messages.

- Transactions: 
    - Messages containing sender, recipient, value and data payload.
    - Transactions modify the state and trigger smart contract execution.

- State machine (EVM):
    - Uses the Ethereum Virtual Machine (EVM) to process state changes.
    - Executes smart contract written in Solidity or Vyper.

- Data Structures:
    - Stores state in a database (LevelDB)
    - Uses Merkle Patricia Tree for efficient transaction and state storage

- Consensus Algorithms:
    - Bitcoin uses Nakamoto Consensus PoW (proof-of -work), securing the chain by making it costly to attack.
    - Ethereum originally used PoW (Ethash) but transitioned to PoS (proof-of-state) in Ethereum 2.0 (Serenity) for better scalability and efficiency.

- Economic Security:
    - PoW ensured security by making the 51% attack expensive.
    - PoS enchances security by requiring validatiors to stake ETH, discouraging malicious behavior.

- Software Implementations:
    - Go-Ethereum (Geth) - Most widely used.
    - OpenEthereum - Deprecated, transitioning to Erigon (formerly Turbo-geth).
    - Other clients: Nethermind, Erigon, Turbo-geth.

- Halting Problem in Etheruem:

     - Ethereum's Ethereum Virtual Machine (EVM) can read and write data to memory, making it a Turing-complete system.
- What is the halting problem:
    - In Turing-complete system, it's impossible to determine in advance whether a given program will eventually stop or run forever.This is known as the Halting problem.
- How does this affect Ethereum ?
    - Since Ethereum runs smart contracts, it cannot predict if a contract will stop or how long it will run. To prevent contracts from running indefinitely and consuming unlimited resources, Ethereum uses a gas system.
- Why gas ? 
    - Gas is like a fuel - every action in a contract uses gas.
    - If a contract runs out of gas, it stops. 
    - This prevents contracts from running forever and keeps Ethereum safe and efficient.

- DApps (Decentralized Applications) shifts from Web 2.0, where apps are controlled by a central authority, to Web 3.0, where apps runs on decentralized peer-to-peer networks for computing, storage and messaging.

How Ethereum Powers Web3:

- Computing Power -> Ethereum Blockchain 
- File Storage -> Swarm 
- Messaging -> Waku (previously whisper)

Types of Decentralization:
- Architectural decentralization 
- Political decentralization 
- Logical decentralization

Different Units of Ether: 
-  Wei           =>  1 Wei 
-  Babbage  =>  10 ** 3 Wei 
-  Lovelace  =>  10 ** 6 Wei 
-  Shannon  =>  10 ** 9 Wei 
-  Szabo      =>  10 ** 12 Wei 
-  Finney     =>  10 ** 15 Wei 
-  Ether       =>  10 ** 18 Wei 

- Gwei (Shannon): Used for gas fees in Etheruem transactions
- Wei: The smallest and most fundamental unit.








