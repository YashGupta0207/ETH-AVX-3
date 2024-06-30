# ERC-20 Token (StephToken)

This is a basic ERC-20 token smart contract written in Solidity.Creating an ERC20 token involves writing a smart contract in Solidity, the programming language for Ethereum.

## Table of Contents
- [Getting Started](#getting-started)
- [Token Details](#token-details)
- [Token Functions](#token-functions)
- [Deployment and Interactions](#deployment-and-interactions)
- [License](#license)

## Getting Started

To get started with the ERC-20 token smart contract, you can follow these steps:

1. Use an online Solidity IDE like Remix.
2. Copy the entire contents of the `ERC20Token.sol` file into your Remix.
3. Compile the contract to check for any errors or warnings.
4. Deploy the contract to an Ethereum network of your choice (mainnet or testnet).

## Token Details

The ERC-20 token has the following details:

- **Name**: StephToken
- **Symbol**: STH
- **Decimals**: 18
- **Total Supply**: Initial supply can be set during deployment or through subsequent minting.

## Token Functions

The ERC-20 token smart contract provides the following functions:

1. **MintTokens(address to, uint256 amount)**
   - This function allows the contract owner to mint new tokens and assign them to a specified address. Only the contract owner can call this function.

2. **BurnTokens(uint256 amount)**
   - This function allows any token holder to burn (destroy) their own tokens. The tokens are removed from circulation, and the total supply decreases accordingly.

3. **transferfrom(address to, uint256 amount)**
   - This function allows users to transfer tokens to another address. The caller must have a sufficient balance to perform the transfer.
   -  The use of _transfer and msg.Sender leverages the inherited functionality from the ERC20 contract to handle the actual token transfer and ensure proper tracking and updating of balances.
   -  explicitly defined in our contract.

## Solidity Code

```solidity
    pragma solidity ^0.8.0;
    // SPDX-License-Identifier: MIT

   import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

   contract StephToken is ERC20 {
    address admin;

    constructor() ERC20("Steph", "STH") {
        admin = msg.sender;
        _mint(address(this), 10 * 10 ** decimals());
    }

    modifier onlyAdmin() {
        require(msg.sender == admin, "Invalid User");
        _;
    }

    function MintTokens(address recipient, uint256 quantity) public onlyAdmin {
        uint balance = balanceOf(address(this));
        require(balance >= quantity, "In-sufficient balance");
        _transfer(address(this), recipient, quantity);
    }

    function BurnTokens(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
        _transfer(sender, recipient, amount);
        uint256 currentAllowance = allowance(sender, _msgSender());
        require(currentAllowance >= amount, "ERC20: transfer amount exceeds allowance");
        _approve(sender, _msgSender(), currentAllowance - amount);
        return true;
   }
   }
```  
## Deployment and Interactions

To deploy and interact with the ERC-20 token smart contract, you can follow these steps:

1. **Deploy the Contract**
   - Deploy the contract to an Ethereum network using your preferred deployment tool Remix.

2. **Receive the Contract Address**
   - After deployment, you will receive the contract address. This address represents your token contract on the blockchain.

3. **Interact with the Contract**
   - You can interact with the contract using the provided functions. For example:
     - Call the `MintTokens` function to create and assign new tokens to a specified address.
     - Call the `BurnTokens` function to burn a certain amount of your own tokens.
     - Call the `transferfrom` function to send tokens to another address.
   - Make sure you have sufficient gas and appropriate permissions (e.g., contract ownership) to execute certain functions.
     
## Authors

YASH GUPTA  
[@YASH GUPTA]

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
