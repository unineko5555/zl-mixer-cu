# Codebase Structure

## Root Directory Structure
```
zk-mixer-cu/
├── circuits/                 # Zero-knowledge circuits (Noir)
├── contracts/               # Smart contracts (Solidity + Foundry)
├── .gitmodules             # Git submodules configuration
├── .gitignore              # Git ignore patterns
├── package.json            # Node.js dependencies
├── package-lock.json       # Locked dependency versions
└── README.md               # Project documentation
```

## Circuits Directory (`circuits/`)
```
circuits/
├── src/
│   ├── main.nr             # Main ZK circuit logic
│   └── merkle_tree.nr      # Merkle tree utilities
├── Nargo.toml              # Noir project configuration
└── target/                 # Compiled circuit artifacts (generated)
    ├── circuits.json       # Compiled circuit
    ├── vk                  # Verification key
    └── Verifier.sol        # Generated Solidity verifier
```

## Contracts Directory (`contracts/`)
```
contracts/
├── src/
│   ├── Mixer.sol           # Main mixer contract
│   ├── IncrementalMerkleTree.sol  # Merkle tree implementation
│   └── Verifier.sol        # ZK proof verifier (auto-generated)
├── test/
│   └── Mixer.t.sol         # Foundry test suite
├── js-scripts/
│   ├── generateProof.ts    # ZK proof generation script
│   ├── generateCommitment.ts # Commitment generation script
│   └── merkleTree.js       # Off-chain Merkle tree utilities
├── lib/                    # Foundry dependencies (git submodules)
│   ├── forge-std/          # Foundry standard library
│   ├── openzeppelin-contracts/ # OpenZeppelin contracts
│   └── poseidon2-evm/      # Poseidon hash implementation
├── .github/workflows/
│   └── test.yml           # CI/CD pipeline configuration
├── foundry.toml           # Foundry configuration
├── .gitmodules           # Contracts git submodules
└── .gitignore           # Contracts git ignore patterns
```

## Key File Responsibilities

### Core Smart Contracts
- **`Mixer.sol`**: Main contract handling deposits, withdrawals, and proof verification
- **`IncrementalMerkleTree.sol`**: Base contract for Merkle tree operations and Poseidon hashing
- **`Verifier.sol`**: Auto-generated contract for ZK proof verification (regenerated when circuits change)

### Zero-Knowledge Circuits  
- **`main.nr`**: Core circuit proving commitment validity, nullifier correctness, and Merkle tree membership
- **`merkle_tree.nr`**: Utilities for computing Merkle tree roots within the circuit

### Testing Infrastructure
- **`Mixer.t.sol`**: Comprehensive Foundry tests covering deposit/withdrawal flows
- **`generateProof.ts`**: Off-chain proof generation for testing
- **`merkleTree.js`**: JavaScript utilities for Merkle tree operations

### Configuration Files
- **`foundry.toml`**: Foundry configuration with remappings and gas limits
- **`Nargo.toml`**: Noir project configuration for circuit compilation
- **`package.json`**: Node.js dependencies for JavaScript tooling

## Dependencies and Libraries

### Foundry Libraries (Git Submodules)
- **OpenZeppelin**: Standard smart contract security patterns
- **Poseidon2-EVM**: ZK-friendly hash function implementation
- **Forge-Std**: Foundry testing utilities

### NPM Dependencies
- **Barretenberg (`@aztec/bb.js`)**: Proving system for ZK proofs
- **Noir (`@noir-lang/noir_js`)**: JavaScript bindings for Noir circuits
- **Ethers**: Ethereum blockchain interaction