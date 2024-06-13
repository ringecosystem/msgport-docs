# Supported Network

The [Msgport Protocol](./../index.md) is a robust and reliable cross-chain messaging protocol that has been deployed on many mainstream Ethereum blockchains, This protocol has undergone careful revisions to enhance its developer and user-friendliness.

## Canonical Cross-chain Contract

The Msgport protocol is a set of contracts that defines the [core interfaces](./interfaces.md) for sending and receiving cross-chain messages. You can think of it as an abstract class in programming, with `Msgport` as its name.
This abstract class can have multiple subclasses, known as messaging protocols, which extend its functionality. Each of these subclasses must adhere to the interfaces defined in the Msgport protocol. To be user-friendly, most of the messaging protocol has 
its unique contract address across all the networks it supports. The table below shows the canonical cross-chain contract address for each supported network.

|  Contract              |  Canonical Cross-chain Deployment Address  |
|------------------------|--------------------------------------------|
| SubAPIMultiSig         | 0x22117Db68370590c1031f52a6D1aDE3DCe0cCf9a |
| [ORMP](../learn/messaging-protocols/ormp.md) |  0x13b2211a7cA45Db2808F6dB05557ce5347e3634e |
| Oracle                 | 0xBE01B76AB454aE2497aE43168b1F70C92Ac1C726 |
| Relayer                | 0x114890eB7386F94eae410186F20968bFAf66142a |
| ORMPUpgradeablePort    | 0x2cd1867Fb8016f93710B6386f7f9F1D540A60812 |
| MsgDeployer            | 0x040f331774Ed6BB161412B4cEDb1358B382aF3A5 |

However, the Tron network and it's testnet(Shasta) have its their canonical cross-chain contract address due to its special design, list below:

|  Contract                |  Canonical Cross-chain Deployment Address  |
|--------------------------|--------------------------------------------|
| Tron SUBAPIMultiSig      | TMP3K1GjRgsXAUHX1jkBaBwaordRi9gHRH |
| [Tron ORMP](../learn/messaging-protocols/ormp.md) | TJPZeFEdc4TBEcNbku5xVZLQ6B2Q1oGnd1 |
| Tron Oracle              | TV9FgX1jHSg1k6kEaZtYR2ZH4AdqnMCDak |
| Tron Relayer             | TSZgvR9xTGeG3RXcUKnWWcUAAAEskXdCHj |
| Tron ORMPUpgradeablePort | TFRF7t9m7pGLnwwX8TFsZvj85EvQ6gSBCm |

| Contract                  |  Canonical Cross-chain Deployment Address  |
|---------------------------|--------------------------------------------|
| Shasta SUBAPIMultiSig      | TEYbMKVNpumbN5myf5uN6VgFStckj9DGe5 |
| [Shasta ORMP](../learn/messaging-protocols/ormp.md) | TPJifBA5MvFf918VYnajd2XmEept4iBX55 |
| Shasta Oracle              | TDULRJrJ2bbsvW3KKtEnnq9moPn5PyUWpd |
| Shasta Relayer             | TZGjiJcoqUo6JSZeYvrwN6qvpEcLm21QbG |
| Shasta ORMPUpgradeablePort | TSZCvXyP618r4AxYmVD15Zu46VB3AFeAyd |

## Supported Networks

The ORMP messaging protocol is available on the following main/test networks, which means you can integrate cross-chain capabilities into your application without needing to deploy the underlying messaging protocol yourself. If your desired network is not listed, please feel free to reach out to our team for support and we will be happy to assist you.

### For Mainnet

- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Crab](https://crab.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Arbitrum](https://arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Ethereum](https://etherscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Polygon](https://polygonscan.com/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Moonbeam](https://moonscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia](https://darwinia.subscan.io/account/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Tron](https://tronscan.org/#/contract/TJPZeFEdc4TBEcNbku5xVZLQ6B2Q1oGnd1)
- [Arbitrum](https://arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Blast](https://blastscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Ethereum](https://etherscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋ [Arbitrum](https://arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)

### For Testnet

- [Darwinia Koi](https://koi-scan.darwinia.network/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Arbitrum Sepolia](https://sepolia.arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Darwinia Koi](https://koi-scan.darwinia.network/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Tron Shasta](https://shasta.tronscan.org/#/contract/TPJifBA5MvFf918VYnajd2XmEept4iBX55)
- [Darwinia Koi](https://koi-scan.darwinia.network/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Sepolia](https://sepolia.etherscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Sepolia](https://sepolia.etherscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Arbitrum Sepolia](https://sepolia.arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
- [Sepolia](https://sepolia.etherscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Tron Shasta](https://shasta.tronscan.org/#/contract/TPJifBA5MvFf918VYnajd2XmEept4iBX55)
- [Arbitrum Sepolia](https://sepolia.arbiscan.io/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e) ⇋  [Taiko Hekla](https://explorer.hekla.taiko.xyz/address/0x13b2211a7cA45Db2808F6dB05557ce5347e3634e)
