# Nervos Builder Track — Weekly Report (Week 22)

**Name:** Ekene Nwobodo  
**Focus:** Dispute Evidence, Stable Escrow Routes, Product UI Polish, and Wallet Lifecycle Hardening  
**Week Ending:** 25-06-2026

---

## 🎯 Overview

Week 22 focused on hardening the escrow product around the parts that matter most once real users begin interacting with live escrows.

The work this week improved:

- dispute evidence and arbitrator review
- participant-aware history counts
- duplicate escrow record handling
- post-action refresh and polling behavior
- active vs terminal escrow routing
- closed escrow receipt redirects
- product UI polish
- wallet refresh and reconnect behavior
- contract tooling and settlement test coverage

This was a dense week because the work touched both user experience and protocol correctness. The goal was not just to make the interface look better, but to make it behave more honestly around CKB's cell lifecycle.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Dispute Evidence and Arbitrator Review Flow

The dispute flow was expanded so it is no longer just a raw state transition.

Work completed:

- added dispute evidence review flow
- connected dispute cases to escrow records
- added support for evidence metadata and review context
- hardened dispute metadata handling
- kept the contract unchanged while linking product evidence to on-chain dispute activity

This is important because a real arbitrator needs context before resolving a dispute. The contract can enforce who is allowed to resolve, but the product needs to help the arbitrator understand why they are resolving.

---

### 2. Homepage Counts Including Escrow History

The homepage statistics were updated so they reflect both active and historical escrows.

Work completed:

- included indexed historical escrows in buyer/seller/arbitrator counts
- kept “needs action” limited to active actionable escrows
- merged live and indexed records before counting
- avoided showing view-only escrows in product statistics

This made the dashboard more accurate for users who have already completed or cancelled escrows.

---

### 3. Duplicate Escrow Record Fixes and Polling

The product had to handle the reality that the same escrow can appear from two sources:

- live cell discovery
- indexed history recovery

Work completed:

- deduped live and indexed records that represent the same escrow
- preferred live records for active work
- preserved indexed records for terminal history
- added bounded polling after state-changing actions
- improved refresh behavior after deliver, cancel, complete, refund, dispute, and resolve actions

This improved the user experience because participants no longer need to manually reload or navigate away just to see that an escrow state changed.

---

### 4. Active and Terminal Route Stability

A major part of the week was spent fixing detail routes so actions stay available on active escrows and receipts stay available for closed escrows.

Work completed:

- enabled dispute from stable escrow routes
- recovered live escrow actions from indexed outpoints
- routed active escrows to live outpoints
- avoided encoded output suffix issues on active routes
- redirected completed or cancelled escrows to indexed receipt routes

This was necessary because active escrows and terminal escrows have different routing needs. Active escrows need action context. Closed escrows need read-only receipt context.

---

### 5. Product UI Polish

The customer-facing product UI received a larger cleanup pass.

Work completed:

- reduced protocol-heavy language from user-facing pages
- refined the escrow detail page into more of a deal room
- made active and past escrow views more ledger-like
- improved footer/layout placement across product pages
- made home page cards more minimal and focused
- preserved Studio as the place for protocol and debugging details

This helped separate the product from the operator console. The main app should feel calm and understandable, while Studio can remain technical.

---

### 6. Wallet Lifecycle Hardening

Wallet connection behavior was audited and hardened.

Work completed:

- reproduced a refresh/reconnect bug where wallet discovery disconnected a signer but the reconnect guard skipped reconnecting it
- forced reconnect after wallet refresh invalidates the signer session
- prevented stale async lock-hash updates after wallet switch or disconnect
- cleared wallet-scoped escrow data immediately on disconnect
- added tests for wallet selection and reconnect behavior

This matters because buyer, seller, and arbitrator actions depend entirely on the correct connected wallet context. If the UI thinks a wallet is connected but the signer is stale, actions become confusing or fail silently.

---

### 7. Contract Tooling and Settlement Test Coverage

The contract repo also received important hardening work.

Work completed:

- hardened contract tooling around local development and deployment preparation
- added reproducible build/checksum support
- improved OffCKB-related deployment tooling
- added release settlement test coverage
- kept contract changes focused on verification and confidence rather than changing state/action semantics

This supported the frontend work by making the contract side more reliable to build, verify, and deploy.

---

## 🧠 Key Learnings

### 1. Dispute Resolution Needs More Than a Button

A dispute button can move the escrow into a disputed state, but that is not enough for a usable arbitration process.

The arbitrator needs:

- the escrow terms
- participant statements
- evidence links or metadata
- action history
- a final decision note

This week clarified why dispute UX is a product layer, even when resolution authority is enforced by the contract.

---

### 2. CKB Routing Must Respect Cell Lifecycle

The routing fixes reinforced an important CKB lesson.

An active escrow and a completed escrow are not the same object from the product's point of view.

Active escrows need live outpoints so actions can consume the current cell. Terminal escrows need indexed receipt IDs because the live cell may already be gone.

That difference has to be visible in the frontend architecture even if the user never sees the technical details.

---

### 3. Good UX Requires Correct Wallet State

The wallet lifecycle work showed that wallet connection is not only a visual state.

The product needs the signer to be genuinely ready because every meaningful escrow action depends on it.

This made it clear that wallet refresh, reconnect, network switching, and active lock hash calculation are core product reliability concerns, not just navbar behavior.

---

### 4. Indexer Data and Live Data Need Careful Merging

The duplicate card issue was a good example of how easy it is to confuse users when live and indexed data are both present.

The frontend needs to understand identity across:

- original creation outpoint
- current live outpoint
- indexed terminal receipt

Without that, the same escrow can look like several different escrows.

---

## 🚧 Current State

By the end of Week 22, the project now demonstrates:

- dispute evidence and arbitrator review support
- better homepage statistics using escrow history
- deduped live/indexed escrow presentation
- post-action polling after state changes
- stable active escrow routes
- read-only receipt routing for closed escrows
- cleaner product UI separation from Studio
- hardened wallet refresh/reconnect behavior
- stronger contract tooling and release settlement test coverage

Still missing:

- production-hosted indexer/database validation
- deeper end-to-end testnet runs across all roles and terminal actions
- further polish around evidence storage and file handling
- final Vercel deployment configuration and environment validation

---

## 🔜 Next Steps

- deploy the frontend with proper testnet contract and arbitrator env variables
- verify indexer-backed history against a hosted Postgres database
- run full buyer/seller/arbitrator testnet flows end to end
- continue refining dispute evidence review into a smoother arbitrator workflow
- keep contract deployment metadata and frontend configuration aligned

---

## 💡 Reflection

Week 22 felt like a hardening week.

The project is no longer only about proving that escrow state transitions can exist. It is now about making those transitions usable, discoverable, recoverable, and trustworthy for real participants.

The biggest lesson was that a decentralized escrow app still needs strong product infrastructure around the contract. The contract protects the value path, but the app has to protect the user journey.
