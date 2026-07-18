# Nervos Builder Track — Weekly Report (Week 25)

**Name:** Ekene Nwobodo  
**Focus:** Hackathon Sprint, MVP Packaging, and Escrow Product Presentation  
**Week Ending:** 18-07-2026

---

## 🎯 Overview

Week 25 was mainly the hackathon week.

The hackathon ended on 16-07-2026, so this week was focused on turning the escrow work into something that could be explained, tested, and presented as a real MVP direction.

The work this week improved:

- project framing
- product walkthrough thinking
- MVP scope clarity
- review submission preparation
- frontend/contract explanation
- understanding of what still blocks public testnet usage

This was less about adding random new features and more about consolidating the escrow system into a clear product story.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-studio

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Hackathon MVP Packaging

The first focus was preparing the escrow app as an MVP instead of only a development experiment.

Work completed:

- reviewed the buyer/seller/arbitrator flow
- clarified the product is standalone escrow, not a marketplace
- refined the explanation of the contract and frontend split
- prepared the app to be shown as a full workflow
- identified which parts were MVP-ready and which parts still needed hardening

This helped me see the project as a product system instead of a collection of separate contract and UI files.

---

### 2. Product Walkthrough Preparation

I worked through how a reviewer or community member would understand the app from the outside.

The intended walkthrough became:

- buyer creates escrow
- seller marks delivered
- buyer releases funds or opens dispute
- arbitrator reviews dispute
- arbitrator resolves to buyer or seller
- past escrow appears in history

This was important because an escrow product needs to be understandable without explaining every CKB internal detail first.

---

### 3. Review Submission Readiness

The project was prepared for external review.

Work completed:

- summarized the project architecture
- documented current features
- listed planned features
- prepared repository links
- clarified testnet/mainnet status
- identified feedback areas for CKB builders

The goal was to ask for useful feedback rather than only saying that the project exists.

---

### 4. MVP Gaps Review

During the hackathon week, I also reviewed remaining gaps that would matter before public testing.

Important gaps identified:

- full hosted testnet validation
- stronger transaction confirmation UX
- persistent backend/indexer behavior
- more dispute evidence hardening
- stronger security review before mainnet

This helped shape the next stage of the project.

---

## 🧠 Key Learnings

### 1. MVP Does Not Mean Finished

This week made it clear that an MVP should show the core value clearly, but it does not mean every production concern is solved.

For escrow, the MVP needs to prove the workflow:

- funds can be locked
- state can move safely
- participants have clear roles
- disputes have a path forward

Production readiness is a separate step.

---

### 2. Presentation Exposes Architecture Problems

Preparing the project for review forced me to explain the system more simply.

That made it easier to see where the architecture was strong and where it still needed work.

The strong parts were:

- CKB cell-based state machine
- role-aware UI
- separate contract and frontend repos
- indexer-backed history direction

The weaker parts were mostly around hardening and production operations.

---

### 3. Escrow Needs Trust at Every Layer

A user needs to trust more than the contract.

They also need to trust:

- the frontend flow
- the transaction preview
- the dispute process
- the arbitrator path
- the history/receipt view

This is why the product has to be designed carefully around clarity and safety.

---

## 🚧 Current State

By the end of Week 25, the project had a clear MVP direction:

- standalone escrow app
- buyer/seller/arbitrator roles
- CKB contract state machine
- product frontend
- studio/debug tooling
- review submission direction
- hackathon-ready explanation

Still missing:

- full hosted testnet validation
- stronger security review
- production indexer worker
- final dispute evidence hardening
- mainnet readiness plan

---

## 🔜 Next Steps

- collect external feedback
- continue intermediate Rust and CKB learning
- review contract settlement safety
- improve backend/indexer reliability
- prepare onward funding scope

---

## 💡 Reflection

Week 25 felt like a transition from building privately to preparing the project for outside eyes.

The hackathon forced the project to become more understandable. That helped me see that the next phase should not be about adding many features, but about making the existing escrow flow safer, clearer, and more reliable.
