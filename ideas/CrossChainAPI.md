# Idea

Enable cross chain transfers using a stable coin AMM for bridge pools.

# Overview

At time of writing Harmony has [$95 Million of Bridged Assets](https://bridge.harmony.one/tokens). To move these assets across chains they need to be swapped to the corresponding bridged asset on Harmony. This is currently done via AMM'S with standard bonding curves, however a stable coin AMM can provide a more efficient swap with lower slippage.


This will provide the ability for users to deposit tokens using one click.
This leverages trades to swap the tokens enabling the deposit of the required tokens in to the liquidity pools.
Also should leverage bridges to allow users to deposit tokens from say ETH to Harmony Liquidity Pools.

# Acceptance Criteria
* Pre-bridged tokens
  * Can jump BUSD from ETH TO BSC and back
  * Can Jump tokens into a liquidity Pool
  * Configurable with token and chain from and to
* Unbridged Tokens
  * Can Jump Tokens to Harmony
  * Can Jump Tokens into a Liquidity Pool 
  * Can Jump tokens to another chain (via lock and  mint, unlock and burn)
# Design
* [User Interface](https://github.com/KangaFinance/kanga-interface/blob/joey/src/pages/jump/index.tsx)
  * Modify to include above scenarios
  * Modify abi's to leverage jump abi's
  * Review [zapper.fi](https://zapper.fi/) [exchange](https://zapper.fi/exchange) and [bridge](https://zapper.fi/bridge)
* [SDK](https://github.com/KangaFinance/kanga-sdk)
  * Move jump contracts and abi's into sdk
* [Smart Contract](https://github.com/KangaFinance/jump)
  * move jump into kanga and update harhat to build based on tags for each module
* [API](https://github.com/KangaFinance/kanga-api)
  * Review [Zapper API Swagger](https://api.zapper.fi/api/static/index.html)
  * Review [Harmony Cross Chain API](https://github.com/harmony-one/crosschain-api)
* Additional Items
  * Create a token-list repo to manage metadata about jump tokens
  * Create a demo repo similar to [zapper fi](https://github.com/Zapper-fi/Zapper-API-Stack)
  * Create a Postman collection
  * Create a swagger api

## Endpoints
**Jump In**
* {type}/supported - Provides a list of networks to protocols that are supported by the Jump In routes.
* {type}/{protocol}/approval-state - Retrieves an ERC20 approval status for a protocol jump-in
* {type}/{protocol}/approval-transaction  - builds an ERC20 approval transaction for a protocol jump-in
* {type}/{protocol}/transaction  - Builds a jump-in transaction for usage with etherjs, complete with best swap from kanga

**Jump Out**
* {type}/supported - Provides a list of networks to protocols that are supported by the Jump In routes.
* {type}/{protocol}/approval-state - Retrieves an ERC20 approval status for a protocol jump-in
* {type}/{protocol}/approval-transaction  - builds an ERC20 approval transaction for a protocol jump-in
* {type}/{protocol}/transaction  - Builds a jump-in transaction for usage with etherjs, complete with best swap from kanga

**Jump Bridge**
* {destinationNetwork}/supported - Provides a list of networks to protocols that are supported by the Jump In routes.
* {type}/{destinationNetwork}/approval-state - Retrieves an ERC20 approval status for a protocol jump-in
* {type}/{destinationNetwork}/approval-transaction  - builds an ERC20 approval transaction for a protocol jump-in
* {type}/{destinationNetwork}/transaction  - Builds a jump-in transaction for usage with etherjs, complete with best swap from kanga


# References
- [Inari UI](https://app.sushi.com/inari)
- [Kanga Contracts](https://github.com/kangafinance)
  - [KangaZap](https://github.com/KangaFinance/jump/blob/main/contracts/KangaZap.sol) - used to invest in given KangaSwap pair through ETH/ERC20 Tokens
  - [JumpV1](https://github.com/KangaFinance/jump/blob/main/contracts/JumpV1.sol) - Allows jumping into Lending(Troop) Flash(Mob) AAVE, COMPOUND/CREAM
  - [Zenko.sol](https://github.com/KangaFinance/jump/blob/main/contracts/Zenko.sol) - to and from Mob, Troop and Compound/Cream
  - [BoringBatchable](https://github.com/KangaFinance/jump/blob/main/contracts/BoringBatchable.sol) - Allows batch calls on itself taking an array of inputs and reverts after a failed call and stops doing further calls.
- Zapper.fi
  - [github](https://github.com/Zapper-fi)
  - [endpoints](https://docs.zapper.fi/zapper-api/endpoints)
  - [docs](https://docs.zapper.fi/zapper-api/api-guides/zap-in)

- Bridge - MDEX, SerumDex, xcmp, ics, snowfork, statemint
    - Bridge ui's - [mdex](https://mdex.com/#/bridge)
    - Whitepapers
        - [serum](https://projectserum.com/serum_white_paper.pdf), [xcmp](https://wiki.polkadot.network/docs/en/learn-crosschain), hrmp, [harmony horizon](https://github.com/harmony-one/papers/blob/master/horizon.pdf) [near](https://near.org/blog/eth-near-rainbow-bridge/), [ics](https://github.com/cosmos/ibc), [snowfork](https://github.com/Snowfork/polkadot-ethereum)
        - [andre](https://andrecronje.medium.com/) - [multichain dapp](https://andrecronje.medium.com/multichain-dapp-guide-standards-and-best-practices-8fabe2672c60) [crosschain-token](https://andrecronje.medium.com/deploying-your-own-cross-chain-token-101-240420efd0d9) [crosschain-swap](https://andrecronje.medium.com/what-is-this-cross-chain-stuff-3528540423e1)