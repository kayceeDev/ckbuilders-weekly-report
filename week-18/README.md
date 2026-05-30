# Nervos Builder Track — Weekly Report (Week 18)

**Name:** Ekene Nwobodo  
**Focus:** Product Flow Consolidation, Arbitrator Assignment, and Live Escrow Routing  
**Week Ending:** 30-05-2026

---

## 🎯 Overview

Week 18 focused on pushing the escrow frontend further toward a real standalone product flow.

The work this week improved:

- automatic arbitrator assignment
- buyer-facing create flow simplification
- tx-hash-based detail routing
- live escrow discovery and refresh behavior
- responsive wallet and navigation polish

This week felt important because the product moved further away from Studio-style manual setup and closer to a buyer-first experience where the app takes responsibility for protocol details.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Automatic Platform Arbitrator Assignment

The biggest product improvement this week was removing buyer responsibility for selecting an arbitrator.

Work completed:

- added typed arbitrator pool configuration by network
- introduced deterministic arbitrator selection from an active platform pool
- wired the create flow so buyers no longer manually provide arbitrator information
- configured a testnet platform arbitrator for live product use

This aligned the product better with the current contract model, where the arbitrator must already be fixed at escrow creation time.

---

### 2. Buyer Create Flow Simplification

The create flow was streamlined so it looked and behaved more like a real buyer journey.

Work completed:

- removed developer-heavy deployment details from the buyer-facing create page
- reduced unnecessary arbitrator messaging in the core form
- improved form readiness and validation around wallet/network prerequisites
- improved post-create status and live-escrow refresh behavior

This was useful because the create flow should ask the buyer for only the information they actually own.

---

### 3. Live Escrow Detail Routing Cleanup

Routing and escrow detail linking were improved to work more safely with real fetched testnet escrows.

Work completed:

- moved buyer-facing links toward tx-hash-based routing
- reduced dependency on `txHash:index` URLs in normal product usage
- improved escrow detail fallback logic for live cells
- improved the flow after escrow creation so the app can recover when discovery is slightly delayed

This reduced routing friction and made the product feel more stable when working with live on-chain data.

---

### 4. Wallet and Responsive Product Polish

The frontend shell continued to improve in terms of wallet handling and navigation.

Work completed:

- tightened wallet controls in the navbar
- improved mobile navigation and page-level consistency
- continued responsive polish across buyer-facing layouts
- removed more buyer-facing debug or operator distractions

This helped the app feel less like a mixed developer console and more like a focused escrow product.

---

## 🧠 Key Learnings

### 1. Escrow UX Should Hide Operational Complexity

A buyer-facing escrow app should not expose every protocol and operations choice directly to the user.

This week reinforced that the product should absorb complexity around:

- deployment metadata
- arbitrator assignment
- routing recovery
- wallet context persistence

while still staying faithful to contract truth.

---

### 2. Deterministic Assignment Is a Good MVP Trade-Off

This week clarified that deterministic platform assignment is a strong MVP decision.

It avoids:

- buyer confusion
- open registration complexity
- backend orchestration overhead
- randomness or fairness claims that are not yet implemented properly

while still fitting the contract’s requirement that the arbitrator be fixed at create time.

---

### 3. Real Product Routing Has Different Requirements Than Demo Routing

As soon as the app started leaning on live escrow cells, routing behavior became much more important.

It is easy to create a detail route for a demo record, but live routing needs to handle:

- delayed discovery
- alternate identifiers
- refresh and fallback states
- wallet/network context mismatches

This week helped make that difference clearer.

---

## 🚧 Current State

By the end of Week 18, the project now demonstrates:

- a platform-assigned arbitrator model in the product flow
- a simpler buyer create experience
- safer live escrow routing behavior
- cleaner responsive navigation and wallet handling

Still missing:

- complete live validation of all settlement actions
- stronger payout and refund runtime handling
- a more complete buyer-facing escrow action lifecycle after delivery/dispute

---

## 🔜 Next Steps

- continue validating product actions against the live deployed contract
- improve settlement and refund handling for real escrow cells
- keep reducing remaining Studio-style friction in the buyer flow
- strengthen action-specific UX around delivered, disputed, and closed escrows

---

## 💡 Reflection

Week 18 felt like a product-shaping week.

The biggest progress was not just adding more features, but deciding what the buyer should *not* have to think about. Moving arbitrator assignment, deployment complexity, and route recovery logic behind the product made the escrow flow feel more intentional and closer to how a real user would expect it to behave.
