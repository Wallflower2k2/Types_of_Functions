# Create and Mint token

This repository has a smart contract that is created to generate a token on the local hardhat network. Remix IDE or any other Ethereum IDE can be used to communicate with the smart contract.
This README file explains in detail the fundamental aspects of the project as well as the methods required for contract deployment on a local hardhat network utilizing remix connect localhost.

# Features
The project provides the following features:
. **function.sol** contains the source code of the token.
. Token attributes like **name**, **symbol**,**decimal**,**initialsupply**.
. **mint** function is used to mint tokens to a address, restricted to be used only by owner.
.**burn** function is used to burn tokens from address , no restriction on access.
.**transfer** is used to transfer tokens fron sender to receiver , no restriction on access.
Only the owner can use **mint** function whereas all the functions can be used by other users/address.

##Deploymnet on Local Hardhat Network


Follow these steps to deploy tokens on local hardhat network , here i am using VS Code.

1. Install node.js in to your systemt to run npm commands.
  
2. You can check whether node.js is installed into your sytem by running the following command in your Command Prompt:
```
 node -v
```
If the CMD shows the version of the node.js implies that it is intalled into your system.

4. Open VS Code and and write the following codes using .sol extension:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract HardHat {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 private _totalSupply;
    mapping(address => uint256) private _balances;
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Burn(address indexed account, uint256 amount);
    event Mint(address indexed account, uint256 amount);

    constructor(string memory tokenName, string memory tokenSymbol, uint8 tokenDecimals, uint256 initialSupply) {
        name = tokenName;
        symbol = tokenSymbol;
        decimals = tokenDecimals;
        _totalSupply = initialSupply * (10 ** uint256(tokenDecimals));
        _balances[msg.sender] = _totalSupply;
        emit Transfer(address(0), msg.sender, _totalSupply);
    }

    function totalSupply() external view returns (uint256) {
        return _totalSupply;
    }

    function balanceOf(address account) external view returns (uint256) {
        return _balances[account];
    }

    function transfer(address recipient, uint256 amount) external returns (bool) {
        _transfer(msg.sender, recipient, amount);
        return true;
    }

    function burn(uint256 amount) external returns (bool) {
        require(amount <= _balances[msg.sender], "Insufficient balance");
        _balances[msg.sender] -= amount;
        _totalSupply -= amount;
        emit Burn(msg.sender, amount);
        emit Transfer(msg.sender, address(0), amount);
        return true;
    }

    function mint(address account, uint256 amount) external returns (bool) {
        require(account != address(0), "Invalid account address");
        _totalSupply += amount;
        _balances[account] += amount;
        emit Mint(account, amount);
        emit Transfer(address(0), account, amount);
        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) internal {
        require(sender != address(0), "Invalid sender address");
        require(recipient != address(0), "Invalid recipient address");
        require(amount <= _balances[sender], "Insufficient balance");

        _balances[sender] -= amount;
        _balances[recipient] += amount;
        emit Transfer(sender, recipient, amount);
    }
}
```
4. Open a terminal in VS code and write the following commands:
```
For package.json - npm init
To install hardhat - npm install --save-dev hardhat
To run hardhat - npx hardhat
To install chai and others - npm install --save-dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai
```
5. In a new terminal wrtite the following command:
```
npx hardhat node
```
To test Hardhat's Network;

5. Open the **Remix** IDE in your browser.
6. Go to File Explorer -> Workspaces -> Connect to locahost and click confirm.
7. Rewrite the function.sol file in the contracts directory with your own token code.
8. Compile the contract in the Remix IDE.
9. In the deploy section of Remix, select the environment as "Dev-Hardhat Provider".
10. Before deploying your contract provide the **Tokenname**, **TokenSymbol**,**TokenDecimals**,**InitialSupply**.
11. Confirm the deployment transaction in Remix.
12. Once the contract is deployed, you will see the contract address in the Remix console. Make note of this address for future interactions.

13. # Interacting with the Contract using Remix with Hardhat Provider
 -After the contract is deployed, Remix will display the deployed contract instance in the "Deployed Contracts" section.

-Expand the deployed contract instance to see the available functions and their input fields.

-You can now interact with the contract by calling its functions and providing the required inputs.

-To mint tokens, call the mint function and provide the receiver's address and the desired amount. -To burn tokens, call the burn function and provide the amount to be burned. -To transfer tokens, call the transfer function and provide the receiver's address and the amount to be transferred.

After providing the inputs, click on the "Transact" button to execute the function.

#Authors
Gauri Kaushal (gaurikaushal18@gmail.com)

#License
This project is licensed under the MIT License


