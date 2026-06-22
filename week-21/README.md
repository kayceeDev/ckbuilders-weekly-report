# Nervos Builder Track — Weekly Report (Week 21)

**Name:** Ekene Nwobodo  
**Focus:** Direct Arbitrator Resolution, Chain-Time Refund Safety, and Indexer-Backed Escrow History  
**Week Ending:** 20-06-2026

---

## 🎯 Overview

Week 21 focused on moving the escrow product from live-cell discovery toward a more reliable product history model.

The work this week improved:

- direct arbitrator resolution from the product UI
- refund eligibility checks using chain time
- active and past escrow history presentation
- recovery of closed escrows after their live cells are consumed
- indexer-backed escrow history scanning
- Postgres-ready persistence for escrow records

This was an important week because it exposed one of the biggest product gaps in the escrow workflow: live cells alone are not enough for a real user history experience.

Once an escrow is completed, cancelled, refunded, or resolved, the live cell may disappear. The product still needs to remember that escrow as a receipt and show it to the buyer, seller, or arbitrator later.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Next.js Development Stabilization

The week started with cleanup around the product shell and route behavior.

Work completed:

- refreshed generated Next.js route type references
- switched local development to the webpack dev path for better stability
- reduced friction from development tooling failures while working on product routes
- kept the frontend focused on reliable iteration instead of fighting the dev server

This was small compared to the feature work, but it mattered because unstable local tooling slows down every wallet, route, and escrow-flow debugging session.

---

### 2. Direct Arbitrator Resolution

The product detail page was improved so arbitrators can resolve disputed escrows more directly.

Work completed:

- added direct arbitrator resolution support in the product flow
- connected disputed escrow state to resolution actions
- kept Studio available as a fallback for raw/debug operations
- aligned the product action model with the contract's `ResolveToBuyer` and `ResolveToSeller` paths

This made the arbitrator role more useful in the actual product experience instead of leaving resolution mostly inside the operator tooling.

---

### 3. Chain-Time Refund Safety

Refund handling was tightened so refund availability is based on CKB chain time instead of only browser/local time.

Work completed:

- gated refund behavior with chain timestamp context
- improved refund eligibility checks for funded escrows after deadline
- reduced the risk of showing refund actions before the contract would accept them
- kept product messaging closer to actual on-chain validation

This was a useful reminder that frontend time and chain time are not the same thing. For a contract-enforced deadline, the product needs to follow chain reality.

---

### 4. Escrow History UI Polish

The escrow list experience was reorganized around active and past escrow records.

Work completed:

- improved active escrow presentation
- improved past escrow history presentation
- moved closed escrows into a history-style flow
- made completed, cancelled, refunded, and resolved escrows feel more like receipts
- reduced the feeling that every escrow was still an active task

This helped the product feel more like a wallet-aware escrow ledger instead of a temporary list of cells.

---

### 5. Indexer-Backed Escrow History

A major part of the week was spent adding the foundation for persistent escrow history.

Work completed:

- added indexer-backed escrow history APIs
- added normalized escrow records and timeline/event modeling
- added a scanner for CKB escrow history
- added stable escrow IDs based on original creation outpoints
- added support for active and terminal escrow states
- added indexed detail recovery for past escrows

This work was important because browser storage is not enough for production-grade history. If a user changes device, clears storage, or reconnects later, the app should still recover escrows they participated in.

---

### 6. Postgres-Ready Persistence

The indexer storage layer was extended beyond in-memory state.

Work completed:

- added Postgres-ready escrow indexer storage
- added persistence for escrow records and timelines
- added fallback behavior when the configured database is unavailable
- added tests around storage behavior and recovery
- prepared the app for deployment environments where API routes need persistent history

This moved the project closer to a production deployment model, especially for Vercel or any hosted frontend/backend environment.

---

### 7. Contract Alignment Without Contract Changes

There was no major contract implementation commit during this specific week.

The frontend work still stayed aligned with the existing contract model:

- escrow state/action codes stayed unchanged
- refund behavior remained deadline-driven
- arbitrator resolution still depended on the arbitrator lock hash fixed at creation
- terminal actions were treated as consumed-cell outcomes rather than mutable state updates

This helped keep the product work grounded in the actual CKB cell model instead of inventing a frontend-only version of escrow state.

---

## 🧠 Key Learnings

### 1. Live Cells Are Not Product History

One of the clearest lessons this week was that live cell discovery and user history are different problems.

Live cells are good for active work, but a real product also needs to answer:

- what did I fund?
- what did I complete?
- what was cancelled?
- which disputes did I arbitrate?
- can I reopen an old receipt?

That requires indexed transaction history, not just current live cells.

---

### 2. Terminal Escrows Need Receipt Thinking

Completed, refunded, cancelled, and resolved escrows should not disappear from the user's point of view.

On CKB, the original cell may be consumed, but the user still expects a record of what happened.

This pushed the product toward a clearer split:

- active escrows are operational tasks
- past escrows are receipts and history

---

### 3. Chain Time Matters for Contract UX

Refund work made it clear that local frontend assumptions can create bad UX if they do not match chain validation.

The app should not encourage a buyer to submit a refund transaction unless the chain context supports it.

That lesson applies beyond refunds. Any contract-dependent action should be shown only when the app has enough chain context to make the state believable.

---

### 4. Backend Support Is Necessary for a Serious Escrow App

The indexer work made the architecture clearer.

A fully useful decentralized escrow app still needs off-chain support for:

- discovery
- history
- receipts
- evidence metadata
- status recovery

The contract enforces value movement, but the product needs an indexer/API layer to make that enforcement understandable and usable.

---

## 🚧 Current State

By the end of Week 21, the project now demonstrates:

- direct product-level arbitrator resolution
- chain-time-aware refund gating
- active and past escrow history presentation
- indexer-backed escrow history recovery
- CKB scanner support for escrow transactions
- Postgres-ready persistence for indexed records
- better recovery of terminal escrow detail pages

Still missing:

- full polish around dispute evidence and arbitrator review
- stronger route handling between active live cells and indexed receipts
- final UI cleanup so product pages feel less protocol-heavy
- more end-to-end verification across all wallet roles

---

## 🔜 Next Steps

- add a dispute evidence and arbitrator review experience
- improve route stability for active and terminal escrows
- reduce duplicate records between live and indexed escrow sources
- make homepage and escrow-list counts include historical records accurately
- keep testing settlement paths against the deployed contract

---

## 💡 Reflection

Week 21 felt like the week where the product stopped treating escrow history as a frontend convenience and started treating it as infrastructure.

That shift matters. A decentralized escrow app is not only about locking and releasing funds. It also has to help participants remember, prove, and understand what happened across the full lifecycle of a deal.
