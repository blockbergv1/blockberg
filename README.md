# Blockberg

A decentralized paper trading terminal built on Solana, powered by real-time price feeds from Pyth Network and ephemeral rollups from MagicBlock.

## Overview

Blockberg is a competitive trading platform where users can practice trading crypto assets without risking real capital. The platform features real-time market data, competitive tournaments, performance analytics, and social trading features. All trades are executed on-chain using Solana's high-performance blockchain.

## Key Features

### Trading Terminal
- Real-time price feeds for SOL, BTC, ETH, AVAX, and LINK powered by Pyth Network
- Support for spot trading and leveraged positions
- Long and short positions with take-profit and stop-loss orders
- Live order book and trade execution
- Market news integration from cryptocurrency news sources
- Trading chart visualization using TradingView-style charts

### Competition System
- Create and participate in trading tournaments
- Registration and active phases with automatic transitions
- Prize pool system with SOL rewards
- Real-time leaderboard with profit and loss rankings
- Multiple simultaneous competitions support
- Automated tournament settlement

### Dashboard & Analytics
- Comprehensive trading performance metrics
- Realized and unrealized profit and loss tracking
- Win rate and trade statistics
- Position management and monitoring
- Trade history with detailed transaction records
- Account balance tracking across all trading pairs
- Social sharing of successful trades

### Social Features
- Trade feed displaying community positions
- Like and comment on published trades
- Share trade analysis and strategies
- User authentication via Solana wallet
- Reputation system based on trading performance

## Technology Stack

### Frontend
- SvelteKit 2.0 for the application framework
- TypeScript for type-safe development
- Vite for build tooling and development server
- TradingView Lightweight Charts for market visualization
- Responsive design with Bloomberg Terminal-inspired UI

### Blockchain & Web3
- Solana blockchain for on-chain trade execution
- MagicBlock Bolt SDK for ephemeral rollups
- Anchor framework for Solana program interaction
- Multiple wallet adapter support including Phantom and Solflare
- Metaplex for NFT and token metadata

### Data & Infrastructure
- Pyth Network Hermes Client for real-time price oracles
- Supabase for user data and social features
- WebSocket connections for live data streaming
- RESTful APIs for external data sources

## Architecture

The application follows a modular architecture with clear separation of concerns:

### On-Chain Components
The platform uses a custom Solana program deployed on Devnet that manages:
- Trading accounts with separate balances per trading pair
- Position tracking for long and short trades
- Competition lifecycle management
- Leaderboard calculation and prize distribution
- Transaction validation and security

### Price Oracle Integration
Pyth Network provides sub-second price updates with:
- Multiple price feed IDs for different assets
- Confidence intervals for price accuracy
- EMA price calculations for trend analysis
- Spread calculation for market volatility
- Historical price data access

### State Management
The frontend implements reactive state management for:
- Wallet connection status
- User trading positions
- Competition participation
- Price feed subscriptions
- Toast notifications for user feedback

## Project Structure

The monorepo contains two main directories:

### frontend-main
The SvelteKit application containing:
- Routes for terminal, dashboard, competition, and landing pages
- Wallet integration and authentication
- Trading interface and order execution
- Chart rendering and market data display
- Social features and user profiles

### backend-main
Supporting services and utilities for:
- Data aggregation
- External API integrations
- Background job processing

## Getting Started

### Prerequisites
- Node.js version 18 or higher
- npm or yarn package manager
- A Solana wallet browser extension
- Solana Devnet SOL for transaction fees

### Environment Configuration

Create a .env file in the frontend-main directory with the following variables:

Supabase Configuration:
- Database URL and anonymous key for backend services
- Required for social features and trade sharing

Solana RPC Endpoints:
- MagicBlock RPC endpoint for ephemeral rollup access
- Standard Solana Devnet RPC for fallback

Pyth Configuration:
- Hermes API endpoint for price feeds
- Price feed IDs for each supported asset

Program IDs:
- Paper trading program address
- Component addresses for accounts, positions, and leaderboards
- System addresses for trade execution and settlements

Competition Configuration:
- World ID and instance ID for MagicBlock integration
- Default competition entity address

### Installation

Navigate to the frontend directory and install dependencies. The project uses npm with legacy peer dependencies to resolve Solana wallet adapter compatibility.

### Development

Start the development server with hot module reloading enabled. The application will be available on localhost with automatic browser refresh on file changes.

### Building for Production

The build process compiles TypeScript, optimizes assets, and generates a production-ready application. The adapter configuration determines the deployment target.

## Deployment

### Vercel Deployment

The application is configured for deployment on Vercel with:
- Automatic builds on git push
- Environment variable management through dashboard
- Edge network distribution for low latency
- Serverless function support

### Environment Variables on Vercel

All PUBLIC prefixed environment variables must be configured in the Vercel project settings. These are required for:
- Blockchain connectivity
- Price feed access
- Database operations
- External API calls

### Build Configuration

The vercel.json file specifies:
- Build command and output directory
- Root directory for monorepo structure
- Framework preset for SvelteKit
- Install command with dependency flags

## Features in Detail

### Wallet Integration

The platform supports multiple Solana wallet providers through a unified adapter interface. Users can connect their wallet to:
- View their SOL balance
- Initialize trading accounts
- Execute trades on-chain
- Join competitions
- Sign transactions securely

### Trading Mechanics

Spot Trading:
Users can buy and sell assets at current market prices with instant execution. Balances are maintained separately for USDT and each crypto asset.

Leveraged Positions:
Open long or short positions with optional risk management through take-profit and stop-loss levels. Positions remain active until manually closed or targets are hit.

Account Management:
Each trading pair requires account initialization. Accounts track token balances and position history independently.

### Competition Flow

Creation Phase:
Competitions are created with parameters including ID, duration, entry fee, and participant limits. The creator sets the registration window and trading duration.

Registration Phase:
Users join by paying the entry fee in SOL, which contributes to the prize pool. All participants start with equal virtual capital.

Active Phase:
Trading is enabled for the competition duration. Participants execute trades, and rankings update in real-time based on portfolio value.

Settlement Phase:
When time expires, final rankings are calculated and prizes are distributed proportionally to top performers.

### Performance Tracking

The dashboard provides comprehensive analytics:
- Total realized profit and loss from closed positions
- Unrealized profit and loss from open positions
- Win rate percentage across all trades
- Average trade size and volume metrics
- Best and worst individual trade performance
- Complete transaction history with timestamps

### Social Trading

Users can share successful trades with the community:
- Post closed positions to the public feed
- Include trade analysis and strategy notes
- Receive likes and comments from other traders
- Build reputation through consistent performance
- Learn from community strategies

## Security Considerations

### On-Chain Security
- All trades are validated by the Solana program
- Program derived addresses prevent unauthorized access
- Transaction signatures required for all state changes
- Account ownership verification for every operation

### Frontend Security
- Environment variables never exposed to client
- Wallet private keys remain in browser extension
- Transaction preview before signing
- Input validation and sanitization

### API Security
- Rate limiting on external requests
- CORS configuration for allowed origins
- Supabase row-level security policies
- Authenticated endpoints for sensitive operations

## Performance Optimizations

### Frontend Optimizations
- Code splitting for reduced initial bundle size
- Lazy loading of chart libraries
- Debounced price updates to prevent UI thrashing
- Optimistic UI updates for better user experience
- Connection pooling for WebSocket efficiency

### On-Chain Optimizations
- Batch transaction support where applicable
- Ephemeral rollups for high-frequency operations
- Compressed transaction data
- Priority fee optimization for faster confirmation

## Troubleshooting

### Common Issues

Wallet Connection Failures:
Ensure the wallet extension is installed and unlocked. Check that the correct network is selected in the wallet settings.

Price Feed Not Updating:
Verify internet connectivity and check browser console for WebSocket errors. Pyth Network status can be checked on their website.

Transaction Failures:
Confirm sufficient SOL balance for transaction fees. Check Solana network status for congestion or outages.

Build Errors:
Clear node modules and reinstall dependencies. Ensure Node.js version meets requirements.

## Contributing

Contributions are welcome to improve the platform. Areas for contribution include:
- Additional trading pairs and assets
- Enhanced chart indicators and tools
- Mobile responsive improvements
- Performance optimizations
- Bug fixes and security patches
- Documentation updates

## License

All rights reserved. Copyright 2026 Blockberg.

## Acknowledgments

This project is built on top of excellent open-source technologies:
- Solana blockchain for high-performance transactions
- Pyth Network for reliable price oracles
- MagicBlock for ephemeral rollup infrastructure
- Metaplex for token standards
- Supabase for backend services
- The SvelteKit and Vite teams for development tools

## Contact and Support

For questions, issues, or feature requests, please refer to the project repository or contact the development team.

## Roadmap

Future enhancements planned:
- Additional trading pairs and markets
- Advanced order types including limit orders
- Portfolio analytics and reporting
- Mobile application development
- Mainnet deployment preparation
- Integration with additional price oracles
- Enhanced social features and community tools
- Trading bot API for algorithmic strategies
