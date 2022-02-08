<p align="center">
  <a href="https://www.quadswap.finance">
    <img alt="Quadswap Logo" src="src/images/quadswap-logo-blue-bordered-thin.png" width="60" />
  </a>
</p>
<h1 align="center">
  QuadSwap
</h1>

A decentralized finance swap platform and liquidity provider product developed at [Miami Hack Week](https://twitter.com/MiamiHackWeek) for the [Terraform Labs](https://www.terra.money/) development house.

## 🤝 DeFi and QuadSwap

**What is Liquidity Providing?**

Exchanges need liquidity to allow a trade between two assets. For example, to trade Bitcoin (BTC) for Ethereum (ETH), and vice versa, there needs to be enough of both BTC and ETH supplied for either side of the trade of the ETH/BTC pair.

Contrasting to centralized custodian exchanges, decentralized exchanges (DEXes) allow users to be the liquidity providers (LP) and accrue the trading fees proportional to the amount of liquidity they provided.

The common LP instrument is the LP pair, a pair of two assets. These two assets will be self-balancing; if asset A goes up in value, it will automatically sell off to buy asset B, bringing the value of both asset A and asset B back to equal value.

**What is our Product?**

Our product is an LP pair of two LP pairs; a new asset class of four self-balancing assets. This introduces increased value to both the liquidity user and the liquidity provider.

Our example case and first QuadSwap LP pair is LUNA-bLUNA LP / LUNA-UST pair.

With this pair, users can swap between their LUNA-bLUNA LP which is a 100% exposure to LUNA, and LUNA-UST which is a 50% exposure to LUNA. The use case for swapping between these pairs is to adjust the LUNA exposure from and between 50% and 100% to risk-on or risk-off depending on market conditions and trend.

Additionally, we will be creating more QuadSwap LP pairs each with its particular value proposition.

**The Users and their Value**

1. Liquidity User

    Normally, to swap from one LP pair to another, the user would have to take their first LP pair A and:
    
    - a) decontruct it to it's two respective assets A<sub>1</sub> and A<sub>2</sub> 

    - b) sell those assets A<sub>1</sub> and A<sub>2</sub> for the assets of the second LP pair B<sub>1</sub> and B<sub>2</sub>

    - c) reconstruct the two B<sub>1</sub> and B<sub>2</sub> assets into the LP pair B.

    However, now with QuadSwap, users can directly swap their LP pair for another LP pair.

    This direct swap streamlines away the manual and multiple-transaction process to get from one LP pair to another, lowering the cost and friction of the LP swap process.

1. Liquidity Provider

    The liquidity provider benefits from their QuadSwap LP pair as they are holding four assets that self-balance for increased portfolio diversity and ease of portfolio management, and increased value accrual from not only the first LP and the second LP trading fees but now the trading fee accrual between the direct swap of the two LPs.

## 💻 Hack Week

**The Process**

Developing QuadSwap consisted of two tasks:
1. Developing the DeFi product
1. Developing the swap platform

Developing the DeFi Product

We invoked smart contracts from Terra using the Terra Station interface.

This took us the first two days of determining the correct combination of smart contracts to call with the correct parameters. With the smart contracts not successful in creating our QuadSwap LP pair, we attempted the same process on the legacy Terra Station interface as well as through the [terrad](https://docs.terra.money/docs/develop/how-to/terrad/using-terrad.html) command-line interface with a running Terra node, both to no avail.

Finally, we invoked the correct combination and parameters of smart contracts through the Terra Station interface and we successfully created and supplied liquidity to our QuadSwap LP pair. You can look at our token [here](https://finder.extraterrestrial.money/testnet/address/terra14fyevljvlw9qtk08vxak902jw835la6ach5m30) and our smart contract [here](https://finder.extraterrestrial.money/testnet/address/terra1xmthceqzfqvrrcnhfzdaku30w5ja7r02h3sgkn) on Extraterrestrial Finder.

Developing the Swap Platform

Although the Terra blockchain is large as a Top 5 Layer-1 Protocol with (as of writing this) a [marketcap over 23 Billion USD](https://cryptowat.ch/assets) and a [total locked value over 12 Billion USD](https://defillama.com/chain/Terra), the Terra ecosystem is relatively new. This means there's a large opportunity for applications on Terra to emerge and to attract billions in volume to their platform.

With that said, there are currently only two swap platforms: [terraswap](https://terraswap.io/) and [Astroport](https://astroport.fi/). Astroport's front-end web application was not available being closed-source. We decided to fork the terraswap web application and develop our QuadSwap swap platform from there.

We spent three days refactoring and configuring the terraswap web application, however, the code base had significant issues with an unclean project structure and redundant and failing APIs calls.

For example, retrieving the token list takes numerous seconds to load. We presumed this was to do with the calling of data and the interaction with the blockchain. However, the platform was being stalled because it was waiting on the result of over 120 failed API calls.

We deemed it was not reusable given the inefficient complexity of when and which APIs were called and the fact that API being used was private. We substituted the API endpoints for our own for the APIs that returned the tokens available and the list of pairs, however, we didn't have the data to create the API endpoints that called price prediction and smart contract references.

On the last day still working on the project at our demo booth before judging started, we were able to successfully create our swap platform by developing from an open-source fork of terraswap developed by [octalMage](https://github.com/octalmage) provided a usable cleaned code base to work with.

We successfully sent the first direct LP to LP swap transaction on the Terra blockchain.

## 🚀 Usage

1.  **Open the QuadSwap web application.**

    Link: https://quadswap.finance/

1.  **Connect your Terra Station wallet.**

    Choose from one of the wallet options. Select the network to be testnet.
    
1.  **Obtain the LP pairs to swap.**

    Ensure you have both the LUNA-bLUNA LP token and LUNA-UST LP token in your wallet. If you need funds you can receive funds through the [Terra Testnet Faucet](https://faucet.terra.money/). If you need the LP pairs, you can Swap for the respective assets of LUNA, bLUNA, and UST needed, and Provide for the respective LP pairs on [terraswap](https://app.terraswap.io/swap?to=&type=swap&from=uluna).

1.  **Make the Swap!**

    Select the LP pair and the amount to swap from and the LP pair to swap to. Click the swap button, approve the transactions, and your direct LP to LP swap will be broadcasted!


## 🧐 What's inside?

A quick look at the top-level files and directories where we made our feature changes in the project.

    src
    ├── pairs.json
    ├── tokens.json
    └── cw20
          ├── useTokenBalance.ts
          └── post
               └── hooks
                     └── wallet
                          └── useSwap.ts



1.  **`/src`**: This directory will contain all of the code related to what you will see on the front-end of the site. `src` is a convention for “source code”.

1.  **`pairs.json`**: This file contains the list of LP pairs for mainnet and testnet, which will be our QuadSwap LP pair token.

1.  **`tokens.json`**: This file contains the list of tokens for mainnet and testnet, which will be our LUNA-bLUNA LP token and LUNA-UST LP token.

1.  **`/cw20`**: This directory contains the typescript files for the hooks regarding retrieving token data.

1.  **`useTokenBalance.ts`**: This file is the hook that retrieves the balance data from the list of tokens provided. We made modifications for `tokens.json` to be used instead of the original list of tokens retrieved through and persisted in state management.

1.  **`/post/hooks/wallet`**: This directory contains the typescript files for the hooks regarding the interaction of the live swap transaction and the user's terra wallet.

1.  **`useSwap.ts`**: This file contains the const functions needed and used for the swap transaction. We removed `nativeTokensOptions` as we are working with our own non-native tokens.

## 📣 Recognition

This project was completed in collaboration with [anonintern](https://github.com/anonintern). Thank you to [Terraform Labs](https://www.terra.money/) and [Hashed](https://www.hashed.com/) that made creating this project possible and especially to [octalMage](https://github.com/octalmage) for the development support.