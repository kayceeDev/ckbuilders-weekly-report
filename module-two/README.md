# Module 2 — The CKB Transaction Model (Cells in Action)

This module explains **how transactions work on CKB**, building directly on the Cell Model introduced earlier.  
Instead of accounts and balances, CKB uses **Cells** as the fundamental unit of state, and transactions are simply the process of **consuming old cells and creating new ones**.

Understanding this module means you understand the *core mechanics* of Nervos CKB.

---

## 🎯 What This Module Covers

In this module, we learned:

- What a **transaction** really is on CKB
- How transactions **consume live cells** and **create new cells**
- Why CKB follows the principle of **off-chain computing, on-chain verification**
- How transactions can be **constructed manually**
- The purpose of each major transaction field:
  - `inputs`
  - `outputs`
  - `outputsData`
  - `cellDeps`
  - `witnesses`
- How **transaction fees** are created by capacity differences
- Why miners reject transactions with **zero fees**
- How signatures prove **ownership of cells**

---

## 🧠 Key Concepts Explained Simply

### Transactions Are Cell Transformations
A CKB transaction does not “send money” in the traditional sense.

Instead, it:
1. Takes existing **live cells** as inputs
2. Verifies you have permission to spend them
3. Creates **new cells** as outputs

Old cells become **dead**.  
New cells become **live**.

---

### Fees Are Not Explicit
CKB does not have a separate `fee` field.


Transaction Fee =
Total Input Capacity − Total Output Capacity
If the output capacity equals the input capacity, the fee is 0 and the transaction will be rejected.

### outputsData Is Explicit State
outputs define structure (capacity + scripts)

### outputsData holds the actual stored data

For normal transfers, outputsData is simply:

`"0x"`
Storing more data requires more capacity.

Witnesses Prove Ownership
Signatures live in the witnesses field

Locks verify signatures

Any transaction change requires re-signing

## References
- [Nervos Documentation](https://docs.nervos.org)
- [CKB basic practical operation](https://academy.ckb.dev/courses/basic-operation)