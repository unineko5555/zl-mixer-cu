# Code Style and Conventions

## Solidity Conventions

### File Organization
- **SPDX License**: MIT license identifier at file top
- **Pragma Version**: `pragma solidity ^0.8.24;`
- **Import Order**: External libraries first, then local imports
- **Contract Structure**: State variables, events, errors, constructor, functions

### Naming Conventions
- **Contracts**: PascalCase (e.g., `Mixer`, `IncrementalMerkleTree`)
- **Functions**: camelCase (e.g., `deposit`, `withdraw`)
- **State Variables**: 
  - Public: camelCase (e.g., `DENOMINATION`)
  - Private/Internal: prefixed with `s_` (e.g., `s_nullifierHashes`, `s_commitments`)
- **Immutable Variables**: prefixed with `i_` (e.g., `i_verifier`)
- **Constants**: SCREAMING_SNAKE_CASE (e.g., `DENOMINATION`)

### Error Handling
- **Custom Errors**: Prefixed with contract name (e.g., `Mixer__DepositValueMismatch`)
- **Error Parameters**: Include expected and actual values where relevant

### Documentation
- **NatSpec Comments**: Used for contract and function documentation
- **Educational Disclaimers**: Clear warnings about educational-only usage
- **Attribution**: Credit to original Tornado Cash inspiration

## Noir Conventions

### Circuit Structure
- **Function Signature**: Clear separation of public/private inputs
- **Variable Naming**: snake_case (e.g., `nullifier_hash`, `merkle_proof`)
- **Field Types**: Explicit `Field` type usage
- **Array Sizes**: Fixed-size arrays with explicit lengths (e.g., `[Field; 20]`)

### Documentation
- **Comments**: Clear explanation of cryptographic operations
- **Assert Statements**: Each assertion explains what security property is enforced

## TypeScript/JavaScript Conventions

### File Extensions
- **TypeScript**: `.ts` for TypeScript files
- **JavaScript**: `.js` for pure JavaScript utilities

### Import/Export
- **Default Exports**: Used for main functions
- **Named Imports**: Destructured imports for specific utilities
- **Path Resolution**: Relative paths with proper extensions

## Testing Conventions

### Foundry Tests
- **File Naming**: `*.t.sol` suffix for test files
- **Test Functions**: Start with `test` prefix
- **Setup Function**: Standard `setUp()` function for test initialization
- **Test Structure**: Arrange, Act, Assert pattern