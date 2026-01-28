# How CKB Works — Beginner Notes

This repository contains my first learning notes on **how the Nervos CKB (Common Knowledge Base) works**, written from a beginner’s perspective.

The goal of this document is to explain the core ideas of CKB in **simple, intuitive terms**, without assuming prior blockchain knowledge.

---

## What is CKB?

CKB (Common Knowledge Base) is the **Layer 1 blockchain** of the Nervos Network.

It is the foundation layer where:
- Ownership of CKBytes is recorded
- Digital assets and important data are stored
- Network consensus is enforced using **Proof of Work**

CKB is designed to be **secure, decentralized, and long-term**, acting as a shared source of truth for the entire Nervos ecosystem.

---

## The Cell Model (Core Concept)

Instead of using accounts (like bank balances), CKB uses **Cells**.

A **Cell** is a small container that can hold:
- CKBytes (value)
- Data (tokens, NFTs, contracts, etc.)
- Rules that control how it can be used

Key ideas:
- Cells are **immutable** (they cannot be changed)
- To update data or send funds, a Cell is **consumed**
- New Cells are created to represent the new state

> Old Cells are destroyed (“dead”), new Cells are created (“live”).

---

## Scripts: The Rules of CKB

Each Cell has scripts that define how it can be used:

- **Lock Script**  
  Controls *who* can spend the Cell (usually via a private key)

- **Type Script**  
  Controls *how* the Cell’s data can be used or transformed (optional)

These scripts are validated by the network before any transaction is accepted.

---

## CKB-VM (Virtual Machine)

CKB uses a virtual machine called **CKB-VM** to run scripts.

- Built on the **RISC-V** instruction set
- Executes script logic during transaction verification
- Uses **cycles** to measure computation cost

This keeps execution deterministic, secure, and efficient.

---

## How Transactions Work (Simplified)

1. Select one or more **Live Cells**
2. Unlock them using the correct script
3. Consume them as inputs
4. Create new Cells as outputs
5. Broadcast the transaction to the network
6. Miners include it in a block

Once confirmed, the new Cells become part of the blockchain state.

---

## Why This Design Matters

CKB’s design allows:
- Secure long-term storage of value and data
- Flexible programmability without account complexity
- A strong, battle-tested Proof-of-Work security model

CKB focuses on **ownership of blockchain state**, not just transaction execution.

---

## Learning Status

This repository represents **Lecture 1** of my learning journey into:
- Blockchain fundamentals
- Nervos Network
- CKB architecture and design philosophy

More notes and deeper dives will be added as learning continues.

---

## References

- Nervos Documentation: https://docs.nervos.org
- “How CKB Works” — Getting Started Guide
