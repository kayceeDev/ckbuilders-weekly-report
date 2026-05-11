# Nervos Builder Track — Weekly Report (Week 15)

**Name:** Ekene Nwobodo  
**Focus:** Wallet Connection, Network Awareness, and Product-State Alignment  
**Week Ending:** 09-05-2026  

---

## 🎯 Overview

Week 15 focused on tightening the connection between the escrow contract, the product frontend, and the agent-assisted development workflow.

The work this week improved:

- connected wallet handling
- testnet and mainnet awareness
- product-level escrow creation flow
- technical understanding of participant identity and settlement requirements

This week felt important because it pushed the project further from a product mockup into a more realistic CKB application flow.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Real Wallet Connection Flow

A major improvement this week was treating wallet connection as a real product feature rather than passive signer discovery.

Work completed:

- improved wallet connection handling in the product app
- made wallet connection part of the main user flow
- connected product behavior more clearly to the active signer
- continued aligning signer-driven actions with the escrow state machine

This made the frontend more realistic, because buyer, seller, and arbitrator actions now depend more clearly on an actual connected participant.

---

### 2. Network-Aware Product Flow

The product flow was extended to handle network context more explicitly.

Work completed:

- added testnet and mainnet awareness to the frontend product workspace
- made product behavior more conscious of deployment and network state
- improved understanding of how address handling differs across environments
- kept the product and studio paths closer to real deployment expectations

This matters because CKB product behavior is not only role-aware, it also has to be environment-aware.

---

### 3. Create Escrow Flow Improvements

The create escrow flow became more technically grounded this week.

Work completed:

- improved the product create flow to better reflect real participant information
- connected create behavior more closely to wallet and network state
- tightened the frontend assumptions around seller and arbitrator identity
- improved the product-side preparation needed before funding an escrow

This made the create flow less of a placeholder and more of a real step toward end-to-end escrow creation.

---

### 4. Shared Product State and Navbar Controls

A useful frontend improvement this week was making core wallet and network state more global and visible.

Work completed:

- moved wallet controls into the top navigation area
- improved visibility of connected state inside the frontend shell
- made the wallet and network controls feel more like product features
- kept the experience aligned with the role-aware product workflow

This was important because wallet and network state affect nearly every meaningful escrow action.

---

## 🧠 Key Learnings

### 1. Product Identity on CKB Must Follow On-Chain Identity

This week reinforced that escrow participants are not abstract application users.

They are represented on chain through scripts and hashes.

That means the frontend must stay aligned with:

- connected signer identity
- participant lock hashes
- actual transaction-building requirements

---

### 2. Role Awareness Is Not Enough Without Network Awareness

Earlier work improved role-aware escrow discovery.

This week added another layer:

> the same role logic must still respect the active network and deployment context.

A user can be a buyer, seller, or arbitrator, but the product still needs the correct network, deployment information, and address interpretation for that role to become actionable.

---

### 3. Settlement Requires More Than Simple Identity Matching

A strong technical insight this week was that lock-hash-based identity is useful, but not always sufficient.

When the frontend moves closer to real settlement and payout behavior, it also has to account for:

- participant script information
- transaction context
- network-correct construction

This helped clarify why some product flows can be direct while others still require more careful preparation.

---

### 4. Agentic Workflows Help Most When Systems Become Layered

This week also deepened my understanding of how to use agents around CKB development.

The more the product involved:

- contract logic
- off-chain transaction building
- wallet state
- frontend role handling

…the more useful agents became as structured collaborators rather than simple code generators.

FiberX-style operational thinking was helpful here because it encouraged reasoning step by step instead of trying to collapse the whole problem into a single pass.

---

## 🚧 Current State

By the end of Week 15, the project now demonstrates:

- stronger wallet-aware product behavior
- explicit testnet and mainnet awareness in the frontend flow
- a more grounded create escrow path
- better visibility of product state through shared wallet and network controls
- improved alignment between contract expectations and product behavior

Still missing:

- full live validation of all settlement paths end to end
- smoother handling of every participant script requirement
- broader live verification across all product actions on deployed environments

---

## 🔜 Next Steps

- continue reducing manual steps in settlement-related flows
- improve end-to-end create and action execution on live deployments
- strengthen deployment-aware product UX further
- keep refining the frontend so it stays beautiful without drifting from contract truth

---

## 💡 Reflection

Week 15 felt like a week of technical alignment.

The main progress was not only in adding UI features, but in making the product behave more honestly with respect to connected wallets, network state, and the underlying CKB escrow model.

That made the system feel closer to a real product and also helped me understand more clearly how agents can support CKB development when the work spans multiple technical layers.
