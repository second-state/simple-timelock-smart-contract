# Simple Timelock Smart Contract

A simple timelock smart contract which locks ERC20 tokens for a specific time period and then allows users to unlock when that time period has elapsed.

![Untitled Diagram](https://user-images.githubusercontent.com/9831342/150889891-7fddb8a9-9af7-498d-8189-1bde57cd3aa0.jpg)

# Deploying the Simple Timelock Smart Contract

## Step 1
Connecting to blockchain and accounts:
- Open https://remix.ethereum.org/
- Connect MetaMask
- Select owner’s account
- Fund owner’s account with ETH as gas for the following transactions

## Step 2
Make sure that the “environment” in Remix is set to “Injected Web3” and that the owner's account is selected in Remix’s “account” section

Compile an ERC20 contract of your choice.

**IMPORTANT**: Please ensure that the ERC20 contract has **18 decimal places** and conforms fully to the ERC20 standard. This is a requirement which will allow this token to be traded on DEXs on Ethereum mainnet.

Deploy your ERC20 contract; making sure that Remix’s “contract” dropdown section is set to “YourERC20Contract.sol” (the drop down resets to other inherited contracts so you have to manually/deliberately choose the correct contract to deploy each time).

Once deployed, please record the ERC20 contract’s address and tx hash for future use.

## Step 3
Make sure that the “environment” in Remix is set to “Injected Web3” and that the owner's account is selected in Remix’s “account” section

Compile the [simple timelock contract](https://github.com/second-state/simple-timelock-smart-contract/blob/main/SimpleTimelock.sol)

Deploy the Timelock contract; making sure that Remix’s “contract” dropdown section is set to “SimpleTimelock.sol”

**You must put the address of the ERC20 token as the one and only parameter for the constructor.**

