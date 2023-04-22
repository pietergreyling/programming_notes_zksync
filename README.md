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
- https://docs.openzeppelin.com/contracts/3.x/erc20
- https://eips.ethereum.org/EIPS/eip-20
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


## References

- https://matter-labs.io/
- https://matterlabs.notion.site/Shape-the-future-of-Ethereum-at-Matter-Labs-dfb3b5a037044bb3a8006af2eb0575e0
- https://era.zksync.io/docs/
- https://era.zksync.io/docs/dev/
