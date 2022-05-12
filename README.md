# Uniswap V2

[![Actions Status](https://github.com/Uniswap/uniswap-v2-periphery/workflows/CI/badge.svg)](https://github.com/Uniswap/uniswap-v2-periphery/actions)
[![npm](https://img.shields.io/npm/v/@uniswap/v2-periphery?style=flat-square)](https://npmjs.com/package/@uniswap/v2-periphery)

In-depth documentation on Uniswap V2 is available at [uniswap.org](https://uniswap.org/docs).

The built contract artifacts can be browsed via [unpkg.com](https://unpkg.com/browse/@uniswap/v2-periphery@latest/).

# Local Development

The following assumes the use of `node@>=10`.

## Install Dependencies

`npm i`

## Compile Contracts

`truffle compile`

## Deployed Contracts

Contracts have been deployed on BSC Testnet and Polygon Mumbai Testnet 

### BSC

GlobalXRouter: https://testnet.bscscan.com/address/0x2561448Acc10A42Ee0aa0A1D5c0f84E14C9e407F

GlobalXFactory: https://testnet.bscscan.com/address/0x2e05a84d53ab9fc1c4377d3dfb5715a0368a4187

Mintable Mock STIR: https://testnet.bscscan.com/address/0xee1fb970faf38647289900d2b990685beff45d69

### Polygon

GlobalXRouter: https://mumbai.polygonscan.com/address/0x0ad86c981880d7d70a747f457f8c2bc3910de2bc

GlobalXFactory: https://mumbai.polygonscan.com/address/0x1ce04cded1a8f9b21bc8d880a5a05a8d869e3b7f

Mintable Mock STIR: https://mumbai.polygonscan.com/address/0x4039f5f14f1530bdeda410bdf7eee10ac47a7389

## How to Interact with contracts 

The Router contract is the main contract via which you can swap tokens, add liquidity and perform all the functions. 

### Swap Functionality 

There are two functions to do a swap, 

function 1 is `swapExactTokensForTokens` and function 2 is `swapTokensForExactTokens`

The difference is that there is always a slipage when you make a trade, so you can not exactly calculate how many tokens you will get for a fixed amount.

`swapExactTokensForTokens` will take a fixed amount of tokens from you and will give you some tokens in return. 

Example : There is an TESLA/STIR pool, price of tesla is 150 USD and price of STIR is 1 USD. There is a user who has 100 STIR and wants to convert all 100 STIR into TESLA Tokens. Then he will use `swapExactTokensForTokens`

`swapTokensForExactTokens` will take a unfixed amount of tokens from you and will give you fixed amount of tokens.

Example : There is an TESLA/STIR pool, price of tesla is 150 USD and price of STIR is 1 USD. There is a user who has 100 STIR, but he wants exactly 1 TESLA token. Then he will use `swapTokensForExactTokens`

#### swapExactTokensForTokens

`function swapExactTokensForTokens(
uint amountIn,
  uint amountOutMin,
  address[] calldata path,
  address to,
  uint deadline
) external returns (uint[] memory amounts);`

* amountIn : The amount of input tokens to send.
(If user wants to convert exactly 100 STIR to Tesla, amountIn will be 100 STIR Token)
* amountOutMin : The minimum amount of output tokens that must be received for the transaction not to revert.
* path : An array of token addresses. path.length must be >= 2. Pools for each consecutive pair of addresses must exist and have liquidity.
(In This case the path would be `['STIR token Address', 'TESLA token Address']`)
* to : Recipient of the output tokens.
* deadline : Unix timestamp after which the transaction will revert.


#### swapTokensForExactTokens

`function swapTokensForExactTokens(
  uint amountOut,
  uint amountInMax,
  address[] calldata path,
  address to,
  uint deadline
)  external returns (uint[] memory amounts);`

* amountOut: The amount of output tokens to receive.
(If user wants to convert STIR and recieve exactly 1 TESLA token, amountOut will be 1 TESLA token)
* amountInMax: The maximum amount of input tokens that can be required before the transaction reverts.
* path : An array of token addresses. path.length must be >= 2. Pools for each consecutive pair of addresses must exist and have liquidity.
(In This case the path would be `['STIR token Address', 'TESLA token Address']`)
* to : Recipient of the output tokens.
* deadline : Unix timestamp after which the transaction will revert.
