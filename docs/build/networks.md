# Supported Network

The [Msgport Protocol](./../index.md) is a robust and reliable cross-chain messaging protocol that has been deployed on many mainstream Ethereum blockchains, This protocol has undergone careful revisions to enhance its developer and user-friendliness.

## Canonical Cross-chain Contract

The Msgport protocol is a set of contracts that defines the [core interfaces](./interfaces.md) for sending and receiving cross-chain messages. You can think of it as an abstract class in programming, with `Msgport` as its name.
This abstract class can have multiple subclasses, known as messaging protocols, which extend its functionality. Each of these subclasses must adhere to the interfaces defined in the Msgport protocol. To be user-friendly, each messaging protocol has 
its unique contract address across all the networks it supports. The table below shows the canonical cross-chain contract address for each supported network.

|  Contract              |  Canonical Cross-chain Deployment Address  |
|------------------------|--------------------------------------------|
| SubAPIMultiSig         | 0x22117Db68370590c1031f52a6D1aDE3DCe0cCf9a |
| [ORMP](../learn/messaging-protocols/ormp.md) | 0xA72d283015c01807bc0788Bf22C1A774bDbFC8fA |
| Oracle                 | 0x3f938756ceFa33665719Eb528E581FF3f460b7C6 |
| Relayer                | 0xaC2b224c2E1eD2E8663097a361A05a72d6671C7D |
| ORMPUpgradeablePort    | 0x8d22f03a675064BFd7509c87206d33730f33e324 |

## Supported Networks

The ORMP messaging protocol is available on the following main/test networks, which means you can integrate cross-chain capabilities into your application without needing to deploy the underlying messaging protocol yourself. If your desired network is not listed, please feel free to reach out to our team for support and we will be happy to assist you.

**NOTE**: All the chains listed above are connected, except for the Tron network, which is only connected to Darwinia network.

### For Mainnet

- Arbitrum
- Blast
- Crab
- Darwinia
- Ethereum
- Polygon
- Moonbeam

#### Tron
```
SUBAPIMultiSig: TMP3K1GjRgsXAUHX1jkBaBwaordRi9gHRH
ORMP: TBuAR5bP2KoJ6Thx4zFqGChSARNRYrknTD
Oracle: TYYcXSzzc8r4Q17xrYUtqWEMtKUNwNictu
Relayer: TWArBv4oRtVE4MAkqaEVHHiBQX1Wc7xDg6
ORMPUpgradeablePort: TVT1osWgsPvdwxN9rPm7rRo78naN3fA23x
```

### For Testnet

- Arbitrum Sepolia
- Sepolia
- Darwinia Pangolin
- Tanssi Pangoro
- Taiko Hekla

#### Tron Shasta
```
SUBAPIMultiSig: TEYbMKVNpumbN5myf5uN6VgFStckj9DGe5
ORMP: TN1j3Ttt1c1mB3X2zdKkdMsUK6pZyLCxSr
Oracle: TGaaHxjof9QcfKwggnFVM3QwjGKzbuNzNk
Relayer: TRediXQ8qcTqorMQqJ2jQgqnjUojWZo2qc
ORMPUpgradeablePort: TQ49GJrj2wQ7RdhRGT26izeRypcQqwNFpo
```
