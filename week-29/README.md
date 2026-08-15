# Nervos Builder Track — Weekly Report (Week 29)

**Name:** Ekene Nwobodo  
**Focus:** Contract Payout Security and Initial Dispute Authentication  
**Week Ending:** 12-08-2026

---

## 🎯 Overview

Week 29 focused on implementing the two highest-priority findings from the external MVP review.

The first issue was in the CKB contract settlement logic. The second was in the frontend dispute API. Both issues affected user trust and had to be addressed before broader testnet use.

This week moved the project from security planning into tested implementation.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Net Payout Validation

The terminal settlement contract was changed from checking gross recipient outputs to checking the recipient's actual net gain.

The new rule is:

> recipient output capacity minus recipient input capacity must be at least the escrow amount.

This prevents a recipient from supplying their own input capacity to make an invalid payout appear valid.

Regression tests now cover:

- malicious self-funded payout rejection
- valid settlement without recipient inputs
- valid recipient fee inputs where the final net gain still covers the escrow amount

---

### 2. Signed Dispute Metadata

The dispute API received its first cryptographic authorization layer.

The flow now includes:

- server-issued nonce
- wallet-signed authorization message
- CCC signature verification
- signer address and lock-hash comparison
- replay rejection
- verification of dispute and resolution transaction hashes

This prevents the API from trusting a participant lock hash simply because it was included in a request body.

---

### 3. On-Chain Transaction Matching

Dispute and resolution metadata is now tied to CKB transactions.

The backend checks that a submitted transaction:

- exists on the selected network
- consumes the expected escrow outpoint
- contains the expected escrow action

This keeps off-chain evidence records connected to real escrow state changes.

---

## 🧠 Key Learnings

### 1. Capacity Must Be Measured as Change

The payout issue reinforced that CKB contract validation must compare inputs and outputs together.

Looking only at an output value does not prove that the escrow created that value.

### 2. Public Identity Is Not Authentication

A lock hash identifies a participant, but it does not prove that the API caller controls that lock.

The signed nonce introduced a real ownership proof.

### 3. Contract and API Security Must Reinforce Each Other

The contract secures funds, while the backend secures evidence and decision metadata. Both layers need independent validation.

---

## 🚧 Current State

By the end of Week 29:

- the terminal payout bypass had a tested contract fix
- dispute writes required wallet signatures
- state-changing metadata required matching CKB transactions
- mainnet remained disabled

Further hardening was still needed for persistent nonces, serverless deployment, wallet-specific identity binding, and indexer recovery.

---

## 🔜 Next Steps

- move nonce state from process memory into PostgreSQL
- make nonce consumption atomic across server instances
- verify how CCC signer identities map to CKB lock scripts
- keep deployment metadata synchronized with the frontend
- design reorganization-safe indexer checkpoints

---

## 💡 Reflection

Week 29 showed how external review can improve implementation quality.

The fixes were not cosmetic. They changed how the contract measures settlement and how the backend proves participant authority.

