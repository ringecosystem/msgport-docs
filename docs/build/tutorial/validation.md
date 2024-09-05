# Validating Received Messages

For the application that receives cross-chain messages, it is crucial to validate the received messages to ensure they come from the intended source chain and application. Adding these validations to your application can help prevent unexpected changes to the contract's state.

The basic validation materials are provided by the Msgport [Application](../interfaces.md#application) contract. It provides the following functions:

* `_msgPort()`: Returns the `msg.sender` of the received message, typically the address of the corresponding port.
* `_messageId()`: Returns the message ID of the received message.
* `_chainId()`: Returns the chain ID of the source chain. It is recommended to validate it by default.
* `_xmsgSender()`: Returns the application address in the source chain from which the received message originates. It is recommended to validate it by default.

Since it is recommended that the application receiving the message extends the `Application` contract, these validation materials can be used directly by the application. You can refer to the [examples](https://github.com/ringecosystem/msgport-examples) for more information.