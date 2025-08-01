# Essential Development Commands

## Project Setup
```bash
# Install dependencies
npm install && cd contracts && forge install

# Navigate back to root
cd ..
```

## Smart Contract Development (Foundry)

### Core Commands
```bash
# Navigate to contracts directory first
cd contracts

# Build contracts
forge build

# Run tests with verbose output
forge test -vvv

# Format Solidity code
forge fmt

# Check formatting without changes
forge fmt --check

# Build with contract size information
forge build --sizes
```

### Environment Profile
- **Default Profile**: For local development
- **CI Profile**: Used in GitHub Actions (`FOUNDRY_PROFILE=ci`)

## Zero-Knowledge Circuit Development (Noir)

### Core Commands
```bash
# Navigate to circuits directory first
cd circuits

# Compile the circuit
nargo compile

# Check circuit syntax
nargo check
```

### Verifier Generation (After Circuit Changes)
```bash
# 1. Compile circuit (from circuits/)
nargo compile

# 2. Generate verification key
bb write_vk --oracle_hash keccak -b ./target/circuits.json -o ./target

# 3. Generate Solidity verifier
bb write_solidity_verifier -k ./target/vk -o ./target/Verifier.sol

# 4. Replace old verifier in contracts/src/
# Manual step: Copy new Verifier.sol to contracts/src/
```

## JavaScript Tooling

### Proof Generation Scripts
```bash
# Generate ZK proofs (from contracts/js-scripts/)
npx ts-node generateProof.ts [arguments]

# Generate commitments
npx ts-node generateCommitment.ts [arguments]
```

## Development Workflow Commands

### Version Checking
```bash
# Check tool versions
forge --version
nargo --version
bb --version
node --version
npm --version
```

### System Tools (macOS Darwin)
- **Git**: `/usr/bin/git` - Standard git operations
- **Find**: `find` - File searching
- **Grep**: `grep` - Text searching  
- **ls**: `ls` - Directory listing
- **cd**: `cd` - Directory navigation

## CI/CD Pipeline
GitHub Actions automatically runs:
1. `forge fmt --check` - Code formatting verification
2. `forge build --sizes` - Contract compilation with size info
3. `forge test -vvv` - Comprehensive test suite