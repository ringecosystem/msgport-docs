# Interfaces

## IMessagePort

The `IMessagePort` interface within the Msgport is crafted to simplify the complexities of underlying cross-chain messaging protocols for dApp developers. It offers a standardized interface to send cross-chain messages across various messaging protocols. The interface includes two critical functions:

- **`send()`**: Serves as the gateway for users or applications to dispatch cross-chain messages.
- **`fee()`**: Retrieves the necessary fee information for utilizing the **`send()`** function.

The Msgport layer accommodates a variety of messaging protocols that adhere to this interface, including ORMP, ICM, and XCMP, among others. The code for the interface furnishes detailed explanations of each function's use.

```solidity linenums="1" title="IMessagePort.sol"
pragma solidity ^0.8.0;

interface IMessagePort {
    error MessageFailure(bytes errorData);

    /// @dev Send a cross-chain message over the MessagePort.
    /// @notice Send a cross-chain message over the MessagePort.
    /// @param toChainId The message destination chain id. <https://eips.ethereum.org/EIPS/eip-155>
    /// @param toDapp The user application contract address which receive the message.
    /// @param message The calldata which encoded by ABI Encoding.
    /// @param params Extend parameters to adapt to different message protocols.
    function send(uint256 toChainId, address toDapp, bytes calldata message, bytes calldata params) external payable;

    /// @notice Get a quote in source native gas, for the amount that send() requires to pay for message delivery.
    ///         It should be noted that not all ports will implement this interface.
    /// @dev If the messaging protocol does not support on-chain fetch fee, then revert with "Unimplemented!".
    /// @param toChainId The message destination chain id. <https://eips.ethereum.org/EIPS/eip-155>
    /// @param toDapp The user application contract address which receive the message.
    /// @param message The calldata which encoded by ABI Encoding.
    /// @param params Extend parameters to adapt to different message protocols.
    function fee(uint256 toChainId, address toDapp, bytes calldata message, bytes calldata params)
        external
        view
        returns (uint256);
}
```

## IPortMetadata

The `IPortMetadata` interface in the Msgport framework is intended to handle essential information regarding each port. It mandates the inclusion of two specific types of data:

- **`name`**: Acts as a globally unique identifier for the port.
- **`uri`**: Serves as a reference to the location where detailed information about the port is stored, typically pointing to an IPFS link by default. For illustration, consider the [uri](https://ipfs.io/ipfs/bafybeid56lijczlbza2won2fhdjnf6qb7pmscgn7x3yr45kgvxvfjjh3pm) associated with the ORMP as an example.

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

## Application

The `Application` contract is typically extended by the receiving application on the destination chain. This extension allows the receiving application to incorporate additional validation checks for the information contained in cross-chain messages. To see this implementation in action, you can examine the provided [runnable demo](https://github.com/msgport/msgport-demo).

```solidity linenums="1" title="Application.sol"
pragma solidity ^0.8.17;

abstract contract Application {
    function _msgPort() internal view returns (address _port) {
        _port = msg.sender;
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