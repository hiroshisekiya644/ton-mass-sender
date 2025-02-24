# TON Transaction Manager Smart Contract

This is a TON smart contract designed for managing and processing transactions in chunks, with functionality to send transfers, manage excess funds, and track progress. The contract supports administrative control and handles large transaction sets efficiently by dividing them into manageable steps.

## Features

- **Chunked Transfer**: The contract sends coins in chunks, with a maximum size of 254 transactions per chunk.
- **Transaction Handling**: Handles a sequence of transfers, verifies messages, and processes them based on flags and state data.
- **Admin Control**: An administrator can control the process and receive excess funds when all transactions are completed.
- **Progress Tracking**: Tracks the completion of tasks and ensures that all funds are processed and sent to the correct addresses.
- **Excess Fund Management**: After processing, excess funds are returned to the administrator.

## Functions

- **`load_data()`**: Loads the current state of the contract, including the total amount of coins, the length of the transaction list, the current key, and more.
- **`save_data()`**: Saves the current state of the contract to storage.
- **`send_transfer(slice dest, int value)`**: Sends the specified amount of coins to the given destination address.
- **`send_excesses(slice dest)`**: Sends any remaining or excess funds to the administrator's address.
- **`recv_internal(int my_balance, int msg_value, cell in_msg_full, slice in_msg_body)`**: Processes incoming messages, handling transfers and other operations based on the state of the contract.
- **`has_finished()`**: Returns `true` if all transactions have been processed and no further action is needed.

## Usage

### Initiating the Contract

- When the contract is first deployed, it is in an uninitiated state. To initiate the contract, an administrator or authorized sender can send a message with enough funds to begin processing.
- The contract will then process transactions in chunks, sending coins to specified addresses and updating its state.

### Sending Transfers

- The contract automatically handles sending funds to destination addresses based on the stored messages. Each transfer is processed in a loop, and the contract will continue processing until all transactions are completed.

### Handling Excess Funds

- If the contract receives more funds than are needed for processing the transactions, the excess is returned to the administrator.

## Example Flow

1. Deploy the contract with an initial message from an authorized sender.
2. The contract loads the data, checks if the process has been initiated, and begins sending transfers in chunks.
3. After processing a chunk, the contract either saves its state and continues or completes the process by sending any remaining funds back to the admin.

## License

This contract is open-source and available under the [MIT License](LICENSE).
