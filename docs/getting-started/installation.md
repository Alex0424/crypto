# Installation Guide

This guide will help you set up your development environment for working with cryptocurrency and blockchain technologies.

## Prerequisites

- **Python 3.8+** for running MkDocs and various crypto tools
- **Node.js 16+** for web3 development
- **Git** for version control

## Installing uv (Python Package Manager)

We recommend using `uv` for fast Python package management:

```bash
# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# Or with pip
pip install uv
```

## Setting Up Documentation Environment

### 1. Create Virtual Environment

```bash
# Create a new virtual environment
uv venv crypto-docs-env

# Activate the environment
source crypto-docs-env/bin/activate  # Linux/Mac
# or
crypto-docs-env\Scripts\activate     # Windows
```

### 2. Install Dependencies

```bash
# Install MkDocs and all dependencies
uv pip install .[mkdocs]
```

### 3. Serve Documentation Locally

```bash
# Start the development server
mkdocs serve

# Or with specific host/port
mkdocs serve --dev-addr 0.0.0.0:8000
```

## Cryptocurrency Development Tools

### Wallet Software

#### MetaMask
Browser extension for Ethereum and EVM-compatible chains:
- [Download MetaMask](https://metamask.io/)
- [MetaMask Developer Documentation](https://docs.metamask.io/)

#### Electrum (Bitcoin)
Lightweight Bitcoin wallet:
- [Download Electrum](https://electrum.org/)
- Command line interface available

### Development Frameworks

#### Hardhat (Ethereum)
```bash
npm install --save-dev hardhat
npx hardhat
```

#### Truffle (Ethereum)
```bash
npm install -g truffle
truffle init
```

#### Brownie (Python)
```bash
uv pip install eth-brownie
brownie init
```

### Blockchain Interaction Libraries

#### Web3.py (Python)
```bash
uv pip install web3
```

#### Web3.js (JavaScript)
```bash
npm install web3
```

#### Ethers.js (JavaScript)
```bash
npm install ethers
```

## API Keys and Services

### Blockchain Data Providers

#### Infura
1. Sign up at [infura.io](https://infura.io/)
2. Create a new project
3. Get your API key
4. Set environment variable:
   ```bash
   export INFURA_API_KEY="your_api_key_here"
   ```

#### Alchemy
1. Sign up at [alchemy.com](https://alchemy.com/)
2. Create a new app
3. Get your API key
4. Set environment variable:
   ```bash
   export ALCHEMY_API_KEY="your_api_key_here"
   ```

### Price Data APIs

#### CoinGecko API
```bash
# Install the Python client
uv pip install pycoingecko
```

#### CoinMarketCap API
```bash
# Install the Python client
uv pip install python-coinmarketcap
```

## Security Setup

### Hardware Wallets

#### Ledger
- [Ledger Hardware Wallets](https://www.ledger.com/)
- [Ledger Live Software](https://www.ledger.com/ledger-live)

#### Trezor
- [Trezor Hardware Wallets](https://trezor.io/)
- [Trezor Suite](https://suite.trezor.io/)

### Software Security

#### GPG Setup
```bash
# Install GPG
sudo apt-get install gnupg  # Ubuntu/Debian
brew install gnupg          # macOS

# Generate key
gpg --gen-key

# Export public key
gpg --armor --export your-email@example.com > public-key.asc
```

#### SSH Key Setup
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"

# Add to SSH agent
ssh-add ~/.ssh/id_ed25519

# Copy public key
cat ~/.ssh/id_ed25519.pub
```

## Testing Environment

### Local Blockchain

#### Ganache
```bash
# Install Ganache CLI
npm install -g ganache

# Start local blockchain
ganache --deterministic
```

#### Hardhat Network
```bash
# Start local node
npx hardhat node
```

### Testnet Setup

#### Ethereum Testnets
- **Sepolia**: Latest Ethereum testnet
- **Goerli**: Legacy testnet (deprecated)

#### Getting Test ETH
- [Sepolia Faucet](https://sepoliafaucet.com/)
- [Alchemy Faucet](https://sepoliafaucet.com/)

## Environment Variables

Create a `.env` file in your project root:

```bash
# API Keys
INFURA_API_KEY=your_infura_key
ALCHEMY_API_KEY=your_alchemy_key
COINGECKO_API_KEY=your_coingecko_key

# Wallet Configuration
PRIVATE_KEY=your_private_key_for_testing
MNEMONIC=your_test_mnemonic_phrase

# Network Configuration
ETH_RPC_URL=https://mainnet.infura.io/v3/your_key
POLYGON_RPC_URL=https://polygon-mainnet.infura.io/v3/your_key
```

!!! warning "Security Warning"
    Never commit real private keys or API keys to version control. Use test keys only for development.

## IDE Setup

### VS Code Extensions

Recommended extensions for cryptocurrency development:

```json
{
  "recommendations": [
    "ms-python.python",
    "ms-vscode.vscode-json",
    "JuanBlanco.solidity",
    "nomic-foundation.hardhat-solidity",
    "ms-vscode.vscode-typescript-next",
    "esbenp.prettier-vscode",
    "ms-python.flake8",
    "ms-python.black-formatter"
  ]
}
```

### Solidity Development

#### Remix IDE
Browser-based IDE for Solidity:
- [Remix IDE](https://remix.ethereum.org/)
- No installation required
- Great for beginners

#### VS Code Solidity Extension
```bash
# Install Solidity extension
code --install-extension JuanBlanco.solidity
```

## Verification

Test your installation:

```bash
# Check Python and packages
python --version
mkdocs --version

# Check Node.js and npm
node --version
npm --version

# Test Web3 connection
python -c "from web3 import Web3; print('Web3 version:', Web3.api.version)"
```

## Troubleshooting

### Common Issues

#### Python Version Conflicts
```bash
# Check Python version
python --version

# Use specific Python version
python3.10 -m venv crypto-docs-env
```

#### Permission Errors
```bash
# Fix npm permissions
npm config set prefix ~/.npm-global
export PATH=~/.npm-global/bin:$PATH
```

#### SSL Certificate Issues
```bash
# Update certificates
pip install --upgrade certifi
```

### Getting Help

- **Documentation Issues**: Check the [MkDocs documentation](https://www.mkdocs.org/)
- **Crypto Development**: Join [Ethereum Stack Exchange](https://ethereum.stackexchange.com/)
- **General Python**: Visit [Python.org](https://www.python.org/)

## Next Steps

Once you have everything installed:

1. **[Complete the Quick Start guide](quick-start.md)**
2. **[Learn about blockchain fundamentals](../blockchain/what-is-blockchain.md)**
3. **[Explore Bitcoin basics](../crypto/bitcoin.md)**
4. **[Try smart contract development](../smart-contracts/introduction.md)**

---

*Your development environment is now ready for cryptocurrency and blockchain development!*
