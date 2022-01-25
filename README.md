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

## Step 4
Set the time stamp of the contract by calling the setTimestamp function. There is only one function parameter called `_timePeriodInSeconds`; which reflects the amount of time (in seconds) for which you want the time lock period to exist.

**timestampSet**

Check that the `timestampSet` variable is `true`

![Screen Shot 2022-01-24 at 12 58 00 pm](https://user-images.githubusercontent.com/9831342/150715021-63881e4f-02d8-43d5-a421-452ce2155461.png)

**initialTimestamp**

Check the `initialTimestamp` variable, and confirm its value in proper date format by using [an online epoch to date converter](https://www.epochconverter.com/)

![Screen Shot 2022-01-24 at 1 00 20 pm](https://user-images.githubusercontent.com/9831342/150715109-8ef231f7-45f3-48a8-8c1a-25bc9b561a66.png)

For example, the value in the above image, `1642993044` is equivalent to `Monday, 24 January 2022 12:57:24 GMT+10:00`

## Step 5

Checking the associated ERC20 contract.

First of all, please check to make absolutely sure that the ERC20 contract associated with this timelock contract is correct. This can be done by calling the `erc20Contract` variable, as shown below.

![Screen Shot 2022-01-24 at 1 09 22 pm](https://user-images.githubusercontent.com/9831342/150715931-edfe5dde-1c6c-4651-8239-c6cb01b27971.png)

## Step 6

Allocating user tokens into the timelock contract.

Tokens can be allocated to users one at a time using the `depositToken` function, as shown below.

![Screen Shot 2022-01-24 at 1 11 21 pm](https://user-images.githubusercontent.com/9831342/150716076-6d6bed3b-25ac-48ce-b54a-f7d7a3e94b26.png)

Tokens can also be allocated in bulk using the `bulkDepositTokens` function. This is done using [a third-party script](https://github.com/ParaState/timelock-token-deployment#bulk-deposit-tokens). Please contact via an issue for access to this script.

Always keep an exact record of how many tokens (sum total of all ERC20 tokens) which you allocated to the users. This sum total figure is required for the next step (and ensures that there will be the exact amount of tokens in the timelock contract to service all of the users, who will be performing the unlock).

## Step 7

Transfer ERC20 tokens to the timelock contract.

From the ERC20 token contract, use the `transfer` function to transfer ERC20 tokens to the timelock smart contract's address.

![Screen Shot 2022-01-24 at 1 15 46 pm](https://user-images.githubusercontent.com/9831342/150716642-b2d63734-e928-4513-aa44-860e016be358.png)

You can confirm that these tokens have been transferred by pasting the timelock contract's address into the ERC20 contract's `balanceOf` function, as shown below.

![Screen Shot 2022-01-24 at 1 19 48 pm](https://user-images.githubusercontent.com/9831342/150716797-ec250368-538d-4105-80c2-8427031b57c6.png)

## Step 8

Finalize owner participation.

Once all allocations have been made and the ERC20 tokens have been transferred into the timelock contract, the owner can call the timelock contract's `finalizeAllIncomingDeposits()` function. This makes the timelock non-custodial, whereby the contract owner has no ability to alter token amounts and so forth. The operation of the timelock contract is purely based on the math in the `transferTimeLockedTokensAfterTimePeriod` function from this point forward.

## Step 9

This simple timelock smart contract has an open source front end user interface. Please follow the instructions there to deploy this on the open web.

