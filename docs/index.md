# Welcome to Crypto Documentation

Welcome to the comprehensive cryptocurrency and blockchain documentation hub! This site provides in-depth guides, tutorials, and reference materials for understanding the world of digital assets and blockchain technology.

## 🚀 What You'll Find Here

### 📚 Comprehensive Guides
- **Blockchain Fundamentals**: Learn the core concepts behind blockchain technology
- **Cryptocurrency Basics**: Understanding Bitcoin, Ethereum, and other digital assets
- **Smart Contracts**: Building and deploying decentralized applications
- **DeFi Ecosystem**: Decentralized finance protocols and strategies
- **NFTs**: Non-fungible tokens and digital collectibles
- **Security**: Best practices for protecting your digital assets

### 🛠️ Practical Resources
- Step-by-step tutorials
- Code examples and implementations
- API references and documentation
- Security checklists and best practices
- Market analysis and trends

### 🔐 Security First
Security is paramount in the cryptocurrency space. Every guide includes security considerations and best practices to help you protect your investments and data.

## 🌟 Featured Topics

=== "Bitcoin"
    The original cryptocurrency and digital gold standard.
    
    - [What is Bitcoin?](crypto/bitcoin.md)
    - Mining and consensus
    - Lightning Network
    - Security best practices

=== "Ethereum"
    The world's programmable blockchain platform.
    
    - [Ethereum Overview](crypto/ethereum.md)
    - Smart contracts and DApps
    - Ethereum 2.0 and staking
    - Gas optimization

=== "DeFi"
    Decentralized finance protocols and applications.
    
    - [DeFi Overview](defi/overview.md)
    - Decentralized exchanges
    - Lending and borrowing
    - Yield farming strategies

=== "NFTs"
    Non-fungible tokens and digital ownership.
    
    - [NFT Introduction](nfts/introduction.md)
    - Token standards (ERC-721, ERC-1155)
    - Marketplaces and trading
    - Creating and minting NFTs

## 🎯 Getting Started

New to cryptocurrency and blockchain? Start here:

1. **[Introduction to Crypto](getting-started/introduction.md)** - Basic concepts and terminology
2. **[Installation Guide](getting-started/installation.md)** - Set up your development environment
3. **[Quick Start](getting-started/quick-start.md)** - Your first blockchain interaction

## 💡 Key Features

!!! tip "Interactive Learning"
    All code examples are tested and include interactive elements where possible.

!!! note "Up-to-Date Information"
    Content is regularly updated to reflect the latest developments in the crypto space.

!!! warning "Security Focus"
    Every tutorial includes security considerations and best practices.

## 🤝 Community

Join our growing community of cryptocurrency enthusiasts and developers:

- **Discord**: Join discussions and get help from the community
- **GitHub**: Contribute to the documentation and report issues
- **Twitter**: Follow for updates and crypto news

## 📈 Market Data

<div class="grid" markdown>

<div class="card" markdown>
**Bitcoin (BTC)**
<br>
Current price and market cap updates
</div>

<div class="card" markdown>
**Ethereum (ETH)**
<br>
Smart contract platform metrics
</div>

<div class="card" markdown>
**DeFi TVL**
<br>
Total value locked in DeFi protocols
</div>

<div class="card" markdown>
**NFT Volume**
<br>
Weekly NFT trading volume
</div>

</div>

---

*Start your journey into the world of cryptocurrency and blockchain technology today!*

name: Deploy Crypto Docs using MkDocs

on:
  push:
    branches:
      - main  # or the branch you want to trigger deployment from
  pull_request:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # Fetch full history for git-revision-date-localized-plugin

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install uv
        uses: astral-sh/setup-uv@v2
        with:
          version: "latest"

      - name: Create virtual environment
        run: |
          uv venv crypto-docs-env
          echo "VIRTUAL_ENV=$PWD/crypto-docs-env" >> $GITHUB_ENV
          echo "$PWD/crypto-docs-env/bin" >> $GITHUB_PATH

      - name: Install dependencies from pyproject.toml
        run: |
          uv pip install .[mkdocs]

      - name: Build MkDocs site
        run: |
          mkdocs build --verbose

      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main'
        run: |
          mkdocs gh-deploy --force
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Upload build artifacts
        if: github.event_name == 'pull_request'
        uses: actions/upload-artifact@v4
        with:
          name: mkdocs-site
          path: site/
