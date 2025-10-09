# Altworth Trading Card Game Platform

**Web3-powered digital trading card game platform built on Solana blockchain**

## About

Altworth is a modern trading card game platform that combines traditional TCG gameplay with Web3 technology. Players can purchase card packs, reveal NFT cards, and engage in a dynamic marketplace powered by the Solana blockchain.

## Architecture

Our platform is built with a microservices architecture:

- **[Frontend](https://github.com/altworth-markets/front-end)** - Next.js application with Web3 integration
  - **Live Demo**: [altworth.netlify.app](https://altworth.netlify.app)
  - Stack: Next.js 15, TypeScript, Tailwind CSS, Solana Web3.js
  - Features: Wallet integration, pack purchase, NFT claiming, admin dashboard

- **[Backend](https://github.com/altworth-markets/backend)** - RESTful API server
  - Stack: Bun runtime, Hono framework, PostgreSQL
  - Features: Card management, pack operations, buyback pricing, transaction tracking

- **[SDK](https://github.com/altworth-markets/sdk)** - TypeScript SDK for platform integration
  - Packages: `@altworth-markets/sdk-core`, `sdk-react`, `sdk-solana`, `sdk-types`
  - Published to: GitHub Packages
  - Features: Type-safe API client, React hooks, Solana utilities

- **[Contracts](https://github.com/altworth-markets/contracts)** - Solana smart contracts
  - Stack: Anchor framework, Rust
  - Features: NFT minting, pack mechanics, marketplace operations

## Tech Stack

**Blockchain & Web3**
- Solana blockchain (devnet/mainnet)
- Anchor framework for smart contracts
- Solana Web3.js for client integration
- Helius RPC for reliable blockchain access

**Frontend**
- Next.js 15 with App Router
- TypeScript for type safety
- Tailwind CSS for styling
- Wallet adapter for multi-wallet support

**Backend**
- Bun runtime for performance
- Hono web framework
- PostgreSQL database
- Drizzle ORM

**Infrastructure**
- Netlify for frontend hosting
- GitHub Actions for CI/CD
- Docker for local development
- GitHub Packages for private SDK distribution

## Security & Best Practices

- **API Key Protection**: Secure RPC proxy pattern keeps Helius API keys server-side
- **Authentication**: GitHub Packages for private SDK access
- **Testing**: Comprehensive test coverage with Jest
- **Type Safety**: Full TypeScript coverage across all repositories
- **Code Quality**: ESLint, Prettier, and automated CI checks

## Getting Started

Visit our [frontend repository](https://github.com/altworth-markets/front-end) for setup instructions and development guides.

**Live Platform**: [altworth.netlify.app](https://altworth.netlify.app)

## Contributing

This is a private organization. If you're a team member, check individual repository READMEs for contribution guidelines and development setup.
