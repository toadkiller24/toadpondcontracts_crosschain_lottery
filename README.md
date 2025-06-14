# ToadPond Cross-Chain Lottery

A sophisticated decentralized cross-chain lottery system leveraging Chainlink's CCIP (Cross-Chain Interoperability Protocol) and VRF (Verifiable Random Function) for secure, fair, and cross-chain lottery operations.

## Technical Overview

### Automatic Pricing System
The lottery implements an advanced auto-pricing mechanism that ensures optimal entry fees and token swaps:

- **Chainlink Price Feeds**: Uses ETH/USD price feed for real-time market data
- **Uniswap V4 Integration**: 
  - Direct pool price observation via `sqrtPriceX96`
  - Optimized swap calculations with price bounds
  - Dynamic slippage adjustment (10%-60% range)
  - Gas-efficient price calculations using bit shifting

### Smart Contract Architecture

#### Core Contracts
- `VRFLottery.sol` (Main Contract):
  - Chainlink VRF V2+ for randomness
  - Advanced ETH-to-BONE swap mechanism
  - Automatic entry fee calculation
  - Cross-chain winner distribution
  - Gas-optimized with packed structs
  - Adaptive slippage based on market conditions
  - Safety bounds for token ratios (10-100M BONE/ETH)

- `CrossChainLotteryEntry.sol`:
  - CCIP-based cross-chain messaging
  - Self-sustaining fee model
  - User-paid cross-chain verification

#### Key Features

**1. Cross-Chain Infrastructure**
- Chainlink CCIP for trustless cross-chain communication
- Verifiable message passing between chains
- Cross-chain prize distribution system

**2. Randomness & Fairness**
- Chainlink VRF V2+ for verifiable random numbers
- Multi-word random number support
- Configurable confirmations (default: 3)

**3. Price Management**
- Real-time ETH/USD price feeds
- Automated price validation and staleness checks
- Dynamic slippage adjustment:
  - Base: 25% (for low TVL pools)
  - Range: 10% to 60%
  - Auto-adjusts based on swap success/failure

**4. Economic Model**
- Prize distribution:
  - Winners: 60%
  - Development: 5%
  - Funding: 30%
  - Token burning: 5%
- Points system (5 points per entry)
- Configurable maximum players per round

**5. Security Features**
- ReentrancyGuard for all entry functions
- Pausable contract functionality
- Cross-chain message verification
- Gas-optimized struct packing
- Price bounds validation
- Emergency withdrawal systems
- Minimum/maximum entry amount checks

## Dependencies

- Chainlink Contracts (VRF V2+, CCIP, Price Feeds)
- OpenZeppelin Contracts (Security, Token Standards)
- Uniswap V4 Core & Periphery
- Permit2 & Universal Router
- Foundry Development Suite

## Development

This project uses Foundry for development, testing, and deployment.

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation)
- [Git](https://git-scm.com/downloads)

### Setup

1. Clone the repository
2. Install dependencies:
   ```shell
   forge install
   ```

### Build

```shell
forge build
```

### Test

```shell
forge test
```

### Deploy

For VRF Lottery:
```shell
forge script script/DeployVRFLottery.s.sol:DeployVRFLottery --rpc-url <your_rpc_url> --private-key <your_private_key>
```

For Cross-Chain Lottery:
```shell
forge script script/DeployCrossChainLottery.s.sol:DeployCrossChainLottery --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Interact with Deployed Contracts

Enter VRF Lottery:
```shell
forge script script/EnterWithETH.s.sol:EnterWithETH --rpc-url <your_rpc_url> --private-key <your_private_key>
```

Enter Cross-Chain Lottery:
```shell
forge script script/EnterCrossChainLottery.s.sol:EnterCrossChainLottery --rpc-url <your_rpc_url> --private-key <your_private_key>
```

## Security

> Note: This is a private repository containing proprietary smart contract code. Please ensure proper security measures when handling the code.

## License

MIT
