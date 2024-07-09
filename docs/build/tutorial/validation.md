# Validating Received Messages

For the application that receive the cross-chain messages, it's important to validate it before processing it, such as validate the message comes from the right source chain or validate the message comes from the right application in the source chain. Adding those validation for your application can avoid the contract state been 
updated in unexpected ways.

The basic validation material is provided by the Msgport [Application](../interfaces.md#application) contract. It provide the following functions:

* `_msgPort()`: Return the `msg.sender` of the received message, normally it should be the address of the corresponding msgport.
* ` _messageId()`: Return the message id of the received message.
* `_chainId()`: Return the chain id of the source chain. It's recommended to validate it by default.
* `_xmsgSender()`: Return the application address of the source chain, where the received message comes from. It's recommended to validate it by default.

Since we recommend the application who receive the message should extend the `Application` contract, so that can validate message using these material directly. See the [examples](https://github.com/msgport/msgport-examples) if you want to know more.  