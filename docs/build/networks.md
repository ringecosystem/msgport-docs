# Supported Network

The [Msgport Protocol](./../index.md) is a robust and reliable cross-chain messaging protocol that has been deployed on many mainstream Ethereum blockchains, This protocol has undergone careful revisions to enhance its developer and user-friendliness.

## Canonical Cross-Chain Contract

The Msgport protocol is a set of contracts that defines the [core interfaces](./interfaces.md) for sending and receiving cross-chain messages. You can think of it as an abstract class in programming, with `Msgport` as its name.
This abstract class can have multiple subclasses, known as messaging protocols, which extend its functionality. Each of these subclasses must adhere to the interfaces defined in the Msgport protocol. To be user-friendly, each messaging protocol has 
its unique contract address across all the networks it supports. The table below shows the canonical cross-chain contract address for each supported network.

|   Name     |  Canonical Cross-Chain Contract Address  |
|------------|--------------------------------------------|
|   [ORMP](../learn/messaging-protocols/ormp.md)     | 0x0000000005d961F950adA391C1511c92bbc64D9F |

## Supported Networks

The ORMP messaging protocol is available on the following main/test networks, which means you can integrate cross-chain capabilities into your application without needing to deploy the underlying messaging protocol yourself. If your desired network is not listed, please feel free to reach out to our team for support and we will be happy to assist you.

### For Mainnet

- [Ethereum](https://etherscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Arbitrum](https://arbiscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Ethereum](https://etherscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Darwinia](https://darwinia.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Arbitrum](https://arbiscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Darwinia](https://darwinia.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Arbitrum](https://arbiscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Blast](https://blastscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Polygon](https://polygonscan.com/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Darwinia](https://darwinia.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Crab](https://crab.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Darwinia](https://darwinia.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)

### For Testnet

- [Sepolia](https://sepolia.etherscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Arbitrum Sepolia](https://sepolia.arbiscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Sepolia](https://sepolia.etherscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Pangolin](https://pangolin.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)
- [Arbitrum Sepolia](https://sepolia.arbiscan.io/address/0x0000000005d961F950adA391C1511c92bbc64D9F) ⇋ [Pangolin](https://pangolin.subscan.io/account/0x0000000005d961F950adA391C1511c92bbc64D9F)