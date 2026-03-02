
---

# Nervos Builder Track — Weekly Report (Week 5)

**Name:** Ekene Nwobodo
**Week Ending:** 26-02-2026

---

## 🎯 Focus This Week

This week was exploratory — focused on understanding CKB’s script composition model while experimenting with a lightweight **Escrow Lite** concept.

### Key Areas Explored

* Lock script execution flow
* Script composition vs manual cryptographic verification
* Lock hash as an identity primitive
* Basic conditional locking patterns

---

## 🏗 Escrow Lite (Experimental)

Built a simple conditional lock with two modes:

---

### 1️⃣ Signature Mode (0x00)

```text
[ 0x00 | 32-byte recipient_lock_hash ]
```

**Unlocks only if:**

* The transaction includes an input
* Whose `lock_hash` matches the expected recipient

Signature verification is delegated to the built-in:

```
secp256k1_blake160_sighash_all
```

> The script does not verify signatures directly — it checks that a valid signer already participated in the transaction.

---

### 2️⃣ TimeLock Mode (0x01)

```text
[ 0x01 | 8-byte big-endian timestamp ]
```

**Unlocks only if:**

```
current_block_timestamp >= specified_timestamp
```

Provides a simple freeze-until mechanism.

---

## 🧠 Key Insight

Instead of re-implementing secp256k1 verification inside the script, the correct CKB approach is:

* Compose existing locks
* Enforce business logic on top of validated inputs

This week reinforced the idea that **CKB scripts enforce conditions, not cryptographic primitives**.

---

## 📌 Current State

Escrow Lite is still a minimal conditional lock — not a full escrow workflow yet.

It currently demonstrates:

* Conditional unlock by specific participant
* Time-based unlock

Future iterations may explore refund patterns, dual conditions, or HTLC-style logic.