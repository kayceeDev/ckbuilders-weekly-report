# Learning Nervos CKB — From First Principles

This repository documents my journey into **blockchain fundamentals**, focused on the **Nervos Network (CKB)**.

The goal:

- Build a strong mental model of CKB
- Learn Nervos architecture from first principles
- Break down complex blockchain concepts clearly
- Progress from foundations to deeper technical work

Each folder represents a weekly learning module.

---

## 📚 Learning Modules

---

### Week 1 — CKB Foundations

**Module One — How CKB Works**

- What CKB is and why it exists
- The Cell model
- Scripts & CKB-VM
- Transaction structure

**Module Two — The Transaction Model**

- Consuming and creating cells
- Off-chain computation, on-chain verification
- Manual transaction construction

➡️ [Week 1](./module-one/) | [Module Two](./module-two/)

---

### Week 2 — Rust & Practical CKB

- Rust fundamentals (ownership, control flow, memory model)
- CKB DApp exercises:
  - Transfer CKB
  - Store data in cells

➡️ [Go to Week 2](./week-two/)

---

### Week 3 — Cryptography & L1 Fundamentals

Strengthened blockchain foundations:

- Public key cryptography & digital signatures
- SHA256 & hash properties
- Proof of Work mechanics
- Block structure & Merkle trees
- CKB architecture (Cells, Locks, Types, VM)

Core mental model reinforced:

- **State → Cells**
- **Ownership → Lock Script**
- **Validation → Type Script**
- **Execution → CKB-VM**

➡️ [Go to Week 3](./week-three/)

---

### Week 4 — Script Consolidation

Focused on deepening understanding of:

- Script execution flow
- Transaction validation lifecycle
- Rust-based CKB script structure

This week emphasized that CKB scripts enforce **conditions**, not application logic.

➡️ [Go to Week 4](./week-four/)

---

### Week 5 — Escrow Lite & Script Composition

Moved from theory to experimentation by building a minimal **Escrow Lite** lock.

Explored:

- Script composition
- Lock hash as identity
- Conditional unlock patterns
- Delegating signature verification to existing system locks

Implemented two modes:

- **Signature Mode** — unlocks if a specified lock hash participates
- **TimeLock Mode** — unlocks after a defined timestamp

Key takeaway:

> Compose existing cryptographic primitives.
> Scripts enforce rules — they don’t re-implement crypto.

➡️ [Go to Week 5](./week-five/)

---

### Week 6 — Architecture Reflection & Mental Model Reinforcement

Week 6 was intentionally used as a reflection and consolidation phase rather than introducing new implementations.

After experimenting with the **Escrow Lite** lock in Week 5, the focus shifted toward strengthening the architectural understanding behind CKB's design decisions.

Key areas revisited:

- The **Cell Model** as a state container
- The role of **Lock Scripts vs Type Scripts**
- How **transaction validation flows through the CKB-VM**
- Why CKB encourages **script composition instead of custom cryptography**
- The relationship between **lock hashes, identities, and transaction participation**

This reflection helped reinforce an important design principle within CKB:

> Scripts should enforce conditions using existing primitives rather than re-implement cryptographic logic.

The week also involved reviewing and refining earlier notes to ensure the explanations remain clear, accurate, and beginner-friendly.

➡️ [Go to Week 6](./week-six/)

---

### Week 7 & 8 — Consolidation, Review & Direction Reset

Used this period to revisit earlier escrow work, strengthen the mental model around script composition, and reset direction before moving into a fuller application build.

➡️ [Go to Week 7 & 8](./week%207-8/)

---

### Week 9 — Escrow System Prototype

Transitioned from isolated script experimentation into a more complete escrow system spanning:

- contract logic
- protocol / transaction construction
- frontend interaction

➡️ [Go to Week 9](./week%209/)

---

### Week 10 — Escrow Infrastructure, Repo Split, and Deployment Preparation

Focused on the foundational work needed to turn the escrow prototype into a more structured system:

- contract hardening
- protocol and service-layer work
- frontend extraction and repo split
- deployment profile support and testnet deployment preparation

➡️ [Go to Week 10](./week-10/)

---

### Week 11 — Frontend Architecture Shift

Moved the frontend into a cleaner product-oriented shell by:

- migrating to a Next.js app structure
- introducing product routes
- separating product-facing and studio/operator surfaces more clearly

➡️ [Go to Week 11](./week-11/)

---

### Week 12 — Product UX, Discovery, and Settlement Preparation

Improved the escrow product experience by:

- refining the buyer-facing interface
- adding mobile navigation
- introducing role-aware escrow discovery
- supporting participant-script-backed settlement preparation

➡️ [Go to Week 12](./week-12/)

---

## 🧠 Learning Philosophy

- First-principles understanding
- Accuracy over hype
- Clear mental models
- Incremental depth

This repository serves as both a **personal learning log** and a reference for developers exploring Nervos CKB.

---

## References

- [Nervos Documentation](https://docs.nervos.org)
- [CKB Academy](https://academy.ckb.dev/courses)

---
