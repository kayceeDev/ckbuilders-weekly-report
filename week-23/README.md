# Nervos Builder Track — Weekly Report (Week 23)

**Name:** Ekene Nwobodo  
**Focus:** Deployment Planning, Environment Configuration, and Product Readiness Review  
**Week Ending:** 04-07-2026

---

## 🎯 Overview

Week 23 focused on preparing the escrow product for deployment outside the local development environment.

The work this week was less about adding new contract behavior and more about checking whether the full system was ready to be hosted, configured, and explained clearly.

The work this week improved:

- Vercel deployment planning
- environment variable strategy
- hosted Postgres/indexer planning
- frontend and contract configuration clarity
- understanding of how arbitrator configuration should work in production
- separation between public contract metadata and private server credentials

This week was important because a working local product is not the same as a deployable product. The project needed a clearer path from local testnet development to a hosted frontend with persistent escrow history.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Vercel Deployment Plan

A major part of the week was spent reviewing how the frontend should be deployed as a monorepo app.

Work completed:

- reviewed the frontend monorepo structure
- confirmed the deployable app lives in `packages/frontend`
- confirmed shared workspace packages are still required at build time
- planned Vercel root/build/output settings
- clarified why production should use `npm run build`, not `npm run dev`

The recommended deployment setup became clearer:

- root directory remains the repository root
- Vercel installs from the workspace root
- root build command builds shared packages before the Next.js frontend
- Vercel serves the generated Next.js output automatically

This helped reduce deployment confusion and made the frontend repo easier to prepare for hosting.

---

### 2. Environment Variable Review

The frontend configuration was reviewed to confirm how contract and arbitrator metadata are loaded.

Work completed:

- checked how `NEXT_PUBLIC_CKB_ESCROW_*` variables are read
- confirmed testnet contract metadata can be supplied through env vars
- confirmed the default platform arbitrator can be supplied through env vars
- clarified which variables are safe to expose publicly
- clarified that database credentials must remain server-side

This was important because contract deployment metadata is public, but database credentials and private keys must never be exposed in the frontend bundle.

---

### 3. Arbitrator Configuration Planning

The arbitrator model was reviewed from both product and contract perspectives.

Work completed:

- clarified that the arbitrator is fixed at escrow creation time
- confirmed the frontend can assign a default platform arbitrator
- confirmed the arbitrator address can come from environment variables
- reviewed how the arbitrator later resolves disputed escrows
- kept the design aligned with the contract's lock-hash authorization model

This made the production path clearer: the platform can start with one default testnet arbitrator address, then later expand to a larger arbitrator pool.

---

### 4. Hosted Database Planning

The indexer-backed history flow requires persistent storage in production.

Work completed:

- reviewed why local browser storage is not enough for escrow history
- confirmed `DATABASE_URL` should be server-side only
- compared hosted Postgres options for Vercel deployment
- selected Neon Postgres as the simplest fit for the current deployment path
- clarified that local Docker hostnames do not work on Vercel

This helped connect the frontend deployment plan with the indexer-backed history requirement.

---

### 5. Production Readiness Review

The system was reviewed as a full product instead of isolated screens or scripts.

Areas reviewed:

- product routes
- wallet connection behavior
- indexer status endpoint
- active and past escrow discovery
- contract metadata configuration
- deployment metadata mapping from contract repo to frontend repo

This review made the next documentation and UI polish pass more obvious.

---

## 🧠 Key Learnings

### 1. Deployment Configuration Is Product Infrastructure

This week made it clear that deployment configuration is not just an operations detail.

For this escrow app, environment variables decide:

- which contract the app uses
- which arbitrator is assigned
- which network is available
- whether history can persist across devices

That means deployment configuration directly affects user trust.

---

### 2. Public Metadata and Secrets Must Stay Separate

The contract metadata can safely use `NEXT_PUBLIC_` variables because it is already public on chain.

Database URLs and private keys are different.

This distinction became important while planning Vercel deployment because it is easy to accidentally treat every environment value the same way.

---

### 3. A Real Escrow Product Needs Backend Support

The indexer work from previous weeks became more practical this week.

A hosted app needs persistent storage so completed and cancelled escrows do not disappear after a browser refresh or device change.

That reinforced the decision to use a hosted Postgres database for the indexer history layer.

---

## 🚧 Current State

By the end of Week 23, the project had a clearer deployment direction:

- Vercel monorepo setup was understood
- testnet contract env vars were identified
- arbitrator env configuration was understood
- hosted Postgres requirement was clarified
- Neon was selected as the simplest database path
- frontend and contract deployment boundaries were clearer

Still missing:

- final README updates for both repos
- final premium UI cleanup before deployment
- actual Vercel deployment
- hosted database connection validation
- full end-to-end testnet run on the deployed app

---

## 🔜 Next Steps

- write deployment-focused READMEs for both repos
- polish the frontend UI before public testing
- configure Vercel environment variables
- connect hosted Postgres
- deploy and test the product on testnet

---

## 💡 Reflection

Week 23 felt like a deployment-readiness week.

The main lesson was that a decentralized escrow product still needs careful off-chain setup around it. The contract protects value movement, but deployment configuration, indexer storage, wallet setup, and documentation are what make the product usable outside a local machine.
