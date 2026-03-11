# Atomic Intent Shield (Hackathon Submission Edition)

Atomic Intent Shield is a privacy-first intent trading prototype for the hackathon theme:

**Deploy on Revive, Scale on Polkadot 2.0**

This sanitized repository is prepared for public GitHub submission and excludes internal deployment records, private environment files, and non-essential operational history.

## Track Selection

- Primary Track: **Track 1 — Revive Migration Challenge**
- Supporting elements:
  - Revive-compatible Solidity contracts (`contracts/solidity`)
  - EVM wallet flow with approve + intent submit
  - Solver-mediated on-chain submission and matching

## What This Project Demonstrates

- ZK intent generation in browser (Circom + snarkjs)
- Intent submission API + matching engine (Rust solver + Redis)
- EVM dark pool contract flow on Revive-compatible endpoint
- Dual-asset intent model (e.g., wETH/USDC)
- End-to-end demo UI for trade and transaction monitoring

## Architecture

1. Frontend creates proof + signed intent payload.
2. Solver validates request and submits intent on-chain.
3. Solver stores pending intents and runs matcher.
4. Matched intents settle through dark pool contract.

Core modules:

- `frontend/` React + TypeScript UI
- `solver/` Rust API + matcher + chain adapter
- `contracts/solidity/` Revive migration contracts
- `circuits/` ZK circuits and setup/test scripts

## Quick Start (Local Demo)

### Prerequisites

- Node.js 18+
- Rust stable toolchain
- Docker + Docker Compose

### Run

```bash
docker compose up -d --build
```

Services:

- Frontend: `http://localhost:13080`
- Solver: `http://localhost:3001`

### Health Check

```bash
curl http://localhost:3001/health
```

## Revive Contract Deployment (Track 1)

```bash
cd contracts/solidity
npm install
npm run build
npm test
npm run deploy:revive
```

After deployment, set addresses in runtime env:

- `DARK_POOL_CONTRACT`
- `INTENT_VERIFIER_CONTRACT`
- `VITE_DARK_POOL_ADDRESS`
- `VITE_VERIFIER_ADDRESS`

## Judging Criteria Mapping

- Technical implementation:
  - Rust solver, Solidity contracts, Circom proof flow are all included.
- Innovation & practicality:
  - Private intent model + atomic match/settlement path.
- Polkadot/Revive integration:
  - Revive-compatible contract deployment and EVM tooling migration path.
- Developer experience:
  - Dockerized run path, structured folders, clear env configuration.
- Ecosystem contribution:
  - Reusable migration scaffold for EVM-to-Revive projects.

## Sanitization Notes

This submission package intentionally excludes:

- Internal server deployment credentials and private host records
- Local `.env` files and private keys
- Internal rollback/ops records not required for judging
- Build artifacts and dependency caches

## Repository Layout

```text
release/github_hackathon_submission/
├── circuits/
├── contracts/
│   ├── dark_pool/
│   ├── groth16_verifier/
│   ├── intent_verifier/
│   └── solidity/
├── deploy/
├── frontend/
├── solver/
├── docker-compose.yml
└── README.md
```

## License

MIT
