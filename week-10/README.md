# Nervos Builder Track — Weekly Report (Week 10)

**Name:** Ekene Nwobodo  
**Focus:** Escrow Infrastructure, Repo Split, and Deployment Preparation  
**Week Ending:** 05-04-2026  

---

## 🎯 Overview

Week 10 focused on turning the escrow prototype into a better-structured project.

The main work this week was not about polishing the interface yet. It was about building the foundation needed for a real escrow workflow:

- protocol and frontend restructuring
- frontend extraction into a separate workspace/repo
- contract hardening
- deployment preparation for testnet

This week created the base that later product work depends on.

---

## 🔗 Repositories

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

- Escrow Frontend / Studio  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

---

## 🏗 What I Built

### 1. Contract Hardening

The escrow contract logic was tightened to better validate value flow.

This matters because escrow contracts are not only about checking who can unlock a cell. They also need to enforce that state transitions and value movement remain consistent.

Work completed:

- hardened escrow contract value-flow checks
- improved confidence in the contract side before deployment

---

### 2. Protocol and App Service Layer

The TypeScript side of the system became more structured this week.

Work completed:

- built the escrow protocol layer
- added tests and CCC adapter support
- added an escrow app service facade

This helped separate protocol concerns from UI concerns, which makes the frontend easier to evolve without pushing transaction logic directly into the interface.

---

### 3. Frontend Extraction and Studio Improvements

The frontend moved closer to being its own product surface rather than just a small layer attached to contract experiments.

Work completed:

- added escrow frontend workspace package
- improved escrow frontend workflow
- split the frontend into routed screens
- added studio snapshot import/export
- added tooling for frontend repo split
- extracted the TypeScript workspace into a separate repo

This was a major architectural change. It created clearer boundaries between:

- contract code
- protocol code
- frontend code

---

### 4. Deployment Preparation

The project also moved toward live usage on testnet.

Work completed:

- added frontend deployment profiles
- added testnet deployment workflow
- documented the deployment process and required script metadata

This established the bridge between the deployed contract and the frontend admin/studio flow.

---

## 🧠 Key Learnings

### 1. Structure Matters as Much as Features

As the escrow system grew, it became clear that putting everything in one place would slow development down.

Separating:

- contract
- protocol
- frontend

made the project easier to reason about.

---

### 2. Deployment Data Is Part of the Application

To actually use a deployed script, the frontend needs more than just the idea of the contract.

It needs concrete deployment values such as:

- code hash
- hash type
- dep tx hash
- dep index

Without those, a real integration cannot happen.

---

### 3. CKB App Development Is More Than Script Authoring

This week reinforced that a usable CKB application includes:

- validation logic on-chain
- transaction construction off-chain
- a workflow for users to operate the system

The script is only one layer of the application.

---

## 🚧 Current State

By the end of Week 10, the project could demonstrate:

- a stronger escrow contract
- a structured protocol layer
- a split frontend workspace
- deployment profile support
- a documented path for testnet deployment

Still missing:

- a product-style frontend shell
- smoother user-facing flows
- richer participant interaction patterns

---

## 🔜 Next Steps

- migrate the frontend into a cleaner product shell
- improve the user-facing application structure
- connect deployment and product flows more tightly
- continue moving from studio tooling toward a more complete product experience

---

## 💡 Reflection

Week 10 was mostly foundational work, but it was necessary.

This was the point where the escrow project started becoming an actual system instead of a collection of experiments.
