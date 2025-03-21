[Solidity-journey /Day 01/Solidity Notes] - 01 

Basics:

- Solidity is a high-level language for implementing smart contracts on Ethereum (and other EVM compatible blockchains)
- Proposed in 2014 by Gavin Wood, developed by Ethereum's team led by Christian reitwiessner etc 

Language Influences:

- Mainly from C++
- Python (modifiers, multiple inheritance)
- JavaScript (function-level scoping, var keyword)

Features: 

- Statically typed 
- Supports inheritance, libraries. user-defined types
- Fully-featured, object-oriented

Source file Layourt:

- Can contain - 
    - pragma directives 
    - import directives 
    - definations of struct, enum, contract 
- Best contract layout order - 
    - state variables 
    - Events 
    - modifiers 
    - constructor 
    - functions 

SPDX License: 
- SPDX = Software Package Data Exchange 
- Included in bytecode metadata for machine readability 

Pragmas: 

- Syntax - pragma solidity x.y.z;
- Example - pragma solidity ^0.8.3; 
     - allows version form 0.8.3 to <0.9.0 (called floating pragmas )
 - you can use combination like >=0.8.0 <0.8.3

NatSpec tags
