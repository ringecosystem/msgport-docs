# Overview

The cross-chain mcessage protocol serves as the underlying technology for cross-chain applications. It acts as a middleman, encapsulating the differences between various blockchains and providing easier support for building cross-chain applications. This protocol functions similarly to an operating system, which acts as a mediator between the machine and users, simplifying the interaction and enhancing compatibility. By leveraging this protocol, developers can seamlessly integrate different blockchains and unlock the full potential of cross-chain functionality.

## Design Principles

- **Guaranteed Delivery:** The protocol must ensure that when a message is successfully committed on the source chain, it will be delivered to the target chain as long as both chains are actively producing blocks. This guarantees that important information is reliably transmitted between chains.
- **Trustless Interoperability:** Users can confidently interact with our system without having to trust any individual or party to act honestly. The protocol must ensure that transactions cannot be exploited by bad actors. This enhances the security and reliability of cross-chain communication.
- **Flexible Message Structure:** The protocol allows messages to be encoded and decoded in any desired way. This flexibility removes the complexity of building chain-specific integrations, making it easier to send messages across different blockchains.

## Current Supported Protocols

| Protocol | Description |
| :--------: | :----------- |
| [ORMP](./ormp.md) | Oracle Relayer Messaging Protocol, based on the Oracle mechanism, as darwinia msgport's default messaging protocol. |
| [XCMP](./xcmp.md) | XCMP, which is based on Polkadot XCM, is on our roadmap for support. |
| [LCMP](./lcmp.md) | Light Client Cross-Chain Messaging Protocol, used for years in Darwinia, currently replaced by ORMP. |