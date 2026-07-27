# Nervos Builder Track — Weekly Report (Week 26)

**Name:** Ekene Nwobodo  
**Focus:** Post-Hackathon Consolidation, Rust Practice, and CKB Intermediate Concepts  
**Week Ending:** 25-07-2026

---

## 🎯 Overview

Week 26 focused on slowing down after the hackathon and consolidating what I had learned.

Instead of rushing into new features, I spent the week reviewing the escrow system more carefully and strengthening my understanding of Rust and CKB concepts that affect contract correctness.

The work this week improved my understanding of:

- Rust error handling
- contract validation structure
- CKB cells and immutable state transitions
- witness-based actions
- lock hash authorization
- integration test thinking
- why frontend transaction builders cannot replace contract security

This was an important learning week because the project had reached a point where small mistakes could become security issues.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Rust Contract Review

I reviewed the escrow contract flow from the Rust side.

Areas reviewed:

- action decoding
- state transition checks
- participant authorization
- terminal settlement behavior
- refund deadline checks
- how errors are mapped into script return codes

This helped me better understand how the contract makes decisions without relying on the frontend.

---

### 2. CKB Cell Model Consolidation

I spent time revisiting the CKB cell model and how it applies to escrow.

Concepts reviewed:

- cells are immutable
- updating state means consuming one cell and creating another
- terminal actions consume the escrow cell completely
- lock scripts prove ownership
- type scripts enforce business rules
- inputs and outputs must be checked together

This became very relevant when thinking about payout validation and settlement safety.

---

### 3. Testing Mindset Improvements

I also reviewed the difference between unit tests and integration tests.

Unit tests are useful for pure logic like:

- parsing escrow data
- checking state transitions
- validating signer requirements

Integration tests are needed for:

- real transaction shape
- input/output capacity behavior
- witness behavior
- CKB VM execution

This helped me understand why both layers are necessary for CKB contract work.

---

### 4. Frontend and Contract Boundary Review

I reviewed the boundary between the frontend and the contract.

One important lesson was:

> the frontend can build the intended transaction, but the contract must reject unsafe alternatives.

This is very important for decentralized applications because users or attackers can build transactions outside the official UI.

---

## 🧠 Key Learnings

### 1. Contract Security Must Assume Hostile Transactions

The frontend is not the source of truth.

Even if the CCC adapter builds a correct transaction, the contract still has to validate all critical rules independently.

This changed how I think about transaction builders. They are UX tools, not security guarantees.

---

### 2. Inputs Matter as Much as Outputs

Before this week, I mostly thought about where escrow capacity goes in the outputs.

But CKB validation often requires comparing both sides of a transaction.

For settlement, it is not enough to ask:

> did the recipient receive enough output capacity?

A safer question is:

> did the recipient gain enough net capacity from this transaction?

---

### 3. Rust Encourages Explicit Thinking

Rust makes contract code feel strict, but that strictness is useful.

Working with `Result`, enums, and explicit matching made the escrow state machine easier to reason about.

It also made me more careful about the exact meaning of each validation branch.

---

## 🚧 Current State

By the end of Week 26, the project had stronger learning foundations around:

- Rust contract structure
- CKB transaction validation
- input/output accounting
- witness action handling
- contract/frontend responsibility split

Still missing:

- specific hardening implementation from review feedback
- stronger exploit-oriented tests
- full real testnet lifecycle validation
- production backend/indexer reliability

---

## 🔜 Next Steps

- write tests that reproduce security edge cases
- continue reading CKB examples and script patterns
- improve settlement validation
- review dispute metadata authorization
- prepare the project for stronger external feedback

---

## 💡 Reflection

Week 26 was a consolidation week.

It was not as visually exciting as the hackathon week, but it was important. I started seeing the escrow project less as a simple app and more as a protocol that needs careful validation at every boundary.
