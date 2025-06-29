# Bamboo Bridge (B3Bridge)

A comprehensive cross-chain bridge solution enabling secure token transfers between Ethereum and Sei networks using Chainlink CCIP (Cross-Chain Interoperability Protocol).

## 🌉 Overview

Bamboo Bridge is a decentralized cross-chain bridge that allows users to transfer tokens seamlessly between Ethereum and Sei blockchains. The platform leverages Chainlink's CCIP infrastructure to ensure secure, reliable, and trustless cross-chain transactions.

### Key Features

- **Cross-Chain Bridging**: Transfer tokens between Ethereum and Sei networks
- **Multi-Token Support**: Bridge ETH, USDC, and wrapped tokens (wETH, wUSDC)
- **Chainlink CCIP Integration**: Leverages Chainlink's secure cross-chain infrastructure
- **Real-time Monitoring**: Track bridge transactions and status updates
- **Validator Network**: Automated validation service for transaction security
- **Modern Web Interface**: User-friendly dApp with responsive design
- **Smart Contract Security**: Audited and secure smart contracts on both chains

### Supported Networks

- **Ethereum** (Sepolia Testnet)
- **Sei** (Atlantic Testnet)

### Supported Tokens

- **ETH** (Native Ethereum)
- **USDC** (USD Coin)
- **wETH** (Wrapped Ethereum on Sei)
- **wUSDC** (Wrapped USDC on Sei)

## 🏗️ Architecture

The Bamboo Bridge consists of four main components:

```
bamboo-bridge/
├── b3bridge-smartcontract-evm/     # Ethereum smart contracts
├── b3bridge-smartcontract-cosmos/  # Sei network smart contracts
├── b3bridge-validator/             # Validator service (NestJS)
└── b3bridge-frontend/              # Web application (Next.js)
```

### Component Overview

#### 1. Smart Contracts (Ethereum)
- **Location**: `b3bridge-smartcontract-evm/`
- **Technology**: Solidity, Hardhat
- **Key Contracts**:
  - `NativeBridge.sol` - Main bridge contract for Ethereum
  - `MockCCIPRouter.sol` - CCIP router implementation
  - `MockERC20.sol` - ERC-20 token implementation

#### 2. Smart Contracts (Sei)
- **Location**: `b3bridge-smartcontract-cosmos/`
- **Technology**: Solidity, Hardhat
- **Key Contracts**:
  - `B3BridgeDest.sol` - Destination bridge contract for Sei
  - `CustomCoin.sol` - Custom token implementation

#### 3. Validator Service
- **Location**: `b3bridge-validator/`
- **Technology**: NestJS, TypeScript
- **Features**:
  - Multi-chain transaction monitoring
  - Automated validation processes
  - RESTful API endpoints
  - Docker containerization

#### 4. Frontend Application
- **Location**: `b3bridge-frontend/`
- **Technology**: Next.js 14, React, TypeScript
- **Features**:
  - Modern UI with dark theme
  - Wallet integration (MetaMask)
  - Real-time transaction tracking
  - 3D WebGL components

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18.x or higher
- **Yarn** or **npm**
- **Git**
- **MetaMask** or compatible Web3 wallet
- **Docker** (optional, for containerized deployment)

### Installation

1. **Clone the Repository**
   ```bash
   git clone --recurse-submodules https://github.com/Bamboo-Software/b3bridge.git
   cd b3bridge
   ```

2. **Install Dependencies**
   ```bash
   # Install validator dependencies
   cd b3bridge-validator
   yarn install

   # Install frontend dependencies
   cd ../b3bridge-frontend
   yarn install

   # Install smart contract dependencies
   cd ../b3bridge-smartcontract-evm
   yarn install

   cd ../b3bridge-smartcontract-cosmos
   yarn install
   ```

3. **Environment Setup**
   ```bash
   # Copy environment files
   cp b3bridge-validator/.env.example b3bridge-validator/.env
   cp b3bridge-frontend/.env.example b3bridge-frontend/.env.local
   ```

4. **Configure Environment Variables**
   
   **Validator Service** (`b3bridge-validator/.env`):
   ```env
   # Application
   HOST=127.0.0.1
   PORT=3000
   NODE_ENV=development

   # Ethereum Configuration
   ETH_CHAIN_ID=11155111
   ETH_CHAIN_RPC_URL=https://sepolia.infura.io/v3/YOUR_PROJECT_ID
   ETH_CHAIN_PRIVATE_KEY=your_ethereum_private_key
   ETH_CHAIN_CONTRACT_ADDRESS=your_ethereum_bridge_contract_address

   # Sei Configuration
   SEI_CHAIN_ID=1328
   SEI_CHAIN_RPC_URL=https://evm-rpc-testnet.sei-apis.com
   SEI_CHAIN_PRIVATE_KEY=your_sei_private_key
   SEI_CHAIN_CONTRACT_ADDRESS=your_sei_bridge_contract_address
   ```

   **Frontend** (`b3bridge-frontend/.env.local`):
   ```env
   # Ethereum Network
   NEXT_PUBLIC_ETH_CHAIN_ID=11155111
   NEXT_PUBLIC_ETH_CHAIN_RPC_URL=https://sepolia.infura.io/v3/YOUR_INFURA_KEY
   NEXT_PUBLIC_ETH_BRIDGE_CONTRACT=your_ethereum_bridge_contract_address
   NEXT_PUBLIC_ETH_USDC_ADDRESS=your_usdc_contract_address

   # Sei Network
   NEXT_PUBLIC_SEI_CHAIN_ID=1328
   NEXT_PUBLIC_SEI_CHAIN_RPC_URL=https://evm-rpc-testnet.sei-apis.com
   NEXT_PUBLIC_SEI_BRIDGE_CONTRACT=your_sei_bridge_contract_address
   NEXT_PUBLIC_SEI_WUSDC_ADDRESS=your_wusdc_contract_address
   NEXT_PUBLIC_SEI_WETH_ADDRESS=your_weth_contract_address
   ```

## 🏃‍♂️ Running the Application

### 1. Start Validator Service
```bash
cd b3bridge-validator

# Development mode
yarn start:dev

# Production mode
yarn build
yarn start:prod

# Docker deployment
docker-compose up --build
```

### 2. Start Frontend Application
```bash
cd b3bridge-frontend

# Development mode
yarn dev

# Production mode
yarn build
yarn start

# Docker deployment
docker build -t b3bridge-frontend .
docker run -p 3000:3000 b3bridge-frontend
```

### 3. Deploy Smart Contracts
```bash
# Deploy Ethereum contracts
cd b3bridge-smartcontract-evm
npx hardhat compile
npx hardhat deploy --network sepolia

# Deploy Sei contracts
cd ../b3bridge-smartcontract-cosmos
npx hardhat compile
npx hardhat deploy --network sei-testnet
```

## 📚 Documentation

### API Documentation
- **Validator API**: `http://localhost:3000/api/docs` (Swagger UI)
- **API Base URL**: `http://localhost:3000/api`

### Frontend Application
- **Local Development**: `http://localhost:3000`
- **Bridge Interface**: `http://localhost:3000/bridge`

## 🧪 Testing

### Smart Contracts
```bash
# Ethereum contracts
cd b3bridge-smartcontract-evm
npx hardhat test

# Sei contracts
cd b3bridge-smartcontract-cosmos
npx hardhat test
```

### Validator Service
```bash
cd b3bridge-validator
yarn test              # Unit tests
yarn test:e2e          # End-to-end tests
yarn test:cov          # Coverage report
```

### Frontend Application
```bash
cd b3bridge-frontend
yarn test              # Unit tests
yarn lint              # Code linting
```

## 🔧 Development

### Available Scripts

**Validator Service**:
```bash
yarn start:dev          # Development with hot reload
yarn build              # Build for production
yarn start:prod         # Start production server
yarn test               # Run tests
yarn lint               # Lint code
yarn format             # Format code
```

**Frontend**:
```bash
yarn dev                # Development server
yarn build              # Build for production
yarn start              # Start production server
yarn lint               # Lint code
```

**Smart Contracts**:
```bash
npx hardhat compile     # Compile contracts
npx hardhat test        # Run tests
npx hardhat deploy      # Deploy contracts
npx hardhat verify      # Verify contracts
```

## 🐳 Docker Deployment

### Validator Service
```bash
cd b3bridge-validator
docker-compose up -d --build
```

### Frontend Application
```bash
cd b3bridge-frontend
docker build -t b3bridge-frontend .
docker run -d -p 3000:3000 b3bridge-frontend
```

## 🔒 Security

- **Smart Contract Audits**: All contracts undergo security audits
- **Chainlink CCIP**: Leverages Chainlink's secure cross-chain infrastructure
- **Validator Network**: Multi-validator consensus for transaction security
- **Rate Limiting**: API rate limiting to prevent abuse
- **Input Validation**: Comprehensive input validation across all components

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow TypeScript best practices
- Write comprehensive tests
- Use conventional commit messages
- Ensure code passes linting
- Update documentation as needed

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: Check the individual component README files
- **Issues**: Report bugs and feature requests via GitHub Issues
- **Discussions**: Join community discussions on GitHub Discussions

## 🔗 Links

- **Frontend**: [B3Bridge Frontend](b3bridge-frontend/)
- **Validator**: [B3Bridge Validator](b3bridge-validator/)
- **Ethereum Contracts**: [B3Bridge EVM Contracts](b3bridge-smartcontract-evm/)
- **Sei Contracts**: [B3Bridge Cosmos Contracts](b3bridge-smartcontract-cosmos/)

---

**Built with ❤️ by the Bamboo Bridge Team**
