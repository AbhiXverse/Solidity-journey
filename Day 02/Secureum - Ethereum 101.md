[Secureum - Ethereum 101 - Day 02] - 02


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
    - In Turing-complete system, it's impossible to determine in advance whether a given program will eventually stop or run forever. This is known as the Halting problem.
- How does this affect Ethereum ?
    - Since Ethereum runs smart contracts, it cannot predict if a contract will stop or how long it will run. To prevent contracts from running indefinitely and consuming unlimited resources, Ethereum uses a gas system.
- Why gas ? 
    - Gas is like a fuel - every action in a contract uses gas.
    - If a contract runs out of gas, it stops. 
    - This prevents contracts from running forever and keeps Ethereum safe and efficient.

- DApps (Decentralized Applications) shifts from Web 2.0, where apps are controlled by a central authority, to Web 3.0, where apps runs on decentralized peer-to-peer networks for computing, storage and messaging.