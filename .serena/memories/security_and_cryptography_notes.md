# Security and Cryptography Implementation Notes

## Cryptographic Components

### Hash Functions
- **Poseidon2**: ZK-friendly hash function used for:
  - Commitment generation: `Poseidon2(nullifier, secret)`
  - Nullifier hashing: `Poseidon2(nullifier)`
  - Merkle tree operations
- **Keccak256**: Standard Ethereum hash function for non-ZK operations

### Zero-Knowledge Proof System
- **Backend**: UltraHonk proving system (Aztec/Barretenberg)
- **Circuit Language**: Noir for expressing ZK constraints
- **Proof Type**: Non-interactive proofs suitable for blockchain verification

## Security Mechanisms

### Double-Spending Prevention
- **Nullifier System**: Each commitment has a unique nullifier
- **Nullifier Hash Recording**: Spent nullifiers stored on-chain in `s_nullifierHashes` mapping
- **Validation**: Withdrawal attempts check nullifier hasn't been used

### Privacy Protection
- **Merkle Tree Anonymity**: Deposits mixed in tree structure
- **Zero-Knowledge Proofs**: Prove membership without revealing which leaf
- **Commitment Hiding**: Secret + nullifier hidden in Poseidon hash

### Smart Contract Security
- **ReentrancyGuard**: OpenZeppelin protection against reentrancy attacks
- **Fixed Denomination**: Prevents amount-based correlation (0.001 ETH)
- **Input Validation**: Proper error handling for invalid inputs

## ZK Circuit Logic

### Public Inputs (Verifiable On-Chain)
- `root`: Current Merkle tree root
- `nullifier_hash`: Hash of the nullifier being spent  
- `recipient`: Withdrawal destination address

### Private Inputs (Hidden from Verifier)
- `nullifier`: Secret nullifier value
- `secret`: Secret value used in commitment
- `merkle_proof`: Proof path from leaf to root (20 levels)
- `is_even`: Boolean array indicating left/right path directions

### Circuit Constraints
1. **Commitment Verification**: `commitment = Poseidon2(nullifier, secret)`
2. **Nullifier Verification**: `nullifier_hash = Poseidon2(nullifier)`
3. **Merkle Proof Verification**: `computed_root = merkle_tree_root(commitment, proof, path)`
4. **Root Matching**: `computed_root == root`

## Known Limitations (Educational Context)

### Security Disclaimers
- **Unaudited Code**: No professional security audit performed
- **Educational Purpose**: Not suitable for mainnet deployment
- **Simplified Implementation**: Some production optimizations omitted

### Potential Attack Vectors (Educational Analysis)
- **Trusted Setup**: UltraHonk requires proper ceremony (handled by Aztec)
- **Circuit Bugs**: Logic errors in ZK circuits can be catastrophic
- **Implementation Bugs**: Smart contract vulnerabilities
- **Front-running**: MEV considerations for deposit/withdrawal timing

## Best Practices Demonstrated

### Cryptographic Hygiene
- Proper field element handling for BN254 curve
- Consistent hash function usage (Poseidon2 for ZK, Keccak for Ethereum)
- Secure randomness requirements for secret/nullifier generation

### Smart Contract Patterns
- Immutable verifier contract reference
- Event emission for off-chain indexing
- Clear error messages with custom error types
- Modifier usage for access control and validation