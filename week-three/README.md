# Nervos Builder Track — Weekly Report (Week 3)

**Name:** Ekene Nwobodo  
**Week Ending:** 14-02-2026  

---

## 🎯 Weekly Focus

This week focused on strengthening foundational knowledge required for Layer 1 development on Nervos CKB, specifically:

- Cryptographic primitives underlying blockchain systems  
- Proof of Work and mining mechanics  
- Blockchain data structures  
- Beginning formal L1 Nervos developer training  
- Advancing Rust systems programming skills  

---

## 📚 Technical Study & Progress

### 🔹 Blockchain & Cryptography Fundamentals

Completed structured study on:

#### Public Key Cryptography & Digital Signatures
- Private/public key generation
- Signature creation and verification flow
- Ownership proofs without revealing private keys
- Relevance to transaction authorization in L1 systems

#### Cryptographic Hashing
- Properties of secure hash functions
- SHA256 fundamentals
- Collision resistance and avalanche effect
- Role of hashing in block linking and data integrity

#### Proof of Work & Mining
- Nonce search mechanism
- Difficulty adjustment
- Economic incentives and network security
- How PoW ensures immutability and consensus integrity

#### Blockchain Architecture
- Block structure (header, transactions)
- Merkle trees
- Chain linkage through previous block hash
- Transaction validation lifecycle

This solidified the foundational mental model necessary to reason about L1 protocol design and security guarantees.

---

### 🔹 Nervos CKB — L1 Developer Training

Started the official Nervos Developer Training Course:

https://nervos.gitbook.io/developer-training-course/nervos-basics

Covered:

- CKB architecture overview  
- Cell Model vs Account Model  
- Role of Lock Scripts and Type Scripts  
- CKB’s separation of state and validation logic  
- High-level understanding of how scripts execute in CKB-VM  

Established a working mental model:
- State → Cells
- Ownership → Lock Script
- Validation → Type Script
- Execution → CKB-VM


This reframes blockchain state management away from contract-centric design toward cell-centric composability.