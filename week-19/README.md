# Nervos Builder Track — Weekly Report (Week 19)

**Name:** Ekene Nwobodo  
**Focus:** Detail Page Simplification, Timeline UX, and Live Settlement Debugging  
**Week Ending:** 06-06-2026

---

## 🎯 Overview

Week 19 focused on making the escrow detail experience clearer for real users while continuing to debug the live settlement paths.

The work this week improved:

- buyer-facing detail page clarity
- timeline presentation and timestamps
- dashboard cleanup and section consistency
- direct action handling for funded and delivered escrows
- diagnosis of settlement failures against the live contract

This week was important because it forced the frontend to be more honest about which product actions were truly ready and which still needed contract/runtime alignment.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Escrow Detail Page Cleanup

The detail page was simplified so it could work as a real buyer-facing screen instead of a protocol-heavy debug surface.

Work completed:

- removed or reduced technical copy that distracted from the actual user journey
- clarified guidance around funded, delivered, disputed, and closed states
- improved action availability messaging
- kept participant role discovery tied to live on-chain lock hashes

This made the page feel more like a product experience and less like an operator console.

---

### 2. Timeline UX Improvements

The timeline and status presentation received another round of work.

Work completed:

- added clearer date/time formatting where the chain data could be recovered
- improved the spacing and presentation of the large signer/timeline area
- reduced visual weight on non-current timeline states
- improved how escrow state progression is explained to the user

This was important because timeline clarity helps users trust what the escrow is actually doing on chain.

---

### 3. Dashboard and Escrow Listing Cleanup

The product shell became more organized this week.

Work completed:

- reduced repeated buyer-facing sections on the dashboard
- improved escrow grouping and list consistency
- prepared a dedicated escrow listing flow separate from the home/dashboard context
- improved the way users return to live escrows after create/refresh

This helped separate “overview” behavior from “browse all escrows” behavior more cleanly.

---

### 4. Live Settlement and Wallet Debugging

A large part of the week was spent debugging real settlement behavior against the live deployed contract.

Work completed:

- investigated cancel and refund contract failures
- checked wallet-specific settlement behavior, including JoyID signing issues
- traced settlement transaction-building paths through frontend, app service, and adapter layers
- compared product assumptions with actual contract validation behavior

This work did not fully eliminate the runtime issues, but it significantly improved understanding of where the remaining problems actually live.

---

## 🧠 Key Learnings

### 1. Product Truth Must Follow Contract Truth

This week reinforced that buyer-facing clarity is only useful if the action semantics are still faithful to the deployed contract.

A button may look simple in the UI, but whether it should be enabled depends on:

- escrow state
- signer role
- output shaping
- lock script expectations
- runtime deployment/dependency alignment

---

### 2. Timeline UX Matters More Once Data Is Real

With real on-chain escrows, the timeline stops being decorative and becomes part of the product’s trust layer.

That means even small improvements like:

- clearer timestamps
- stronger current-state emphasis
- cleaner status explanations

make the product easier to understand and debug.

---

### 3. Settlement Debugging Is Multi-Layered

One of the clearest lessons this week was that settlement bugs can come from several places at once:

- contract validation rules
- transaction builder assumptions
- fee completion behavior
- witness preparation
- wallet-specific signing behavior
- reconstructed runtime cell data

That made debugging slower, but it also improved my understanding of where each class of problem actually belongs.

---

## 🚧 Current State

By the end of Week 19, the project now demonstrates:

- a cleaner and more buyer-facing detail page
- improved timeline presentation with live timestamps
- more consistent dashboard/list behavior
- deeper understanding of the remaining runtime settlement issues

Still missing:

- stable refund execution against the deployed contract
- a fully re-enabled and verified release-funds path
- final cleanup of settlement wiring mismatches between product and runtime

---

## 🔜 Next Steps

- continue debugging refund and release-funds against the actual deployed contract
- verify escrow input reconstruction and settlement dependency handling
- keep improving dedicated escrow listing and post-create navigation flow
- restore blocked actions only after runtime parity is confirmed

---

## 💡 Reflection

Week 19 felt like the week where the product had to grow up.

The UI was no longer the main challenge by itself. The real challenge became keeping the frontend, wallet behavior, and deployed contract aligned while still giving users a clear and calm experience. That tension between product polish and protocol correctness was the main lesson of the week.
