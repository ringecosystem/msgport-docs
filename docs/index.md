# What is Msgport?

Msgport gets its name from hubs of connectivity, such as airports, seaports, and spaceports, because it serves as a gateway for messages between different blockchain systems. By acting as a crucial hub, Msgport enables the connection of various blockchain systems with minimal changes to their underlying architecture. Specifically, Msgport defines a set of [essential interfaces](./build/interfaces.md) for cross-chain communication, including sending, receiving, and verifying messages. This is similar to a superclass or abstract class in programming, which outlines a template for functionality. Concrete implementations of Msgport, known as [messaging protocols](./learn/messaging-protocols/overview.md), may vary to accommodate the unique designs of different underlying blockchains. However, as long as an implementation adheres to the Msgport interfaces, it can be used interchangeably, making it easier for developers to create cross-chain decentralized applications.

## Core Components and Innovations

The Msgport encompasses a collection of smart contracts that outline standardized interfaces for facilitating a cross-chain messaging protocol. 

At the heart of this system is the core interface, [IMessagePort](./build/interfaces.md#imessageport), which is designed with flexibility to support various implementations. 

![msgport-overview-1](./images/msgport-overview-1.png)

Highlighting Msgport's versatility are its flagship integrations:

  - [ORMP](./learn/messaging-protocols/ormp.md): Oracle Relayer Messaging Protocol leverages chain-independent components, such as oracles and DApp-preferred relayers, to verify cross-chain messages. This approach integrates diverse verification mechanisms, ensuring robust and flexible cross-chain communication.
  - [LCMP](./learn/messaging-protocols/lcmp.md): Light Client Cross-Chain Messaging Protocol employs blockchain consensus mechanisms and light clients as decentralized verifiers. This ensures the integrity and accuracy of message verification across different blockchains, fostering a secure and trustless environment for message passing.
  - [XCMP](./learn/messaging-protocols/xcmp.md): Developed by Polkadot, Cross-Consensus Message Passing facilitates seamless messaging between various parachains within the Polkadot network. Messages are exchanged directly by parachains, relayed and verified by the relay chain, exemplifying efficient inter-parachain communication and interoperability.

These implementations underscore Msgport's commitment to fostering interoperability, ensuring that assets and information can navigate the complex landscape of blockchain technology smoothly.

## Integration and Understanding
For developers and applications eager to leverage the power of Msgport, the journey begins with the [Msgport Workflow Documentation](./build/workflow.md) and a series of comprehensive [Tutorials](./build/tutorial/remix-demo.md). These resources are meticulously crafted to demystify the complexities of Msgport, offering a clear path to integration. From foundational knowledge to step-by-step guides, developers can expect a seamless onboarding experience, enabling them to harness the full potential of cross-chain messaging.