# Nervos Builder Track — Weekly Report (Week 27)

**Name:** Ekene Nwobodo  
**Focus:** Backend Planning, Indexer Architecture, and Testnet Readiness  
**Week Ending:** 01-08-2026

---

## 🎯 Overview

Week 27 focused on planning the next stage of the escrow project after the MVP and hackathon work.

The main question this week was how to move from a local/test prototype toward a hosted testnet product that can be used and reviewed properly.

The work this week focused on:

- backend/indexer architecture
- escrow history recovery
- hosted database planning
- testnet readiness
- deployment configuration
- proposal direction for onward funding

This week helped clarify that a real escrow product needs more than just a frontend and contract.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Backend and Indexer Planning

I reviewed why escrow history needs an indexer-backed backend.

The main reason is that terminal escrows are consumed on-chain. Once an escrow is completed, cancelled, refunded, or resolved, it may no longer appear as a live cell.

A product still needs to show that history.

The backend/indexer direction should support:

- active escrow discovery
- past escrow recovery
- stable escrow IDs
- event timelines
- participant filtering
- dispute metadata
- hosted persistence

This is important for cross-device history and real user trust.

---

### 2. Hosted Database Direction

I reviewed the database direction for the frontend/indexer layer.

The preferred path is hosted Postgres, likely through Neon, because it works well with Vercel and gives the project a production-ready persistence layer.

This is better than relying on browser local storage because escrow history should not disappear when a user changes browser or device.

---

### 3. Testnet Readiness Planning

I reviewed what still needs to happen before broader testnet usage.

Important readiness items:

- deployed contract metadata must be correct
- frontend env vars must point to the correct scripts
- wallet network must match the selected chain
- escrow actions must refetch state after submission
- terminal history must be recoverable
- transaction errors must be understandable

This planning helped define the next real milestone.

---

### 4. Onward Funding Direction

I also started thinking about how to shape the next funding proposal.

A strong next phase should focus on:

- testnet validation
- hosted indexer/backend
- security hardening
- dispute flow improvement
- production UX

This feels more realistic than proposing many new product features before the MVP is hardened.

---

## 🧠 Key Learnings

### 1. Backend Does Not Mean Centralized Escrow

Adding a backend/indexer does not mean the escrow becomes centralized.

The contract still controls funds and state transitions.

The backend helps the product recover history, organize dispute metadata, and provide a better user experience.

---

### 2. Terminal State History Is a Product Requirement

In an escrow app, completed deals are not irrelevant.

They are receipts.

Users need to see past deals for trust, records, and dispute history. That means the product needs indexed history, not only live-cell discovery.

---

### 3. Funding Proposals Need Clear Milestones

A good proposal should not only say “continue building.”

It should define a clear phase with measurable outcomes.

For this project, the strongest next milestone is likely:

> Testnet validation, hosted indexer, and production readiness.

---

## 🚧 Current State

By the end of Week 27, the project had a clearer next-stage plan:

- keep the escrow contract as the source of truth
- use backend/indexer for history and metadata
- prepare Vercel and hosted Postgres path
- prioritize testnet validation before mainnet
- shape onward funding around hardening and reliability

Still missing:

- continuous indexer worker
- full deployed testnet lifecycle proof
- stronger dispute API authentication
- final security fixes from review feedback

---

## 🔜 Next Steps

- collect and respond to community review feedback
- harden contract settlement validation
- add authenticated dispute metadata writes
- prepare testnet walkthrough
- refine onward funding proposal

---

## 💡 Reflection

Week 27 helped me see that the project is moving from “can this work?” to “can this be operated safely?”

That is a different kind of work. It is more about reliability, history, security, and deployment than just adding screens.
