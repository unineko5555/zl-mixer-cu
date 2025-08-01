# ZK Mixer App - Project Overview

## Purpose
The ZK Mixer App is an educational implementation of a privacy-preserving cryptocurrency mixer, inspired by Tornado Cash but simplified for learning purposes. It allows users to deposit assets and later withdraw them without linking the withdrawal to the deposit, providing transaction privacy through zero-knowledge proofs.

## Key Features
- **Anonymous Deposits/Withdrawals**: Users can deposit ETH and withdraw it to a different address without revealing the connection
- **Merkle Tree Privacy**: Uses an incremental Merkle tree to maintain anonymity sets
- **Zero-Knowledge Proofs**: Utilizes Noir language and bb.js for ZK proof generation and verification
- **Double-Spending Prevention**: Implements nullifiers to prevent reuse of the same commitment

## How It Works
1. **Deposit Phase**: Users create a commitment (hash of secret + nullifier) and deposit fixed ETH amount (0.001 ETH)
2. **Merkle Tree**: Commitments are stored in an on-chain Merkle tree, root updates with each deposit
3. **Withdrawal Phase**: Users prove knowledge of a valid commitment in the tree without revealing which one
4. **Nullifier System**: Prevents double-spending by recording nullifier hashes on-chain

## Educational Context
⚠️ **Important**: This is an educational adaptation developed by Cyfrin for blockchain development courses. It is unaudited and should never be deployed to mainnet or used with real funds.