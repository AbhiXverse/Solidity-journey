Cryptography in Ethereum:- 

- Two types of cryptography: 
    - Symmetric cryptography: Uses the same key for encryption and decryption 
    - Asymmetric cryptography(Public-key cryptography): Uses two keys, a public key and a private key
- Ethereum uses asymmetric cryptography for digital signatures 
  (not for encryption)
- Digital Signature Algorithm used: ECDSA (Elliptic Curve Digital Signature Algorithm)
- Elliptic Curve Cryptography (ECC): A method of public-key cryptography using mathematical properties of elliptic curves
- Curve used: SECP-256K1 (same as Bitcoin)
- Keys:
    - Private key: A 256-bit random number, secret, used to generate the public key
    - Public key: Generated from the private key and used to derive the Ethereum address 
- Ethereum addresses: Derived from the last 20 bytes of the Keccak-256 hash of the public key

Ethereum Accounts:-

- Ethereum accounts store and manage funds and transaction 

