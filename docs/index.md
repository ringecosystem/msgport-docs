# What is Msgport?

Msgport gets its name from hubs of connectivity, such as airports, seaports, and spaceports, because it serves as a gateway for messages between different blockchain systems. By acting as a crucial hub, Msgport enables the connection of various blockchain systems with minimal changes to their underlying architecture. Specifically, Msgport defines a set of [essential interfaces](./build/interfaces.md) for cross-chain communication, including sending, receiving, and verifying messages. This is similar to a superclass or abstract class in programming, which outlines a template for functionality. Concrete implementations of Msgport, known as [messaging protocols](./learn/messaging-protocols/overview.md), may vary to accommodate the unique designs of different underlying blockchains. However, as long as an implementation adheres to the Msgport interfaces, it can be used interchangeably, making it easier for developers to create cross-chain decentralized applications.

## Key Features

### Flexible and Extensible
  
The [core interfaces](./build/interfaces.md) of Msgport are intentionally created with a broad and adaptable design to accommodate diverse implementations. With flexibility as a key principle, our roadmap includes various messaging protocols such as [ORMP](./learn/messaging-protocols/ormp.md), [LCMP](./learn/messaging-protocols/lcmp.md), and [XCMP](./learn/messaging-protocols/xcmp.md). While each protocol implements the foundational interfaces of Msgport, they leverage distinct cross-chain technologies to achieve interoperability. This design strategy ensures that the Msgport framework can support a wide array of cross-chain communication methods, allowing for robust and flexible blockchain messaging solutions.

### Developers Friendly

For application developers looking to enhance their dApps with cross-chain functionality, mastering the [core interfaces](./build/interfaces.md) for sending and receiving messages is essential. There's no need for in-depth knowledge of the underlying messaging infrastructure. Additionally, we offer various tools such as a message scanner and a cross-chain message fee calculator to streamline cross-chain activities.

### Decentralized and Open Source

All projects related to Msgport are open-source and governed by the members of RingDAO. Unlike many cross-chain solutions that utilize centralized trust models with histories of vulnerabilities to exploits and hacks, Msgport offers a more secure alternative, reducing the need for concern regarding such issues.