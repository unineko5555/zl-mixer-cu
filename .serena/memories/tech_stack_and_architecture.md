# Tech Stack and Architecture

## Core Technologies

### Smart Contracts (Solidity)
- **Foundry Framework**: Used for Solidity development, testing, and deployment
- **Solidity Version**: ^0.8.24
- **Key Libraries**:
  - OpenZeppelin Contracts (ReentrancyGuard)
  - Poseidon2 hasher for efficient ZK-friendly hashing
  - Custom Incremental Merkle Tree implementation

### Zero-Knowledge Circuits (Noir)
- **Noir Language**: Used for writing ZK circuits
- **Barretenberg (bb.js)**: Aztec's proving system for proof generation
- **UltraHonk Backend**: Advanced proving system for efficient proofs
- **Circuit Logic**: Verifies Merkle tree membership and nullifier validity

### JavaScript/TypeScript Tooling
- **Node.js**: v20.18.0 runtime environment  
- **NPM**: v10.8.2 package manager
- **Key Dependencies**:
  - `@aztec/bb.js`: Barretenberg proving system
  - `@noir-lang/noir_js`: Noir JavaScript bindings
  - `ethers`: Ethereum interaction library
  - `msgpackr`: Message pack serialization

## Architecture Components

### 1. Contracts Layer (`contracts/`)
- `Mixer.sol`: Main contract handling deposits/withdrawals
- `IncrementalMerkleTree.sol`: Merkle tree implementation  
- `Verifier.sol`: Auto-generated ZK proof verifier

### 2. Circuits Layer (`circuits/`)
- `main.nr`: Core ZK circuit logic
- `merkle_tree.nr`: Merkle tree proof utilities
- Proves: commitment validity, nullifier correctness, Merkle membership

### 3. JavaScript Scripts (`contracts/js-scripts/`)
- `generateProof.ts`: ZK proof generation
- `generateCommitment.ts`: Commitment creation
- `merkleTree.js`: Off-chain Merkle tree utilities

## Development Tools
- **Foundry**: Smart contract development framework
- **Nargo**: Noir project manager and compiler
- **bb**: Barretenberg CLI for proof system operations