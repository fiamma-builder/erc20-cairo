# ERC20 Contracts Cairo

A Cairo-based implementation of upgradeable ERC20 token contracts for Starknet, built with OpenZeppelin Contracts for Cairo.

## Overview

This project provides a secure, upgradeable ERC20 token implementation that combines the power of Cairo smart contracts with battle-tested OpenZeppelin components.
## Features

- **ERC20 Standard Compliance**: Full implementation of the ERC20 token standard
- **Upgradeable Architecture**: Uses OpenZeppelin's upgradeable pattern for contract evolution
- **Ownership Management**: Built-in ownership controls with transfer and renouncement capabilities
- **Camel Case Support**: Supports both snake_case and camelCase function naming conventions
- **Comprehensive Testing**: Extensive test suite covering all functionality
- **OpenZeppelin Integration**: Built on top of trusted OpenZeppelin components

## Contract Components

### Core Functionality

- **ERC20Component**: Standard token functionality (transfer, approve, balance queries)
- **OwnableComponent**: Access control and ownership management
- **UpgradeableComponent**: Contract upgrade capabilities

### Key Features

1. **Token Operations**
   - Transfer tokens between addresses
   - Approve spending allowances
   - Query balances and allowances
   - Get token metadata (name, symbol, decimals)

2. **Ownership Management**
   - Transfer ownership to another address
   - Renounce ownership (make contract ownerless)
   - Owner-only functions for privileged operations

3. **Upgrade Capability**
   - Owner can upgrade contract implementation
   - Maintains state during upgrades
   - Secure upgrade process with ownership checks

## Installation

### Prerequisites

- [Scarb](https://docs.swmansion.com/scarb/) (Cairo package manager)
- [Starknet Foundry](https://foundry-rs.github.io/starknet-foundry/) (for testing)

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd erc20-cairo
```

2. Build the project:
```bash
scarb build
```

3. Run tests:
```bash
scarb test
```

## Usage

### Deployment

The contract constructor requires the following parameters:

```cairo
constructor(
    name: ByteArray,           // Token name (e.g., "My Token")
    symbol: ByteArray,         // Token symbol (e.g., "MTK")
    fixed_supply: u256,        // Initial token supply
    recipient: ContractAddress, // Address to receive initial supply
    owner: ContractAddress,    // Contract owner address
)
```

### Contract Interface

#### ERC20 Functions

```cairo
// Standard ERC20 functions
fn transfer(recipient: ContractAddress, amount: u256) -> bool
fn transfer_from(sender: ContractAddress, recipient: ContractAddress, amount: u256) -> bool
fn approve(spender: ContractAddress, amount: u256) -> bool
fn balance_of(account: ContractAddress) -> u256
fn allowance(owner: ContractAddress, spender: ContractAddress) -> u256
fn total_supply() -> u256

// Metadata functions
fn name() -> ByteArray
fn symbol() -> ByteArray
fn decimals() -> u8

// CamelCase variants
fn transferFrom(sender: ContractAddress, recipient: ContractAddress, amount: u256) -> bool
fn balanceOf(account: ContractAddress) -> u256
fn totalSupply() -> u256
```

#### Ownership Functions

```cairo
fn owner() -> ContractAddress
fn transfer_ownership(new_owner: ContractAddress)
fn renounce_ownership()

// CamelCase variants
fn transferOwnership(newOwner: ContractAddress)
fn renounceOwnership()
```

#### Upgrade Functions

```cairo
fn upgrade(new_class_hash: ClassHash)  // Owner only
```

## Testing

The project includes a comprehensive test suite covering:

- Token transfers and approvals
- Ownership management
- Contract upgrades
- Error conditions and edge cases
- Event emissions

Run tests with:
```bash
scarb test
```

For verbose output:
```bash
scarb test -- --nocapture
```

## Project Structure

```
├── src/
│   └── lib.cairo           # Main contract implementation
├── tests/
│   ├── test_contract.cairo # Comprehensive test suite
│   └── erc20_interface.cairo # Test interface definitions
├── Scarb.toml             # Project configuration
└── README.md              # This file
```

## Dependencies

- `starknet`: Core Starknet functionality
- `openzeppelin_access`: Access control components
- `openzeppelin_token`: Token implementations
- `openzeppelin_upgrades`: Upgrade functionality
- `snforge_std`: Testing framework
- `openzeppelin_testing`: Testing utilities

## Security Considerations

- The contract uses OpenZeppelin's battle-tested components
- Ownership functions are protected by access controls
- Upgrade functionality requires owner privileges
- All state changes emit appropriate events
- Comprehensive test coverage ensures reliability

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with [OpenZeppelin Contracts for Cairo](https://github.com/OpenZeppelin/cairo-contracts)
- Powered by [Starknet](https://starknet.io/)
- Testing with [Starknet Foundry](https://foundry-rs.github.io/starknet-foundry/) 
