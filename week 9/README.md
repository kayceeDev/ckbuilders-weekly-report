# Nervos Builder Track — Weekly Report (Week 9)

**Name:** Ekene Nwobodo  
**Focus:** Escrow Lite → Escrow System (UI + Protocol + Contract)  
**Week Ending:** 29-03-2026  

---

## 🎯 Overview

This week marked a transition from isolated script experiments to building a **full escrow system prototype** on Nervos CKB.

Instead of focusing only on lock scripts, the work expanded into:

- Contract layer (CKB lock script)
- Protocol / transaction construction layer
- Frontend (operator-facing UI)

The goal was to understand how **real applications are composed on CKB**, not just how individual scripts work.

---

## 🔗 Repositories

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow  

- Escrow Studio (Frontend + Protocol Layer)  
  https://github.com/kayceeDev/ckb-escrow-studio  

---

## 🏗 What I’m Building

### 1. Escrow Contract (Rust / CKB Script)

A composable escrow lock script that supports:

- Signature-based unlock (ownership)
- Time-based unlock (expiry / refund logic)

Key idea:

> The contract does NOT verify signatures itself — it verifies that a valid signer exists in the transaction.

This follows CKB’s design:
- Use existing locks for cryptography
- Build logic through composition

---

### 2. Escrow Studio (Frontend + Protocol Layer)

A UI for interacting with the escrow system.

#### Current Features:

- Wallet connection & discovery
- Escrow creation interface
- Input fields for:
  - Seller lock
  - Arbitrator lock
  - Escrow lock
  - Amount
  - Deadline
- Protocol notes to guide execution flow

#### Key Design Principle:

> The frontend does NOT manually construct low-level script bytes.

Instead:
- Delegates logic to a **protocol/service layer**
- Keeps UI clean and less error-prone

---

## 🧠 Key Learnings

### 1. CKB Apps Are Multi-Layered

Building on CKB is not just writing scripts.

You need:

- **Lock Script** → enforces rules  
- **Transaction Builder** → constructs valid transactions  
- **Frontend/UI** → user interaction  

---

### 2. Script Composition > Rewriting Crypto

Earlier approach:
- Tried to implement signature verification manually

Current approach:
- Use built-in `secp256k1_blake160_sighash_all`
- Verify participation via lock hash

This is:
- Safer  
- More efficient  
- Aligned with CKB philosophy  

---

### 3. Lock Hash = Identity

Instead of accounts:
- Identity on CKB = `lock_hash`

This simplifies:
- Authorization logic  
- Escrow participant validation  

---

### 4. Separation of Concerns

Clear boundaries emerged:

| Layer        | Responsibility |
|-------------|----------------|
| Contract     | Validate rules |
| Protocol     | Build transactions |
| Frontend     | User interaction |

---

## 🚧 Current State

The system is **not production-ready**, but demonstrates:

- Conditional escrow locking  
- UI-driven escrow creation flow  
- Early protocol abstraction  

Still missing:

- Full transaction submission flow  
- Dispute / arbitrator logic  
- Refund paths  
- Multi-party coordination  

---

## 🔜 Next Steps

- Complete transaction building pipeline  
- Integrate signing + submission  
- Implement dual-condition escrow (signature + timelock)  
- Introduce arbitrator logic  
- Improve UX for escrow lifecycle (create → operate → release)  

---

## 💡 Reflection

This week shifted my understanding from:

> “How do I write a CKB script?”

to:

> “How do I build a complete system on top of CKB?”

That shift is critical for building real applications.

### Screenshots

![](./screenshots/escrow%20studio.png)