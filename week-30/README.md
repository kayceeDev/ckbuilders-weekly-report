# Nervos Builder Track — Weekly Report (Week 30)

**Name:** Ekene Nwobodo  
**Focus:** Security Consolidation, CCC Identity Models, and PostgreSQL Authorization Design  
**Week Ending:** 19-08-2026

---

## 🎯 Overview

Week 30 focused on consolidating the security work from the previous week and studying what was still required for a serverless production deployment.

The main question was no longer only whether a wallet could sign a message. The deeper question was whether the backend could prove that the signature identity maps to the participant's exact CKB lock script.

This was primarily a learning, design, and verification week rather than a commit-heavy implementation week.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🧾 Commit Grouping

No repository commits were recorded for this reporting window.

The week was used to review the Week 29 implementation, study CCC signer behavior, and turn remaining security gaps into implementation milestones.

---

## 🏗 What I Worked On

### 1. CCC Signature Identity Research

I reviewed how CCC represents signatures for different signer families:

- CKB secp256k1
- EVM personal signatures
- Bitcoin ECDSA
- JoyID
- Nostr and other wallet types

The important realization was that verifying a valid signature is only one part of authorization.

The backend must also derive or verify the CKB lock script associated with that signature identity.

---

### 2. Persistent Nonce Design

The initial nonce implementation used process memory.

That works locally but is unreliable for Vercel because separate serverless instances do not share memory.

I designed a PostgreSQL nonce model with:

- hashed nonce storage
- network, escrow, action, and lock-hash scope
- expiration time
- consumed timestamp
- atomic single-use update

---

### 3. Fail-Closed Production Behavior

Another design decision was that dispute authorization must not silently fall back to memory in production.

If PostgreSQL is unavailable, sensitive metadata writes should stop and return a clear service error.

This is safer than accepting weaker authorization during an infrastructure failure.

---

### 4. Test Planning

I expanded the security test plan to include:

- missing and invalid signatures
- wrong participant role
- wrong network
- expired nonce
- concurrent replay
- unsupported signer families
- pending or mismatched CKB transactions

---

## 🧠 Key Learnings

### 1. Serverless State Must Be Shared State

An in-memory map is not a reliable security boundary when requests can reach different server instances.

### 2. Multi-Wallet Support Increases Verification Work

Supporting more wallets is not only a frontend connection task. Each signature family requires a trustworthy identity-to-lock derivation.

### 3. Failing Closed Is Part of Security

A secure feature should become unavailable when its authorization storage is unavailable, instead of falling back to weaker behavior.

---

## 🚧 Current State

The contract payout fix remained stable and the initial signed dispute flow was working.

The next implementation still needed:

- PostgreSQL nonce persistence
- atomic replay protection
- explicit supported-wallet allowlist
- structured API error responses
- committed transaction confirmation

---

## 🔜 Next Steps

- implement the PostgreSQL nonce repository
- add verified CKB, EVM, and BTC identity adapters
- reject unsupported evidence-signing wallets clearly
- require committed dispute and resolution transactions
- rerun frontend and indexer test suites

---

## 💡 Reflection

Week 30 was useful because it separated “a signature was provided” from “the correct participant authorized this request.”

That distinction is essential for a dispute system that users may rely on when funds are locked.

