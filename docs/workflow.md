# Msgport Workflow

Within the diverse landscape of today's blockchain technology, each blockchain possesses its unique architecture and set of features. This diversity often results in cross-chain messaging protocols that are multifaceted, involving numerous roles, and can appear daunting to comprehend in terms of message transmission and execution across different chains.

For dApp developers looking to incorporate these cross-chain messaging protocols into their applications, a solid grasp of the underlying mechanics is crucial. This knowledge becomes particularly important when encountering unexpected issues during development, which can often be resolved with an awareness of how these complex systems operate.

The purpose of this page is to provide you with a clear understanding of how the Msgport and [ORMP](../msgport/messaging-protocols/ormp.md) messaging protocols facilitate cross-chain interactions. By breaking down these protocols, we aim to demystify the process, making it more accessible for developers needing to integrate cross-chain functionality into their projects.

## Verifying network support

Before diving into the integration of the Darwinia Msgport protocol, the initial and critical step is to confirm whether the [Darwinia Msgport supports the network](../msgport/networks.md) you intend to use. If the network is supported, the integration process simplifies significantly, and your focus shifts to learning how to utilize the Msgport contract's capabilities for sending and receiving cross-chain messages. Typically, getting accustomed to these functions could take as little as half a day.

On the other hand, if the network is not currently supported, your first course of action should be to [reach out to the Darwinia team](https://t.me/DarwiniaNetwork) to inquire about potential future support. Alternatively, if you prefer a more hands-on approach, you have the option to develop and deploy the necessary contracts yourself and register them with the PortRegister.

## Messaging workflow

!!! note
    For those interested in gaining a more in-depth understanding of how Msgport operates, there is a [runnable demo available](https://github.com/darwinia-network/msgport-demo) for reference. This can be a valuable resource to see the message port in action.

### Find the Port Contract Address

After verifying that the Darwinia Msgport aligns with your project's objectives, the subsequent step is to locate the port contract address. If you're unfamiliar with the concept of a port contract, you can learn more by visiting **[this link](../msgport/glossary.md#port)**. There are two methods to acquire the appropriate port address:

1. Check the [Supported Networks list](../msgport/networks.md) for the endpoint. The port addresses are standardized across all networks to enhance clarity and ease of use, and you can easily find this information there.
2. Use the  `get(uint256 chainId, string calldata name)` function to consult the [PortRegistry](../msgport/glossary.md#portregistry) contract. By supplying the chainId and the specific protocol name, you can retrieve the endpoint for the target network. The PortRegistry contract is a detailed ledger of all registered port contracts, providing a trustworthy reference point.

### Build the receiver application in the target chain

Integrating Msgport into the receiver application on the target chain is a straightforward process. Simply extend your contract to implement the [Application](../msgport/interfaces.md#application) interface, and then incorporate your business logic into the contract as usual. Below is a demo code snippet for your reference.

```solidity linenums="1" title="TestReceiver.sol"
pragma solidity ^0.8.17;

import "lib/darwinia-msgport/src/user/Application.sol";

contract TestReceiver is Application {
    event DappMessageRecv(uint256 fromChainId, address fromDapp, address localPort, uint256 num);

    // local port address
    address public immutable PORT;

    uint256 public sum;

    constructor(address port) {
        PORT = port;
        REMOTE_DAPP = remoteDapp;
    }

    /// @notice You could check the fromDapp address or messagePort address.
    function addReceiveNum(uint256 num) external {
        uint256 fromChainId = _fromChainId();
        address fromDapp = _xmsgSender();
        address localPort = _msgPort();
        require(localPort == PORT);
        sum += num;
        emit DappMessageRecv(fromChainId, fromDapp, localPort, num);
    }
}
```

The **`TestReceiver`** contains a public **`num`** variable and provides an **`addReceiveNum`** function that can be used to increment this value. Next, we will outline the steps for activating this function through Msgport to increase the **`num`** value from a different blockchain.

### Setting Up the Message Content

Prior to initiating a cross chain transaction, it's essential to determine the content of the message, which encompasses several key fields required for the message transmission process:

- **`toChainId`**: This is the identifier of the destination chain where the message will be sent.
- **`toDapp`**: This refers to the contract address of the user application that will receive the message on the destination chain, in this example, the `TestReceiver` address.
- **`message`**: This is the ABI-encoded call data that contains the information or instructions for the receiving contract, in this example, `bytes memory message = abi.encodeCall(TestReceiver.addReceiveNum, 10);`

### Estimate message fee in native token

Message fees play a critical role in the design of a cross-chain messaging protocol. They represent not just the cost of incorporating cross-chain functionality into your applications, but they also impact the user experience of your application. A thoughtfully constructed fee mechanism is crucial for success.

The fee structure for Msgport is implemented through the [Msgport API](https://github.com/darwinia-network/darwinia-msgport-api). For detailed information on the fee design, please refer to the [Msgport API Document](../msgport/api.md). Additionally, you can explore the [Pangolin > Sepolia Message Demo](../msgport/tutorial/script-demo.md) to see how the fee mechanism is applied in practice.

### Send message in source chain application

With the preliminary setup out of the way, you're all set to send your cross-chain message. The process is quite simple—refer to the demo code below for guidance.

```solidity linenums="1" title="TestSender.sol"
pragma solidity ^0.8.17;

import "lib/darwinia-msgport/src/interfaces/IMessagePort.sol";

contract TestSender {
    event DappMessageSent(address localPort, bytes message);

    address public immutable PORT;

    constructor(address port) {
        PORT = port;
    }

    function send(uint256 toChainId, address toDapp, bytes calldata message, bytes calldata params) external payable {
        **IMessagePort(PORT).send{value: msg.value}(toChainId, toDapp, message, params);**
        emit DappMessageSent(PORT, message);
    }
}
```

The line **`IMessagePort(PORT).send{value: msg.value}(toChainId, toDapp, message, params);`** initiates the cross-chain messaging process. Here's a breakdown of its components:

- **`PORT`**: This is the port contract address you've located in the previous "Find the Port Contract Address" step.
- **`toChainId`**, **`toDapp`**, and **`message`**: These are the variables you've established while preparing the message content, the
- **`msg.value`** and **`params`**: These represent the estimated message fee in the native token, as determined in the "Estimate Message Fee" step.

By invoking the **`send`** function within the TestSender demo with the parameters you've prepared, your message is transmitted to the specified **`toChainId`** and will be executed by the **`toDapp`** contract on the destination chain. And that's the entire process.

### Monitor the message status

The delivery and execution of your message on the target chain may take approximately 5 to 15 minutes. To monitor the status of your message, we offer a scanning tool [Darwinia Messages Explorer](https://msgscan.darwinia.network/) that allows you to track the progress using your sent message's transaction hash or the message hash itself.

