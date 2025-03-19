Cryptography in Ethereum:- 

- Two types of cryptography: 
    - Symmetric cryptography: Uses the same key for encryption and decryption 
    - Asymmetric cryptography(Public-key cryptography): Uses two keys, a public key and a private key
- Ethereum uses asymmetric cryptography for digital signatures 
  (not for encryption)
- Digital Signature Algorithm used: ECDSA (Elliptic Curve Digital Signature Algorithm)
- Elliptic Curve Cryptography (ECC): A method of public-key cryptography using mathematical properties of elliptic curves
- Curve used: SECP-256K1 (same as Bitcoin)
- Keys -
    - Private key: A 256-bit random number, secret, used to generate the public key
    - Public key: Generated from the private key and used to derive the Ethereum address 
- Ethereum addresses: Derived from the last 20 bytes of the Keccak-256 hash of the public key

Ethereum Accounts:-

- Ethereum accounts store and manage funds and transaction 
- Two types of accounts -
     1. Externally Owned Accounts (EOAs): Controlled by private keys
     2. Contract Accounts: Controlled by smart contract code
- Fields in an Ethereum accounts -
    - Nonce: Prevents duplicate transactions
    - Balance: Account of Ether held 
    - Contract code: Present only in contract accounts 
    - Storage: Stores contract data, initially empty

Transaction in Ethereum:- 

- A transaction is a signed message that changes Ethereum's state 
- Transaction are created by EOAs and broadcasted to the network 
- Components of a transaction: 
     - Nonce: Transaction count from the sender's account 
     - Gas price: Fee per gas uint (measured in Wei) 
     - Gas limit: Maximum gas allowed for the transaction
     - Recipient: Address receiving the transaction
     - Value: Amount of Ether being sent
     - Data: Extra information, mainly for smart contract 
     - v, r 
     

