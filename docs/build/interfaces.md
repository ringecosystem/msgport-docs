# Core Interfaces

This table summarizes the core interfaces that may be used in the application's Msgport integration. These interfaces are straightforward and easy to understand. Let's dive in!

| Interface | Description |
| --- | --- |
| **[IMessagePort](./interfaces.md#imessageport)** | This serves as the endpoint for cross-chain messages in the source chain. |
| **[Application](./interfaces.md#application)** | This is utilized in the receiving application on the destination chain to extract crucial information for validating messages before execution. |
| **[IPortMetadata](./interfaces.md#imessageport)** | This is utilized in the source chain to retrieve the message port information, such as fee, metadata, before sending a message. |

## Interfaces Introduction

### IMessagePort

The `IMessagePort` interface within the Msgport is crafted to simplify the complexities of underlying cross-chain messaging protocols for dApp developers. It offers a standardized interface to send cross-chain messages across various messaging protocols. The interface includes two critical functions:

- **`send()`**: Serves as the gateway for users or applications to send a cross-chain message. It returns a msgId, which is the identifier of the message and can be used to track the message status.
- **`fee()`**: Retrieves the necessary fee information for utilizing the **`send()`** function.

The Msgport layer accommodates a variety of messaging protocols that adhere to this interface, including ORMP, ICMP, and XCMP, among others. The code for the interface furnishes detailed explanations of each function's use.

```solidity linenums="1" title="IMessagePort.sol"
pragma solidity ^0.8.0;

interface IMessagePort {
    event MessageSent(
        bytes32 indexed msgId, address fromDapp, uint256 toChainId, address toDapp, bytes message, bytes params
    );
    event MessageRecv(bytes32 indexed msgId, bool result, bytes returnData);

    /// @dev Send a cross-chain message over the MessagePort.
    /// @notice Send a cross-chain message over the MessagePort.
    /// @param toChainId The message destination chain id. <https://eips.ethereum.org/EIPS/eip-155>
    /// @param toDapp The user application contract address which receive the message.
    /// @param message The calldata which encoded by ABI Encoding.
    /// @param params Extend parameters to adapt to different message protocols.
    /// @return msgId Return the ID of message.
    function send(uint256 toChainId, address toDapp, bytes calldata message, bytes calldata params)
        external
        payable
        returns (bytes32 msgId);

    /// @notice Get a quote in source native gas, for the amount that send() requires to pay for message delivery.
    ///         It should be noted that not all ports will implement this interface.
    /// @dev If the messaging protocol does not support on-chain fetch fee, then revert with "Unimplemented!".
    /// @param toChainId The message destination chain id. <https://eips.ethereum.org/EIPS/eip-155>
    /// @param fromDapp The user application contract address which send the message.
    /// @param toDapp The user application contract address which receive the message.
    /// @param message The calldata which encoded by ABI Encoding.
    /// @param params Extend parameters to adapt to different message protocols.
    function fee(uint256 toChainId, address fromDapp, address toDapp, bytes calldata message, bytes calldata params)
        external
        view
        returns (uint256);
}
```

### Application

The `Application` contract is typically extended by the receiving application on the destination chain. This extension allows the receiving application to incorporate additional validation checks for the information contained in cross-chain messages. To see this implementation in action, you can examine the provided [runnable examples](https://github.com/msgport/msgport-examples).

```solidity linenums="1" title="Application.sol"
pragma solidity ^0.8.17;

abstract contract Application {
    function _msgPort() internal view returns (address _port) {
        _port = msg.sender;
    }

    function _messageId() internal pure returns (bytes32 _msgDataMessageId) {
        require(msg.data.length >= 84, "!messageId");
        assembly {
            _msgDataMessageId := calldataload(sub(calldatasize(), 84))
        }
    }

    /// @notice The cross-chain message source chainId
    function _fromChainId() internal pure returns (uint256 _msgDataFromChainId) {
        require(msg.data.length >= 52, "!fromChainId");
        assembly {
            _msgDataFromChainId := calldataload(sub(calldatasize(), 52))
        }
    }

    /// @notice Get the source chain fromDapp address.
    function _xmsgSender() internal pure returns (address payable _from) {
        require(msg.data.length >= 20, "!fromDapp");
        assembly {
            _from := shr(96, calldataload(sub(calldatasize(), 20)))
        }
    }
}
```

### IPortMetadata

The `IPortMetadata` interface in the Msgport framework is intended to handle essential information regarding each port. It mandates the inclusion of two specific types of data:

- **`name`**: Acts as a globally unique identifier for the port.
- **`uri`**: Serves as a reference to the location where detailed information about the port is stored, typically pointing to an IPFS link by default.

This interface enables the Msgport to maintain vital information that applications may need in order to utilize the ports effectively.

```solidity linenums="1" title="IPortMetadata.sol"
pragma solidity ^0.8.0;

interface IPortMetadata {
    event URI(string uri);

    /// @notice Get the port name, it's globally unique and immutable.
    /// @return The MessagePort name.
    function name() external view returns (string memory);

    /// @return The port metadata uri.
    function uri() external view returns (string memory);
}
```

