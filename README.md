# Learning Nervos CKB — From First Principles

This repository documents my learning journey into **blockchain fundamentals** with a focus on the **Nervos Network and CKB (Common Knowledge Base)**.

The goal of this repo is to:
- Build a strong mental model of how CKB works
- Learn Nervos architecture from first principles
- Break down complex blockchain concepts in a clear, beginner-friendly way
- Progress from fundamentals to deeper technical topics over time

Each folder represents a **learning module**, with notes written as short, focused explanations.

---

## Learning Modules

### Week 1 - 📘 Module one — How CKB Works (Foundations)
An introduction to the core ideas behind CKB, including:
- What CKB is and why it exists
- The Cell model
- Scripts and CKB-VM
- How transactions work on CKB

➡️ [Go to Module 1](./module-one/)

### Week 1 - Module Two - The CKB Transaction Model (Cells in Action)
- What a **transaction** really is on CKB
- How transactions **consume live cells** and **create new cells**
- Why CKB follows the principle of **off-chain computing, on-chain verification**
- How transactions can be **constructed manually**

➡️ [Go to Module 2](./module-two/)

### Week 2 - Rust and Praticals
 **Rust Programming Language**:

  - Read through the Chapter 1-3 of the [Rust Book](https://doc.rust-lang.org/book/),including:
     
     - Variables and Mutabilty
     - Functions and control flow
     - Data types
     - Brief overview of ownership
     - Stack vs heap memory management
     - Did some rust related exercises.

- **CKB (pratical Exercises)**
  
  - Went through the Build DApp [CKB Docs](https://docs.nervos.org/docs/dapp/transfer-ckb)
    
    - Transfer CKB 
    - Store Data on Cell

---


➡️ [Go to Week 2](./week-two//)


### Week 3 - 🔐 Cryptography, Consensus & L1 Foundations

This week focused on strengthening the **first-principles understanding** required for Layer 1 blockchain engineering.

#### Blockchain & Cryptography Fundamentals

- Public key cryptography and digital signatures  
- SHA256 hashing fundamentals  
- Hash properties (collision resistance, avalanche effect)  
- Proof of Work mechanics (nonce search, difficulty adjustment)  
- Block structure and Merkle trees  
- How immutability emerges from chained hashing  

This deepened my understanding of how blockchain security emerges from cryptography and economic incentives.

#### Nervos L1 Developer Training

Started the official Nervos Developer Training Course:  
https://nervos.gitbook.io/developer-training-course/nervos-basics

Covered:

- CKB architecture overview  
- Cell Model vs Account Model  
- Lock Scripts and Type Scripts  
- CKB-VM execution model  
- Separation of state and validation logic  

This reinforced the idea that on CKB:
- State → Cells
- Ownership → Lock Script
- Validation → Type Script
- Execution → CKB-VM

➡️ [Go to Week 3](./week-three/)

---

### Week 4 - focused on consolidation rather than major implementation.

The primary goal was to revisit foundational concepts, experiment with transaction workflows, and gain deeper clarity around Rust-based script development in the Nervos ecosystem.

➡️ [Go to Week 4](./week-four/)

---

> More modules will be added as learning progresses.

---

## Learning Philosophy

- Beginner-first explanations
- Accuracy over hype
- Understanding *why* design decisions were made
- Notes written to reinforce long-term understanding

This repository is both a **personal learning log** and a **reference** for anyone new to Nervos CKB.

---

## References

- [Nervos Documentation](https://docs.nervos.org)
- [CKB Academy](https://academy.ckb.dev/courses)
