# Integrate Msgport into Your Application

!!! note
    It's recommended to understand the [core interface](./interfaces.md) of the Msgport before diving into the integration process.

!!! note
    For those interested in gaining a more in-depth understanding of how Msgport operates, there are some [runnable examples available](https://github.com/msgport/msgport-examples) for reference. This can be a valuable resource to see the Msgport in action.

The purpose of this page is to provide a step-by-step guide on how to integrate the Msgport into your application and the concrete steps to follow in the process. By following these instructions, you can quickly and easily integrate Msgport into your application and unlock the potential of cross-chain messaging.

The guide is divided into the following steps:

1. [Check Network Support](#check-network-support)
2. [Find Port Contract Address](#find-port-contract-address)
3. [Extend Target Chain Receiver](#extend-target-chain-receiver)
4. [Prepare the Message Payload](#prepare-the-message-payload)
4. [Estimate Message Fee](#estimate-message-fee)
5. [Send Message](#send-message)
6. [Track the Message Status](#track-the-message-status)

## Check Network Support

Before diving into the integration of the Msgport, the initial and critical step is to confirm whether the [Msgport supports the network](./networks.md) you intend to use. If the network is supported, the integration process simplifies significantly, and your focus shifts to learning how to utilize the Msgport contract's capabilities for sending and receiving cross-chain messages. Typically, getting accustomed to these functions could take as little as half a day.

On the other hand, if the network is not currently supported, your first course of action should be to Msgport team to inquire about potential future support. Alternatively, if you prefer a more hands-on approach, you have the option to develop and deploy the necessary contracts yourself and register them with the PortRegister.

## Find Port Contract Address

After verifying that the Msgport aligns with your project's objectives, the subsequent step is to locate the port contract address. If you're unfamiliar with the concept of a port contract, you can learn more by visiting **[this link](../learn/glossary.md#port)**. There are two methods to acquire the appropriate port address:

1. Check the [Supported Networks list](./networks.md) for the endpoint. The port addresses are standardized across all networks to enhance clarity and ease of use, and you can easily find this information there.
2. Use the  `get(uint256 chainId, string calldata name)` function to consult the [PortRegistry](../learn/glossary.md#portregistry) contract. By supplying the chainId and the specific protocol name, you can retrieve the endpoint for the target network. The PortRegistry contract is a detailed ledger of all registered port contracts, providing a trustworthy reference point.

## Extend Target Chain Receiver

Integrating Msgport into the receiver application on the target chain is a straightforward process. Simply extend your contract to implement the [Application](./interfaces.md#application) interface, and then incorporate your business logic into the contract as usual. Below is a demo code snippet for your reference.

```solidity linenums="1" title="ExampleReceiver.sol"
pragma solidity ^0.8.17;

import "msgport/user/Application.sol";

contract ExampleReceiver is Application {
    event DappMessageRecv(uint256 fromChainId, address fromDapp, address localPort, uint256 num);

    address public immutable PORT;

    uint256 public sum;

    constructor(address port) {
        PORT = port;
        REMOTE_DAPP = remoteDapp;
    }

    function addReceiveNum(uint256 num) external {
        // optional validation
        uint256 fromChainId = _fromChainId();
        address fromDapp = _xmsgSender();
        address localPort = _msgPort();
        require(localPort == PORT);
        
        sum += num;

        emit DappMessageRecv(fromChainId, fromDapp, localPort, num);
    }
}
```

The **`ExampleReceiver`** contains a public **`sum`** variable and provides an **`addReceiveNum`** function that can be used to increment this value. Next, we will outline the steps for activating this function through Msgport to increase the **`sum`** value from a different blockchain.

## Prepare the Message Payload

Prior to initiating a cross chain transaction, it's essential to determine the content of the message, which encompasses several key fields required for the message transmission process:

- **`toChainId`**: This is the identifier of the destination chain where the message will be sent.
- **`toDapp`**: This refers to the contract address of the user application that will receive the message on the destination chain, in this example, the `ExampleReceiver` address.
- **`message`**: This is the ABI-encoded call data that contains the information or instructions for the receiving contract, in this example, `bytes memory message = abi.encodeCall(ExampleReceiver.addReceiveNum, 10);`

## Estimate Message Fee

Message fees play a critical role in the design of a cross-chain messaging protocol. They represent not just the cost of incorporating cross-chain functionality into your applications, but they also impact the user experience of your application. A thoughtfully constructed fee mechanism is crucial for success.

The cross-chain estimated fee can be obtained through the [Msgport API](https://apidog.msgport.xyz/). For more information on how to use the API, refer to the [documentation](./api.md). Additionally, you can find examples of how to fetch the estimated fee via script in the [Msgport Examples](https://github.com/msgport/msgport-examples) repository.

## Send Message

With the preliminary setup out of the way, you're all set to send your cross-chain message. The process is quite simple, and refer to the demo code below for guidance.

```solidity linenums="1" title="ExampleSender.sol"
pragma solidity ^0.8.17;

import "msgport/interfaces/IMessagePort.sol";

contract ExampleSender {
    event DappMessageSent(address localPort, bytes message);

    address public immutable PORT;

    constructor(address port) {
        PORT = port;
    }

    function send(uint256 toChainId, address toDapp, bytes calldata message, bytes calldata params) external payable {
        IMessagePort(PORT).send{value: msg.value}(toChainId, toDapp, message, params);

        emit DappMessageSent(PORT, message);
    }
}
```

The line **`IMessagePort(PORT).send{value: msg.value}(toChainId, toDapp, message, params);`** initiates the cross-chain messaging process. Here's a breakdown of its components:

- **`PORT`**: This is the port contract address you've located in the previous [Find Port Contract Address](#find-port-contract-address) step.
- **`toChainId`**, **`toDapp`**, and **`message`**: These are the variables you've established while [Prepare the Message Payload](#prepare-the-message-payload).
- **`msg.value`** and **`params`**: These represent the estimated message fee in the native token, as determined in the [Estimate Message Fee](#estimate-message-fee) step.

By invoking the **`send`** function within the ExampleSender demo with the parameters you've prepared, your message is transmitted to the specified **`toChainId`** and will be executed by the **`toDapp`** contract on the destination chain. And that's the entire process.

## Track the Message Status

The delivery and execution of your message on the target chain may take approximately 5 minutes. To monitor the status of your message, we offer a scanning tool [Messages Scan](https://scan.msgport.xyz/) that allows you to track the progress using your sent message's transaction hash or the message id.
