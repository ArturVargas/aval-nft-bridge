# Avalanche Non Fungible Token Transfer

Avalanche Non Fungible Token Transfer is an application that allows users to transfer tokens between Subnets. The implementation is a set of smart contracts that are deployed across Subnets, and leverages Teleporter for cross-chain communication.

Each token transferrer instance consists of one "home" contract and at least one but possibly many "remote" contracts. Each home contract instance manages one asset to be transferred out to TokenRemote instances.
The home contract lives on the C-Chain where the asset to be transferred exists. A transfer consists of locking the asset as collateral on C-chain and minting a representation of the asset on the remote Subnet. The remote contracts, each of which has a single specified home contract, live on other Subnet that want to import the asset transferred by their specified home. The token transferrers are designed to be permissionless: anyone can register compatible TokenRemote instances to allow for transferring tokens from the TokenHome instance to that new TokenRemote instance.
The home contract keeps track of token balances transferred to each TokenRemote instance, and handles returning the original tokens back to the user when assets are transferred back to the TokenHome instance. TokenRemote instances are registered with their home contract via a Teleporter message upon creation.
Home contract instances specify the asset to be transferred as either an ERC721 token, and they allow for transferring the token to any registered TokenRemote instances. The token representation on the remote chain can also either be an ERC721, allowing users to have tokens between home and remote chains:
ERC721 —> ERC721

The remote tokens are designed to have the same metadata and the origin smart contract address as reference.

## How to develop

1. Create a Subnet connected on Fuji
2. [Implement Teleporter on Subnet](https://github.com/ava-labs/teleporter)
3. Deploy a Smart Contract NFT on fuji c-chain
4. You can mint sending messages with the same nft metadata

[!Diagram](https://github.com/ArturVargas/aval-nft-bridge/blob/main/photo_2024-07-09%2002.17.49.jpeg)

   
