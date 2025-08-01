# Task Completion Checklist

## After Making Code Changes

### 1. Smart Contract Changes
When modifying Solidity contracts:

```bash
cd contracts

# Format code
forge fmt

# Build to check compilation
forge build

# Run comprehensive tests
forge test -vvv

# Verify contract sizes haven't grown too large
forge build --sizes
```

### 2. Circuit Changes  
When modifying Noir circuits:

```bash
cd circuits

# Check circuit syntax
nargo check

# Compile circuit
nargo compile

# If circuit logic changed, regenerate verifier:
bb write_vk --oracle_hash keccak -b ./target/circuits.json -o ./target
bb write_solidity_verifier -k ./target/vk -o ./target/Verifier.sol

# Copy new Verifier.sol to contracts/src/ (manual step)
```

### 3. Integration Testing
After circuit changes affecting the verifier:

```bash
cd contracts

# Rebuild contracts with new verifier
forge build

# Run full test suite to ensure integration works
forge test -vvv
```

### 4. Code Quality Checks
Before considering a task complete:

- [ ] **Formatting**: All Solidity code properly formatted (`forge fmt`)
- [ ] **Compilation**: All contracts compile without warnings (`forge build`)
- [ ] **Tests**: All existing tests pass (`forge test -vvv`) 
- [ ] **Circuit Compilation**: Circuits compile without errors (`nargo check`, `nargo compile`)
- [ ] **Integration**: If verifier was regenerated, contracts integrate properly
- [ ] **Documentation**: Code includes appropriate NatSpec and comments
- [ ] **Security**: No obvious security vulnerabilities introduced

### 5. Git Workflow
```bash
# Stage changes
git add .

# Commit with descriptive message
git commit -m "descriptive message"

# Push if working on a branch
git push origin branch-name
```

## Important Notes

- **Never deploy to mainnet**: This is educational code only
- **Test thoroughly**: ZK circuits and cryptographic code requires careful testing
- **Verify proofs**: When changing circuits, always test the full proof generation and verification flow
- **Performance**: Monitor gas costs and proof generation time for efficiency