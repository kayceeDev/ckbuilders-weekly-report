# Nervos Builder Track — Weekly Report (Week 31)

**Name:** Ekene Nwobodo  
**Focus:** Testnet Deployment Verification, Indexer Recovery, and Release-Gate Planning  
**Week Ending:** 26-08-2026

---

## 🎯 Overview

Week 31 focused on planning how the hardened escrow system would operate after deployment, not only how it would compile locally.

The work covered reproducible contract artifacts, frontend deployment metadata, indexer synchronization, chain reorganization recovery, and the checks required before asking the public to test the application.

This was another planning and verification week with no repository commits recorded in the reporting window.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🧾 Commit Grouping

No repository commits were recorded for Week 31.

The work was grouped into the next implementation milestones:

1. production dispute authorization
2. reorganization-safe indexer synchronization
3. pre-sign transaction safety
4. public testnet acceptance

---

## 🏗 What I Worked On

### 1. Deployment Metadata Verification

I reviewed how OffCKB deployment output maps into the frontend configuration.

The frontend needs:

- contract code hash
- hash type
- CellDep transaction hash
- CellDep index
- lock and type script configuration

The deployed binary must also match the binary produced by the reproducible build.

---

### 2. Indexer Recovery Design

The indexer already reconstructed active and terminal escrow history, but production use requires stronger synchronization behavior.

The recovery design included:

- finalized block depth
- canonical checkpoint block hash
- incremental scanning
- reorganization detection
- scanner concurrency lock
- scheduled synchronization

---

### 3. Vercel and PostgreSQL Planning

Because the frontend includes server routes, dispute metadata, and indexer APIs, deployment requires more than static frontend hosting.

The planned Vercel configuration included:

- server-only `DATABASE_URL`
- protected cron endpoint
- `CRON_SECRET`
- once-daily Hobby plan schedule
- read-triggered catch-up for fresher history

---

### 4. Pre-Sign Safety Plan

I planned a shared preflight that would run immediately before wallet signing.

It would verify:

- selected network genesis
- deployment CellDep availability
- deployed code hash
- current escrow outpoint status
- escrow capacity, scripts, and data
- recipient lock script

---

## 🧠 Key Learnings

### 1. Deployment Metadata Is Part of the Security Boundary

A correct contract does not help if the frontend builds transactions against stale or incorrect deployment data.

### 2. History Requires Canonical Chain Awareness

An indexer must know whether its last processed block still belongs to the canonical chain.

### 3. Release Readiness Needs Evidence

A release decision should be based on recorded tests, transaction hashes, reproducible artifacts, and independent review.

---

## 🚧 Current State

The security direction was clear, but the production milestones still needed implementation and commits.

Mainnet remained gated while testnet deployment and recovery requirements were being formalized.

---

## 🔜 Next Steps

- update frontend testnet deployment metadata
- verify the deployed binary hash
- implement persistent dispute authorization
- add canonical indexer checkpoints and Vercel cron
- add transaction preflight checks
- create a public testnet acceptance record

---

## 💡 Reflection

Week 31 moved the project from feature thinking toward operational thinking.

For an escrow system, correctness must cover the contract, transaction builder, indexer, database, deployment configuration, and recovery process together.

