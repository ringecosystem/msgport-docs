# Glossary

## Port

The "port" is a fundamental concept in the msgport protocol, designating the access point where users or applications directly interact by sending or receiving messages. It is a pivotal element of the protocol's infrastructure. Each port is represented by an independent smart contract with a predefined address and can be uniquely identified by a combination of the chain_id and the port address.

## PortRegistry

Once the concept of a "port" is clear, it becomes easier to comprehend the role of the PortRegistry. This registry acts as a catalog for all ports that are recognized by a particular blockchain, and it is administered by a decentralized body known as **MsgDao**. Each port listed has to pass through a meticulous process of audit and registration, which is conducted through governance mechanisms. Upon successful registration, developers of decentralized applications (DApps) can tap into these verified ports to create sophisticated cross-chain applications. This decentralized registry process enhances the transparency and trustworthiness of the messaging infrastructure, empowering developers to integrate these ports into their applications with confidence. For more in-depth information, you're encouraged to review the [contract code](https://github.com/msgport/msgport/blob/main/src/PortRegistry.sol).

## MsgHash

MsgHash, as the only identifier for a cross-chain message, is returned if the message was successfully  sent in the source chain.