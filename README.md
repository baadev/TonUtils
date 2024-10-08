
# TonUtils

<img src="https://github.com/baadev/TonUtils/blob/main/assets/TonUtils.png?raw=true" width=500 />

[![Telegram Group][tgg-svg]][tg-group]
[![Telegram Chanel][tgc-svg]][tg-chanel]
![Licence](https://img.shields.io/github/license/baadev/TonUtils?style=flat-square)
![NPM Version](https://img.shields.io/npm/v/tonutils-ts?style=flat-square)
![NPM Downloads](https://img.shields.io/npm/dw/tonutils-ts?style=flat-square)
![Stars](https://img.shields.io/github/stars/baadev/TonUtils?style=flat-square)


<!-- TOC -->

- [TonUtils](#tonutils)
    - [Why TonUtils?](#why-tonutils)
    - [Features](#features)
    - [Getting Started](#getting-started)
        - [Prerequisites](#prerequisites)
        - [Installation](#installation)
        - [Usage](#usage)
    - [Features Description](#features-description)
        - [Wallet Creation](#wallet-creation)
        - [Public Address Utils](#public-address-utils)
    - [CLI commands](#cli-commands)
        - [Get Public Address by Mnemonic CLI](#get-public-address-by-mnemonic-cli)
        - [Wallet Management CLI](#wallet-management-cli)
        - [Create Activated Wallets with Balance](#create-activated-wallets-with-balance)
        - [Transaction Crafting](#transaction-crafting)
    - [How to Contribute](#how-to-contribute)
    - [License](#license)
    - [Support](#support)

<!-- /TOC -->
The TON blockchain can be tough, especially when you are new to TON. Suppose you are an NFT marketplace developer, trying to sell your collections, but you face confusing docs, random bugs, and unreliable APIs. Official tools often don't work well, making things even harder.

## Why TonUtils?

TON is the fastest blockchain, but high activity (such as major listings) can cause endpoints like TonApi or Public Light Servers to go down, leading to failed transactions and frustration. TonUtils helps solve these problems:

- **Minimal dependencies**: Simple tools for stable blockchain interaction.

- **Alternative light servers**: Automatically connects to other servers when the current one fails, keeping your project running smoothly.

- **Easy to use**: No need to spend weeks learning. TonUtils has ready-made solutions so you can start building right away.

Focus on your product, not on fighting with the blockchain.

## Features

- [**Wallet Creation**](#wallet-creation): Create secure wallets easily with simple code, no complex guides needed.
- [**Public Address Utils**](#public-address-utils): Quickly validate and manage wallet addresses, reducing errors and saving time.
- [**Transaction Crafting**](#transaction-crafting) (Coming soon): Effortlessly craft and send transactions, focus on your project, not on blockchain complexity.

## Getting Started

### Prerequisites

Before you begin, ensure you have installed:

- Node.js (v16.x or later)
- npm (v8.x or later)

### Installation

To get started with `TonUtils`, simply install it as a package using npm:

```bash
npm install tonutils-ts
```
### Usage

To use `tonutils-ts` in your project, import the necessary functions listed below (see [full list here](#features-description)). 

For example, to create a wallet, import the functions `createWallet` and `getPublicAddressByWallet` and implement them as shown below: 

```typescript
import { createWallet, getPublicAddressByWallet } from 'tonutils-ts';

async function getAddress(): Promise<void> {
  // Create a new wallet
  const { mnemonic, keyPair, generatedWallet } = await createWallet();

  // Get the public address of the created wallet
  const publicAddress = getPublicAddressByWallet(generatedWallet).toString();

  // Convert public and secret keys from Buffer to hex string
  const publicKey = keyPair.publicKey.toString('hex');
  const secretKey = keyPair.secretKey.toString('hex');

  // Log all useful information
  console.log('Wallet Address:', publicAddress);
  console.log('Mnemonic:', mnemonic);
  console.log('Public Key (Hex):', publicKey);
  console.log('Secret Key (Hex):', secretKey);
}

// Call the function
getAddress();
```

This will create a TON-wallet and display its address, mnemonic and key pair. Adjust the code to suit your project needs. For a full list of functions, see the list above.

## Features Description

### Wallet Creation

- **createWallet**
  - **Description**: Returns a new wallet.
  - **Example**:

    ```typescript
    const { mnemonic, keyPair, generatedWallet } = await createWallet();
    // Output: { mnemonic, keyPair, generatedWallet }
    ```

### Public Address Utils

- **getPublicAddressByWallet**
  - **Description**: Returns the public address associated with a given wallet.
  - **Example**:

    ```typescript
    const address = getPublicAddressByWallet(WalletContractV4);
    // Output: EQCgBnDa0omfX3xW-UoxUZNn0fdCm7YWnaj1dVjZz_EDpxZL
    ```

- **getPublicAddressByMnemonic**
  - **Description**: Retrieves the public address associated with a given mnemonic.
  - **Example**:

    ```typescript
    const address = await getPublicAddressByMnemonic("one two three...");
    // or
    const address = await getPublicAddressByMnemonic(["one", "two", "three"]);
    // Output: EQCgBnDa0omfX3xW-UoxUZNn0fdCm7YWnaj1dVjZz_EDpxZL
    ```

- **getBouncableAddress**
  - **Description**: Returns the bounceable address for the given address (non-bounceable).
  - **Example**:

    ```typescript
    const bouncableAddress = getBouncableAddress("UQ...");
    // Output: EQCgBnDa0omfX3xW-UoxUZNn0fdCm7YWnaj1dVjZz_EDpxZL
    ```

- **getNonBouncableAddress**
  - **Description**: Returns the non-bounceable address for the given address(bounceable).
  - **Example**:

    ```typescript
    const nonBouncableAddress = getNonBouncableAddress("EQ...");
    // Output: UQCgBnDa0omfX3xW-UoxUZNn0fdCm7YWnaj1dVjZz_EDp0uO
    ```

   ```
## CLI commands

These features are currently available only via the command line. Useful for creating and managing wallets, sending transactions, and testing addresses. 

To use them, clone the repository:

```bash
git clone https://github.com/baadev/tonutils-ts.git
cd TonUtils
```

Then, you can run the CLI tools below.

### Get Public Address by Mnemonic (CLI)

A CLI command to get a public address from a mnemonic. Helpful for quick wallet creation and testing addresses:

```BASH
npx ts-node ./modules/public.address.utils.ts -m 'abandon ability able about above absent absorb abstract absurd abuse access accident account accuse achieve acid acoustic acquire across act action actor actress actual adapt'

# Output:
Bounceable:  EQBDyloUvY25siQu-6XzJ4M7bBWUwUxGQ7BRC7oOB0R1JQ3Y
Not Bounceable:  UQBDyloUvY25siQu-6XzJ4M7bBWUwUxGQ7BRC7oOB0R1JVAd
```

### Wallet Management (CLI)

Wallet Management utility will allow you to generate specified amount of new wallets and send specified amount of TON in order to activate it in blockchain.

### Create Activated Wallets with Balance

1. Create a `.env` file in your project:

```BASH
   # Your wallet with funds
   FUNDING_SEED="one two three.."
   # optional, tonapi key
   TONAPI_KEY=""

   # For multisend
   # destination address / giver
   RECEIVER_ADDRESS="UQBFoaSviVB76rjARNE8mz5RJADALWEv_owkRhDNIs326obj" 
   # amount to be sent
   SENT_AMOUNT=0.01
   # 0 will send endlessly until manual stop
   SENT_COUNT=0
   # delay between sends
   SENT_DELAY=""
   # comment for transaction
   SENT_BODY="Any comment here"
```

2. Run the command:

```BASH
npx ts-node ./wallet_gen/multi_wallet_gen.ts --wallets 3 --popup 0.01
```

#### Arguments available

| Argument | Description | Example |
| ----------- | ---------| ----------- |
| `--wallets` | The number of wallets to be created | `--wallets 3`|
| `--popup`   | The amount of TON to be sent to each wallet | `--popup 0.01` |

See the [README](./wallet_gen/README.md) in the `wallet_gen directory` for more details.

-----------

### Transaction Crafting

The `wallet_popup` directory contains a script for sending TON cryptocurrency from a funding wallet to a list of other wallets.

Here’s how to set up `WALLET_LIST` in your `.env` and run the script from the command line:

1. Create a `.env` file in project root if it doesn’t exist.
2. Add `WALLET_LIST` as a JSON array of wallet addresses. Example:

```ini
   FUNDING_SEED="your mnemonic phrase here"
   SEND_VALUE="10"
   WALLET_LIST='["UQBFoaSviVB76rjARNE8mz5RJADALWEv_owkRhDNIs326obj", "EQCDeEg..."]'
```

3. Run the script using `ts-node`:

```bash
npx ts-node ./wallet-popup/multi_wallet_popup_ton.ts
```
The script will read the addresses from `WALLET_LIST` and send the specified amount of TON to each address.

See the [README](./wallet_popup/README.md) file in the `wallet_popup` directory for more details.

## How to Contribute

We welcome contributions from the community! If you're interested in helping improve TonUtils, here are ways you can contribute:

- **Reporting Bugs**: Open an issue to report a bug.
- **Suggesting Enhancements**: Have ideas on how to make TonUtils better? Open an issue with your suggestions.
- **Pull Requests**: Submit pull requests with bug fixes or new features.

## License

TonUtils is released under the [MIT License](LICENSE). Feel free to fork and modify it as per your needs.

## Support

If you need assistance or have any questions, feel free to open an issue or contact us directly:

[tgg-svg]: https://img.shields.io/badge/Telegram%20-Group-blue?style=flat-square
[tgc-svg]: https://img.shields.io/badge/Telegram%20-Chanel-blue?style=flat-square
[tg-group]: https://t.me/tonutils_ts
[tg-chanel]: https://t.me/tonutilsts
