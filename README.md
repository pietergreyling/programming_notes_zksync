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
```

An ERC20 token contract keeps track of fungible tokens: 
- any one token is exactly equal to any other token; 
- no tokens have special rights or behavior associated with them. 
- This makes ERC20 tokens useful for things like 
  - a medium of exchange currency, 
  - voting rights, 
  - staking, 
  - and more.

OpenZeppelin Contracts provides many ERC20-related contracts.
```

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

### ERC20 Token Implementation Specification

- https://ethereum.org/en/developers/docs/standards/tokens/erc-20/

#### Methods
```solidity
function name() public view returns (string)
function symbol() public view returns (string)
function decimals() public view returns (uint8)
function totalSupply() public view returns (uint256)
function balanceOf(address _owner) public view returns (uint256 balance)
function transfer(address _to, uint256 _value) public returns (bool success)
function transferFrom(address _from, address _to, uint256 _value) public returns (bool success)
function approve(address _spender, uint256 _value) public returns (bool success)
function allowance(address _owner, address _spender) public view returns (uint256 remaining)

```

#### Events
```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```


- https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol
- https://docs.openzeppelin.com/contracts/3.x/api/token/erc20
- https://wizard.openzeppelin.com/#erc20

A simple ERC20 smart contract that mints 100 tokens called "MyToken"

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 100 * 10 ** decimals());
    }
}
```

Another sample from https://docs.openzeppelin.com/contracts/3.x/erc20
```solidity
// contracts/GLDToken.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract GLDToken is ERC20 {
    constructor(uint256 initialSupply) public ERC20("Gold", "GLD") {
        _mint(msg.sender, initialSupply);
    }
}
```

The previous ERC20 sample token contracts implement the IERC20 interface

```solidity
// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts (last updated v4.6.0) (token/ERC20/IERC20.sol)

pragma solidity ^0.8.0;

/**
 * @dev Interface of the ERC20 standard as defined in the EIP.
 */
interface IERC20 {
    /**
     * @dev Emitted when `value` tokens are moved from one account (`from`) to
     * another (`to`).
     *
     * Note that `value` may be zero.
     */
    event Transfer(address indexed from, address indexed to, uint256 value);

    /**
     * @dev Emitted when the allowance of a `spender` for an `owner` is set by
     * a call to {approve}. `value` is the new allowance.
     */
    event Approval(address indexed owner, address indexed spender, uint256 value);

    /**
     * @dev Returns the amount of tokens in existence.
     */
    function totalSupply() external view returns (uint256);

    /**
     * @dev Returns the amount of tokens owned by `account`.
     */
    function balanceOf(address account) external view returns (uint256);

    /**
     * @dev Moves `amount` tokens from the caller's account to `to`.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transfer(address to, uint256 amount) external returns (bool);

    /**
     * @dev Returns the remaining number of tokens that `spender` will be
     * allowed to spend on behalf of `owner` through {transferFrom}. This is
     * zero by default.
     *
     * This value changes when {approve} or {transferFrom} are called.
     */
    function allowance(address owner, address spender) external view returns (uint256);

    /**
     * @dev Sets `amount` as the allowance of `spender` over the caller's tokens.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * IMPORTANT: Beware that changing an allowance with this method brings the risk
     * that someone may use both the old and the new allowance by unfortunate
     * transaction ordering. One possible solution to mitigate this race
     * condition is to first reduce the spender's allowance to 0 and set the
     * desired value afterwards:
     * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729
     *
     * Emits an {Approval} event.
     */
    function approve(address spender, uint256 amount) external returns (bool);

    /**
     * @dev Moves `amount` tokens from `from` to `to` using the
     * allowance mechanism. `amount` is then deducted from the caller's
     * allowance.
     *
     * Returns a boolean value indicating whether the operation succeeded.
     *
     * Emits a {Transfer} event.
     */
    function transferFrom(address from, address to, uint256 amount) external returns (bool);
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
