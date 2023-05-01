# zkSync Era Programming Notes

## Introduction

This repository captures some notes on how to write code for the zkSync Era blockchain platform from Matter Labs.

The content represents a simple on-boarding guide based upon my initial experiences when building basic Ethereum smart contracts and front-ends integrated with the zkSync Era blockchain platform and tools.

## The Challenge

The challenge is to learn by implementing the following application components:

- A custom ERC-20 token with a compliant smart contract
  - This contract should mint an initial amount of tokens 
- A smart contract that allows participants to guess a secret number under the control of the contract owner

## The Development Approach

I chose to use the following process in building the application.

### Study the ERC-20 specification and a how to mint the token with a Solidity contract implementation
- https://ethereum.org/en/developers/docs/standards/tokens/erc-20/

```
What is a Token?

Tokens can represent virtually anything in Ethereum:

- reputation points in an online platform
- skills of a character in a game
- lottery tickets
- financial assets like a share in a company
- a fiat currency like USD
- an ounce of gold
- and more...

Such a powerful feature of Ethereum must be handled by a robust standard, right? 

That's exactly where the ERC-20 plays its role! 
This standard allows developers to build token applications that are interoperable with other products and services.

What is ERC-20?

The ERC-20 introduces a standard for Fungible Tokens, in other words, 
- they have a property that makes each Token be exactly the same (in type and value) as another Token. 
- For example, an ERC-20 Token acts just like the ETH, 
- meaning that 1 Token is and will always be equal to all the other Tokens.
```

- https://docs.openzeppelin.com/contracts/3.x/erc20
- https://eips.ethereum.org/EIPS/eip-20
```
Simple Summary
- A standard interface for tokens.

Abstract
The following standard allows for 
- the implementation of a standard API for tokens within smart contracts. 
- This standard provides basic functionality to transfer tokens, 
- as well as allow tokens to be approved so they can be spent by another on-chain third party.

Motivation
- A standard interface allows any tokens on Ethereum to be re-used by other applications: 
  - from wallets to decentralized exchanges.
```

- https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol
- https://wizard.openzeppelin.com/#erc20

A simple ERC-20 smart contract that mints 100 tokens called "MyToken"

```typescript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 100 * 10 ** decimals());
    }
}
```

## Programming Tools
- https://wizard.openzeppelin.com/#erc20
- https://era.zksync.io/docs/api/tools/zksync-cli/
- https://hardhat.org/
- https://hardhat.org/hardhat-runner/docs/getting-started#overview


## Matter Labs (zkSync Era) References

### Matter Labs (zkSync Era) Documentation
- https://matter-labs.io/
- https://matterlabs.notion.site/Shape-the-future-of-Ethereum-at-Matter-Labs-dfb3b5a037044bb3a8006af2eb0575e0
- https://era.zksync.io/docs/
- https://era.zksync.io/docs/dev/

### Matter Labs (zkSync Era) Toolchain

- zkSync-CLI to scaffold a project: 
  - https://era.zksync.io/docs/api/tools/zksync-cli/
- A quickstart tutorial that includes a frontend integration: 
  - https://era.zksync.io/docs/dev/building-on-zksync/hello-world.html
- Deployment instructions: 
  - https://era.zksync.io/docs/api/hardhat/hardhat-zksync-deploy.html
- zkSync-Web3 frontends to interact with contracts: 
  - https://era.zksync.io/docs/api/js/getting-started.html
