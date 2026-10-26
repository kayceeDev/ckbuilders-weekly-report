# Nervos Builder Track — Monthly Report (October 2026)

**Name:** Ekene Nwobodo  
**Focus:** Reorganization Recovery, Production Persistence, and Public Testnet Readiness  
**Month Ending:** 31-10-2026

---

## Overview

October focused on closing the remaining operational gaps identified after the escrow MVP security review.

The contract payout vulnerability and dispute authorization work had already established a stronger security baseline. The remaining questions were about recovery and deployment behavior:

- Can indexed escrow history recover safely from a CKB reorganization?
- What happens to dispute evidence when its on-chain transaction disappears?
- Will a Vercel deployment use persistent PostgreSQL storage, or silently lose state in memory?
- Is the project ready for a structured real-wallet testnet acceptance run?

This month converted those questions into tested implementation and a clearer public testnet release gate.

---

## Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## Commit Grouping

### Frontend and Indexer Repository

| Commit | Milestone |
| --- | --- |
| `c67b9c8` | Rebuild canonical escrow history atomically and reconcile orphaned dispute metadata |
| `4326b03` | Require persistent indexer storage in production and support Vercel Postgres variables |
| `c99e3a0` | Record deployment guidance, acceptance results, and the project review response |
| `0f06416` | Classify direct PostgreSQL failures without mislabeling CKB RPC errors |
| `eed20bc` | Record the successful deployed canonical indexer recovery |

### Contract Repository

No new contract logic was required during this October milestone.

The existing security fix remains the contract baseline:

- `bbace18` validates terminal settlement using recipient net capacity gain.
- `d5cfee1` records the reproducible release and debug binary checksums.

---

## What I Built

### 1. Atomic Canonical Indexer Recovery

The indexer recovery path was changed so a chain rebuild no longer deletes live production history before the replacement snapshot is ready.

The new flow:

1. scans finalized CKB history into temporary in-memory storage
2. rebuilds escrow records from deployment block `22272848`
3. replaces escrows, events, and the canonical checkpoint in one PostgreSQL transaction
4. rolls the entire operation back if any snapshot write fails

The scanner also stores event block hashes and treats a checkpoint below the deployment block as invalid.

This is important because an indexer should never expose a partially rebuilt view of user escrow history.

---

### 2. Dispute Metadata Reconciliation

Dispute evidence is off-chain metadata linked to on-chain transactions. A chain reorganization can therefore invalidate the dispute or resolution transaction while the evidence still exists.

The recovery process now:

- preserves participant evidence
- marks a missing dispute transaction as `orphaned`
- marks a missing arbitrator decision transaction as `orphaned`
- returns the dispute to an open review state when a resolution disappears
- restores confirmed status when the matching canonical transaction reappears

The product detail page displays a clear warning and pauses arbitrator resolution while the dispute is not canonical.

---

### 3. Production PostgreSQL Fail-Closed Behavior

The Vercel deployment can now use either:

- `DATABASE_URL`
- `POSTGRES_URL`

`DATABASE_URL` takes precedence when both are present. Both variables remain server-only.

Production no longer falls back to process memory when PostgreSQL is missing or unavailable. Escrow history, indexer status, cron synchronization, nonce issuance, and dispute metadata APIs return a structured `503` error instead.

Memory storage remains available only for local development and tests.

This prevents a serverless deployment from appearing healthy while silently losing state between function instances.

---

### 4. Verification and Review Preparation

The completed automated verification included:

- all workspace TypeScript checks
- 111 frontend/shared-package tests
- Next.js production build
- atomic rollback regression tests
- evidence preservation and orphan reconciliation tests
- Vercel `POSTGRES_URL` configuration tests
- production fail-closed tests

A response document was also prepared for the CKBuilder project review issue. It explains which findings are fixed, which commits contain the fixes, and which release gates remain pending.

---

## Key Learnings

### 1. Reorganization Safety Is About Atomic Visibility

Detecting a changed block hash is only the first part of recovery.

The replacement state must be built completely before production records are changed. Otherwise users can see missing or inconsistent escrow history during a rebuild.

### 2. Off-Chain Evidence Needs Chain-Aware Status

Evidence can remain useful even when the transaction that created the dispute is reorganized out.

Deleting the evidence would lose participant work. Treating it as confirmed would be misleading. An explicit orphan status preserves the record while communicating the actual chain state.

### 3. Serverless Memory Is Not Persistent Storage

An in-memory fallback is useful during local development, but it is unsafe as a production recovery strategy on Vercel.

Failing clearly is better than returning incomplete history or accepting authorization state that another function instance cannot see.

### 4. Automated Verification and User Acceptance Are Different Gates

The automated suite now covers the main security and recovery logic, but the release still needs real buyer, seller, and arbitrator wallets.

The final testnet evidence must include transaction hashes, explorer links, reconnect behavior, and deployed indexer status.

---

## Current State

The escrow MVP now has:

- contract-level recipient net payout validation
- signed and persistent dispute authorization
- committed dispute and resolution transaction verification
- pre-sign transaction safety checks
- finalized canonical indexer checkpoints
- atomic reorganization recovery
- preserved evidence with orphan reconciliation
- Vercel Postgres support with production fail-closed behavior
- a documented public testnet acceptance matrix

The latest frontend commits are now deployed through the canonical Vercel-connected repository. The hosted indexer reported PostgreSQL as active and healthy at finalized block `22888550`, with one successful canonical rebuild and no stored error.

Still pending:

- complete all real-wallet testnet flows
- record transaction hashes and explorer links
- obtain independent review of the final hardening commits

Mainnet remains disabled.

---

## Next Steps

- run create, deliver, complete, cancel, refund, dispute, and both resolution flows
- reconnect all three participant wallets in fresh browser sessions
- update the CKBuilder issue with the prepared review response
- request independent review of the October hardening commits
- use the completed acceptance evidence to support the next funding proposal

---

## Reflection

October moved the project from feature security into operational security.

The main lesson was that an escrow product is not ready only because its contract and transaction builder work. It also needs durable authorization, recoverable history, honest chain status, and a release process that proves complete user journeys with real wallets.
