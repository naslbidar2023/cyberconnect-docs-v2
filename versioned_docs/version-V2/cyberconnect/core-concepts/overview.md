---
id: Overview
title: Overview
slug: /core-concepts/overview
sidebar_label: Overview
sidebar_position: 1
description: Concepts - Overview
---

The CyberConnect protocol consists of a set generative smart contracts deployed on BNB chain. Generative smart contracts means the protocol will generate a set of new smart contracts associated with dApps or users when they interact with the protocol. This pattern is similar to the Uniswap protocol where a set of liquidity pair smart contracts will be generated when people create a new liquidity pool.

On CyberConnect, these generated smart contracts enable dApps to create their context-specific on-chain social network or users to issue their customizable NFTs to monetize their social data. At a high level, the protocol represents social data using three main contracts (all implementations of the ERC721 standard):

1. [ccProfileNFT](/core-concepts/cc-profile) 👤
2. [SubscribeNFT](/core-concepts/subscribe-nft) 👥
3. [EssenceNFT](/core-concepts/essence-nft) 📝

# Architecture

![gp_sm](/img/v2/Smart_Contract_Protocol_overview.png)

## ccProfileNFT 👤

ccProfileNFT represents each user’s profile as an NFT. It serves as a prerequisite for users who want to issue their customized EssenceNFTs or SubscribeNFTs. In addition, the deployed ccProfileNFT contract is used as the gateway for users to perform actions such as collecting essence, creating a profile, and subscribing to a profile in a specific dApp context. Developers can integrate the ccProfileNFT into their dApp/protocol to benefit from the existing network of identities being built through Link3 and other CyberConnect integrated protocols.

Similar to an ENS domain, developers are able to use CyberConnect to map all on-chain credentials/assets to the ccProfileNFT. Whether it’s an NFT, an SBT, a Twitter handle, or a DID, we map all of them to one holistic identity: the ccProfileNFT.

<img src="https://media.giphy.com/media/ONopM3fhonIkFxVKWw/giphy.gif" alt="ccProfile" width="200" height="400" class="center" />

## SubscribeNFT 👥

SubscribeNFT represents the uni-directional relationship between an address and a ccProfileNFT. Each ccProfileNFT holder can only issue one unique SubscribeNFT. Each SubscribeNFT can be configured with rules like pay-to-follow (paid subscribers), hold-to-follow (token-gated community), etc. The SubcribeNFT is highly-customizable and can be used to represent arbitrary social connections; including following, subscribing to a creator, friend relationship, belonging to an organization, and participations in activities and communities.

![follow-gif](/img/v2/follow-gif.gif)

## EssenceNFT 📝

EssenceNFT is a generic NFT that individual ccProfileNFT holders can issue to represent any piece of content (ex. social media posts, videos, blog publications). Each EssenceNFT can be configured with rules like pay-to-mint (crowdfunding), hold-to-mint (community participants), etc. It can be also configured as a tradable NFT or a non-transferable soul bound token (SBT) to represent a given role such as investor, patron, team member, community participant, etc.

## Composable Middleware

Although the computational condition varies a lot on different dApps, many commonly seen patterns can be generalized into reusable and extensible modules. For example, dApp A wants to build a BAYC club by setting the condition that only BAYC holders can mint their app-specific ccProfileNFT and dApp B wants to do the same thing for CloneX holders. The underlying pattern is the same and the only difference is the gated ERC-721 contract address.

The protocol utilizes a composable middleware layer before and after the user applies their minting actions (e.g. subscribe to a profile or collect essence). The middleware can be created to express generic constraints such as allowing only certain ERC-721 holders to pass the check. In such a way, the community can build a wide range of reusable middlewares together and dApp developers can pick and choose the relevant ones to plug into their dApp easily.

It is important to point out though that while the middleware is powerful when used to set constraints against the current blockchain state or to collect on-chain assets, it has limited utility when using it to check historical state or off-chain data. One possible solution is to call oracle contracts inside middleware to get data feeds from off-chain indexers.

You can find query examples & the GraphQL schema in Apollo for your reference.

- [Schema](https://studio.apollographql.com/public/Cyberconnect-Gaia-Stg-6ewjtr/schema/reference?variant=current)
- [Query Examples](https://studio.apollographql.com/public/Cyberconnect-Gaia-Stg-6ewjtr/explorer?variant=current)