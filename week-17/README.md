# Nervos Builder Track — Weekly Report (Week 17)

**Name:** Ekene Nwobodo  
**Focus:** Testnet Deployment, Standalone Product Configuration, and Transaction Capacity Fixes  
**Week Ending:** 24-05-2026  

---

## 🎯 Overview

Week 17 focused on making the buyer-facing escrow product work more independently from Studio.

The work this week improved:

- testnet deployment metadata handling
- standalone product configuration
- create escrow transaction correctness
- wallet and navbar product experience
- separation between real on-chain escrows and seeded previews

This week was important because the product moved closer to a real buyer flow where deployment details are handled by the developer, not by the user.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Testnet Deployment Metadata Prefill

After deploying the escrow contract on testnet, the frontend was updated to include the deployment metadata directly.

Work completed:

- added a typed frontend deployment config module
- prefilled the testnet escrow script code hash
- prefilled the testnet cell dep transaction hash and index
- supported `data2` hash type from the OffCKB deployment output
- kept mainnet unavailable until complete deployment metadata exists

This means the product can now resolve testnet deployment metadata automatically instead of asking the buyer to configure protocol values manually.

---

### 2. Standalone Product Deployment Configuration

The product deployment flow was changed so Studio is no longer a buyer prerequisite.

Work completed:

- added static deployment config per network
- supported optional `NEXT_PUBLIC_*` environment overrides
- kept Studio deployment profiles as developer/admin overrides
- made product deployment resolution automatic
- replaced Studio instructions with product-level network availability states

This is a better product architecture because buyers should only think about seller, arbitrator, amount, deadline, and description.

---

### 3. Create Escrow Capacity Fix

The create escrow transaction builder was fixed to respect CKB occupied capacity rules.

Work completed:

- diagnosed `InsufficientCellCapacity` during escrow creation
- updated the CCC adapter to calculate occupied storage capacity
- made escrow cell capacity equal to escrow amount plus storage deposit
- added a regression test for the capacity calculation

This was an important CKB learning point: the amount being escrowed is not the same as the total cell capacity required to create the escrow cell.

---

### 4. Product UI and Wallet Flow Improvements

The buyer-facing frontend received another round of product polish.

Work completed:

- improved the navbar wallet control
- moved wallet connection into a dropdown-style flow
- reduced scattered wallet controls across the page
- improved spacing and typography for larger screens
- made the product layout more focused on live escrow activity

This made the application feel more like a real product and less like a technical dashboard.

---

### 5. Live Escrow Focus

The frontend was adjusted to reduce confusion between seeded preview data and real on-chain escrow cells.

Work completed:

- removed seeded preview escrows from the buyer-facing home page
- removed the example escrow route from navigation
- updated escrow detail behavior to resolve live fetched escrows
- improved the not-found and loading states for escrow detail pages

This is important because once real testnet data exists, the product should not mix fake preview cases with live contract state.

---

## 🧠 Key Learnings

### 1. Buyers Should Not Configure Protocol Metadata

A buyer-facing escrow product should not ask users for deployment hashes, cell deps, or lock script configuration.

Those values are developer-owned application configuration.

The buyer flow should stay focused on:

- who the seller is
- who the arbitrator is
- how much is being escrowed
- when the deadline is
- what the escrow is for

---

### 2. CKB Capacity Is Both Value and Storage

The `InsufficientCellCapacity` error made an important protocol rule very clear.

On CKB, a cell's capacity is not only the value being transferred. It also pays for the storage occupied by:

- lock script
- type script
- output data
- cell structure

For escrow creation, the product must reserve enough capacity for both the escrowed amount and the storage deposit.

---

### 3. Deployment Metadata Must Be Typed and Network-Specific

The testnet deployment produced `data2` script metadata.

That revealed why deployment config should be typed carefully and not treated as loose strings.

The frontend now has a better foundation for:

- testnet deployment metadata
- future mainnet metadata
- environment-specific overrides
- safer Studio/admin overrides

---

### 4. Real Product UX Should Prefer Live State

Seeded previews are useful early in development, but they become confusing once live on-chain data exists.

This week made the product more honest by focusing the buyer-facing experience on real escrow cells discovered from the selected network.

---

## 🚧 Current State

By the end of Week 17, the project now demonstrates:

- deployed testnet escrow metadata wired into the frontend
- standalone product deployment config
- buyer-facing create flow that no longer depends on Studio setup
- corrected create escrow capacity calculation
- cleaner navbar wallet connection flow
- product pages focused on live on-chain escrow discovery

Still missing:

- broader live testing of every state transition
- a more complete settlement UX for all payout paths
- stronger persistence and recovery around connected wallet sessions
- production-ready mainnet deployment metadata

---

## 🔜 Next Steps

- continue testing create escrow against the live testnet deployment
- verify delivery, dispute, cancellation, refund, and resolution paths
- improve wallet persistence and page-to-page connection behavior
- keep Studio for operator workflows while simplifying the buyer-facing product
- prepare a clearer path for mainnet once testnet flows are stable

---

## 💡 Reflection

Week 17 felt like a shift from building screens to building a real network-aware product.

The biggest progress was understanding that the frontend must absorb protocol complexity on behalf of the user. The buyer should not need to know about cell deps, hash types, or occupied capacity, but the product must handle those details correctly for the escrow to work on CKB.
