# Nervos Builder Track — Weekly Report (Week 28)

**Name:** Ekene Nwobodo  
**Focus:** Community Review Feedback, Security Hardening, and Mainnet Gating  
**Week Ending:** 08-08-2026

---

## 🎯 Overview

Week 28 focused on feedback from the project review submission and turning that feedback into a concrete hardening plan.

The review confirmed that the overall CKB architecture is viable, including:

- cell-based escrow state machine
- CCC transaction layer
- role-aware UI
- indexer package
- PostgreSQL-ready schema
- separate Studio interface

However, the review also identified two important issues that must be fixed before public testnet testing:

- terminal payout validation can be bypassed
- dispute APIs do not have cryptographic authorization

This week was important because it moved the project from general MVP improvement into security-driven hardening.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Review Feedback Analysis

I went through the review feedback carefully and separated it into contract-level and frontend/backend-level issues.

The contract issue was about terminal payouts.

The frontend/backend issue was about dispute metadata authorization.

This separation matters because contract bugs and API bugs require different fixes.

---

### 2. Payout Validation Hardening Plan

The contract currently checks whether the recipient output capacity is at least the escrow amount.

The review pointed out that this is not enough because the recipient could also provide their own input capacity.

A safer validation is:

> recipient output capacity minus recipient input capacity must be at least the escrow amount.

This turns the check into a net-gain validation instead of a gross-output validation.

---

### 3. Dispute API Authentication Plan

The dispute API currently accepts participant lock hashes in the request body.

The review pointed out that anyone can copy a public lock hash, so this does not prove wallet ownership.

The planned fix is to add:

- nonce generation
- wallet message signing
- CCC signature verification
- signer address parsing
- signer lock hash matching
- single-use nonce enforcement
- transaction hash verification against on-chain actions

This will make dispute metadata writes much safer.

---

### 4. Mainnet Gating Review

The feedback also reinforced that mainnet should remain gated.

Mainnet should not be enabled until:

- payout vulnerability is fixed
- dispute API authentication is fixed
- integration tests pass
- real testnet flows pass
- deployment metadata is verified
- indexer recovery is tested
- independent security review is completed

This is the right direction because escrow handles user funds.

---

## 🧠 Key Learnings

### 1. Positive Review Still Requires Hardening

The review said the architecture is viable, but that does not mean the project is production-ready.

This is a useful distinction.

A design can be directionally correct and still have specific security issues that must be fixed before users rely on it.

---

### 2. Net Accounting Matters on CKB

The payout issue taught an important CKB lesson.

When validating money flow, outputs alone may be misleading.

For settlement logic, the contract needs to reason about what changed between inputs and outputs.

That is a deeper use of the cell model.

---

### 3. Metadata APIs Need Wallet Proof

The contract protects on-chain state, but the backend stores dispute evidence and decisions.

That metadata still matters for user trust.

If anyone can submit metadata using someone else’s lock hash, the dispute process becomes unreliable even if the contract is safe.

---

### 4. Mainnet Readiness Is a Process

Mainnet should not be treated as just another environment variable.

It requires:

- stronger tests
- security review
- deployment discipline
- monitoring
- recovery planning

This week made that much clearer.

---

## 🚧 Current State

By the end of Week 28, the project had clear external feedback and a concrete hardening direction.

Current strengths:

- viable CKB architecture
- clear product/Studio separation
- role-aware frontend
- indexer-backed history direction
- documented contract/frontend repos

Issues to fix next:

- terminal payout net-gain validation
- dispute API cryptographic authorization
- on-chain transaction verification before storing dispute metadata
- full testnet flow validation
- indexer reorg/recovery demonstration

---

## 🔜 Next Steps

- reproduce the payout bypass with tests
- fix contract terminal settlement validation
- add frontend/API nonce and wallet-signature authorization
- verify dispute and resolution transaction hashes on-chain
- rerun full contract and frontend checks
- update project review thread with the fixes
- keep mainnet gated

---

## 💡 Reflection

Week 28 was one of the most useful weeks because the feedback was specific.

It showed that the project direction is valid, but it also showed where the safety bar must be higher.

For an escrow product, this is exactly the kind of feedback that matters before broader testing.
