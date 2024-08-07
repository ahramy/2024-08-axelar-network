# Interchain Token Service Hub

## Overview

The Interchain Token Service (ITS) Hub contract is a crucial component of a cross-chain ITS protocol. It facilitates the transfer of tokens between different blockchains, manages token deployments, and maintains balance integrity across chains. It connects to ITS edge contracts on different chains (e.g. EVM ITS [contract](https://github.com/axelarnetwork/interchain-token-service)).

## Key Components

1. **ITS Message Processing**: Processes incoming ITS messages from trusted sources.
2. **Balance Tracking**: Ensures accurate token balances are maintained during cross-chain operations.
3. **ITS Address Registry**: Tracks the trusted ITS address for each chain for routing.

### Balance Tracking

ITS Hub maintains balance invariants for native interchain tokens for every chain they're deployed to. This helps isolate the security risk between chains. A compromise on one chain can only affect the token balance that was moved to that chain in the worst case. For e.g. say if USDC was deployed from Ethereum to Solana via the ITS Hub, and 10M USDC was moved to Solana (in total). If there's a compromise on Solana, an attacker can only withdraw at most 10M USDC back to Ethereum (and not all the USDC that was locked on the Ethereum ITS contract).

### Cross-chain messaging

The ITS Hub makes use of the Axelarnet gateway contract to facilitate 

## Build

Ensure that `rust >= 1.78` is installed.

```bash
# Install protoc
brew install protobuf

# Install rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install rust 1.78.0
rustup default 1.78.0

# Add wasm toolchain
rustup target add wasm32-unknown-unknown

# Build the contract
cargo wasm

# Run tests
cargo test
```
