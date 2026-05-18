# Nervos Builder Track — Weekly Report (Week 16)

**Name:** Ekene Nwobodo  
**Focus:** Network-Aware Deployment, Testnet/Mainnet Separation, and Frontend Network Context  
**Week Ending:** 16-05-2026  

---

## 🎯 Overview

Week 16 focused on making the escrow system more deployment-aware.

The work this week improved:

- testnet and mainnet separation
- contract deployment flow
- frontend network selection
- Studio visibility into active network and deployment state

This was an important step because the escrow product can only be useful if the contract, frontend, wallet, and explorer context all agree on the same CKB network.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Network-Aware Contract Deployment Flow

The contract deployment process was updated so it no longer assumes only testnet.

Work completed:

- replaced the old testnet-only deployment script
- added a network-aware deployment script
- supported separate testnet and mainnet deployer keys
- added explicit mainnet confirmation before deployment
- updated deployment documentation around the new flow

This made the contract deployment process safer and more realistic, especially because testnet and mainnet must never share deployment assumptions.

---

### 2. Testnet and Mainnet Separation

The project now treats testnet and mainnet as separate operating environments.

Work completed:

- added support for `testnet` and `mainnet` deployment targets
- separated deployment output directories by network
- documented how to run testnet deployment by default
- added guardrails for mainnet deployment

This matters because a CKB contract deployment is not just a code artifact. It produces network-specific metadata that the frontend needs in order to build valid transactions.

---

### 3. Frontend Network Selection

The frontend was updated so the product and Studio can understand the active CKB network.

Work completed:

- added frontend network state
- wired testnet and mainnet client selection
- updated Studio overview to show network-specific deployment context
- improved explorer link handling for the active network
- kept wallet and deployment state tied to the selected network

This helped move the frontend away from hidden assumptions and toward a clearer product model.

---

### 4. Studio Deployment Awareness

Studio became more useful as an operator and developer tool this week.

Work completed:

- made deployment state more visible
- improved network switching behavior
- kept deployment profiles separate across environments
- made network context easier to inspect before building transactions

Studio is still useful for debugging and advanced protocol flows, but this work made it less ambiguous and safer to use.

---

## 🧠 Key Learnings

### 1. Deployment Metadata Is Part of the Product

On CKB, deploying the contract is only one part of the job.

The frontend also needs:

- script code hash
- hash type
- cell dep transaction hash
- cell dep index
- correct network context

Without these values, the frontend cannot build transactions that reference the deployed contract correctly.

---

### 2. Testnet and Mainnet Need Hard Boundaries

This week made it clearer that testnet and mainnet should be treated as separate systems.

They can share the same contract logic, but they cannot safely share:

- deployer keys
- deployment records
- explorer links
- address assumptions
- frontend deployment profiles

Adding explicit separation now reduces the risk of confusing environments later.

---

### 3. Frontend UX Should Expose Protocol Reality

Network selection is not only a developer setting.

For a CKB escrow product, network context affects:

- which wallet addresses are valid
- which deployment is active
- where escrow cells are discovered
- which explorer links make sense

The UI has to surface that reality without making the buyer handle raw protocol details.

---

## 🚧 Current State

By the end of Week 16, the project now demonstrates:

- a network-aware contract deployment script
- separate testnet and mainnet deployment handling
- safer mainnet deployment guardrails
- frontend network selection
- Studio awareness of active network and deployment state

Still missing:

- fully deployed and verified frontend metadata for all networks
- live validation of every escrow action path after deployment
- a cleaner buyer-facing flow that does not depend on Studio configuration

---

## 🔜 Next Steps

- deploy the escrow contract to testnet
- capture deployment metadata and wire it into the frontend
- remove buyer dependency on manual Studio deployment setup
- validate create escrow and action flows against the deployed testnet contract

---

## 💡 Reflection

Week 16 was about moving from local assumptions to real deployment thinking.

The main lesson was that a decentralized product needs more than contract logic. It also needs a careful path for deployment metadata, network selection, wallet context, and frontend transaction building to stay aligned.
