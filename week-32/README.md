# Nervos Builder Track — Weekly Report (Week 32)

**Name:** Ekene Nwobodo  
**Focus:** Production Security Milestones and Public Testnet Release Gate  
**Week Ending:** 05-09-2026  
**Progress Recorded Through:** 01-09-2026

---

## 🎯 Overview

Week 32 brought the planned security milestones into implementation.

The frontend received updated deployment metadata, production dispute authorization, scheduled canonical indexing, and shared pre-sign validation. The contract reproducible checksum was also updated and verified.

Current progress includes an automated release gate and a manual real-wallet testnet acceptance matrix.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🧾 Commit Grouping

### Contract Repository

| Commit | Date | Milestone |
| --- | --- | --- |
| `d5cfee1` | 01-09-2026 | Update reproducible release and debug binary checksums |

### Frontend Repository

| Commit | Date | Milestone |
| --- | --- | --- |
| `f21c76c` | 01-09-2026 | Update testnet deployment metadata and Vercel env handling |
| `6205853` | 01-09-2026 | Harden dispute writes with persistent authorization |
| `376cf9c` | 01-09-2026 | Add canonical scheduled escrow indexing |
| `06ad7d0` | 01-09-2026 | Validate escrow transactions before signing |
| `e0c9c40` | 01-09-2026 | Add public testnet release gate and acceptance record |

---

## 🏗 What I Built

### 1. Verified Testnet Deployment Configuration

The frontend now uses the latest deployed contract metadata.

I also replaced dynamic environment-variable lookup with explicit `NEXT_PUBLIC_` references so Next.js and Vercel can include the values correctly during production builds.

The reproduced contract binary hash was confirmed to match the deployed testnet output data hash.

---

### 2. Production Dispute Authorization

The nonce system was moved to PostgreSQL for deployed environments.

The implementation now provides:

- hashed nonce storage
- expiration
- atomic single-use consumption
- fail-closed production behavior
- CKB, EVM, and BTC identity-to-lock verification
- explicit rejection of unsupported evidence signature types
- committed transaction enforcement
- structured authorization and conflict errors

---

### 3. Canonical Scheduled Indexing

The indexer now uses:

- twelve-block confirmation depth
- canonical checkpoint hashes
- reorganization detection
- PostgreSQL advisory locking
- deployment-block lower bound
- protected Vercel cron endpoint
- daily Hobby-plan synchronization

Read-triggered synchronization and post-action polling remain available for fresher product history.

---

### 4. Pre-Sign Transaction Safety

A shared preflight now runs after fee completion and immediately before transaction signing.

It checks:

- signer and selected-network genesis
- deployment CellDep availability
- deployed code hash
- live escrow outpoint
- escrow capacity, lock, type, and data

This gives users clearer errors when an escrow has already changed or the wallet is connected to the wrong network.

---

### 5. Public Testnet Release Gate

The automated release checks completed successfully:

- 99 frontend and shared-package tests
- frontend monorepo typecheck
- Next.js production build
- 26 contract unit tests
- 7 CKB-VM integration tests
- reproducible Docker checksums

A testnet acceptance document now tracks the remaining wallet-signed flows and transaction hashes.

---

## 🧠 Key Learnings

### 1. Authentication Must Survive Multiple Server Instances

Atomic PostgreSQL nonce consumption is stronger than process memory because it works across Vercel functions.

### 2. Signing Safety Should Use Current Chain State

The application should verify that the escrow and deployment cells are still live immediately before asking the wallet to sign.

### 3. Indexers Need Finality and Recovery

Cross-device history requires more than storing records. It requires canonical checkpoints, synchronization locking, and a recovery path.

### 4. Automated Tests Do Not Replace Real-Wallet Acceptance

The automated gate is complete, but buyer, seller, and arbitrator flows still need to be executed with real testnet wallets and recorded transaction hashes.

---

## 🚧 Current State

The project now has:

- hardened contract payout validation
- verified testnet deployment metadata
- persistent dispute authorization
- role-aware and wallet-aware product actions
- canonical scheduled indexer synchronization
- pre-sign transaction validation
- automated release evidence

Still required before mainnet:

- complete real-wallet testnet matrix
- independent review of the new hardening commits
- atomic index snapshot replacement during deep reorganization recovery
- explicit orphan-status reconciliation for dispute metadata

---

## 🔜 Next Steps

- push and deploy the milestone commits to Vercel
- configure PostgreSQL and cron environment variables
- run create, deliver, complete, cancel, refund, dispute, and both resolution paths
- record explorer links in the acceptance report
- submit the hardening commits for independent review
- keep mainnet disabled until every release gate passes

---

## 💡 Reflection

Week 32 was the point where the escrow MVP became much more security- and operations-aware.

The system is no longer judged only by whether a transaction can be built. It is judged by authorization, current chain state, recoverable history, reproducible deployment, and evidence that the complete user journey works.
