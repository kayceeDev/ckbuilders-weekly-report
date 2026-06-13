# Nervos Builder Track — Weekly Report (Week 20)

**Name:** Ekene Nwobodo  
**Focus:** Escrow Listing Flow, Create-to-List Navigation, and Contract-Aligned Settlement Refinement  
**Week Ending:** 13-06-2026

---

## 🎯 Overview

Week 20 focused on connecting the buyer-facing product flow more tightly from creation through escrow browsing, while continuing to refine settlement behavior against the live deployed contract.

The work this week improved:

- dedicated escrow listing flow
- navbar and mobile navigation structure
- self-escrow prevention in the create flow
- refund-after-deadline buyer experience
- runtime settlement diagnostics for refund and release

This week was important because it connected more of the product into a coherent user journey while exposing the final contract/runtime gaps that still need to be closed.

---

## 🔗 Repositories

- Escrow Frontend / Product Shell  
  https://github.com/kayceeDev/ckb-escrow-test-frontend

- Escrow Contract (Rust / CKB Script)  
  https://github.com/kayceeDev/ckb-escrow

---

## 🏗 What I Built

### 1. Dedicated Escrows Listing Page

The product now has a separate page dedicated to browsing live escrow cards.

Work completed:

- created a new `/escrows` route
- extracted reusable escrow-listing sections/components
- highlighted newly created escrows in the list flow
- linked the list into navbar and wallet-panel navigation
- made create flow redirect into the escrow list experience

This was useful because users often need a place to browse and reopen escrows without being dropped back into the dashboard summary view.

---

### 2. Create Flow Safeguards and Redirect Improvements

The buyer create journey received another round of product hardening.

Work completed:

- prevented buyers from creating escrows against themselves
- validated buyer/seller identity more clearly through lock-hash comparison
- improved post-create redirects toward the escrow listing page
- improved status messaging after create and refresh

This made the create flow more realistic and removed one obvious class of user error.

---

### 3. Refund-After-Deadline Product Behavior Refinement

The funded-after-deadline buyer path was updated so refund feels more immediate in the product.

Work completed:

- treated refund as the primary buyer action after deadline
- adjusted product copy so refund is surfaced more clearly once eligible
- auto-prepared timestamp/header-proof context in the buyer-facing refund flow
- continued tracing live refund failures against the deployed contract rules

This improved the product semantics even though the runtime settlement path still needs additional debugging.

---

### 4. Release-Funds and Settlement Runtime Investigation

A major part of the week was dedicated to understanding why settlement actions still fail live.

Work completed:

- traced the release-funds path through product detail, service, and adapter layers
- investigated escrow input reconstruction and live lock hash type handling
- compared current frontend wiring against the current deployed contract expectations
- refined tests to better reflect the current runtime assumptions

This did not fully resolve the release/refund problems yet, but it narrowed the remaining issues to concrete contract/runtime mismatches rather than vague UI uncertainty.

---

### 5. Navigation and Product Shell Consistency

The buyer-facing shell became more coherent.

Work completed:

- added the escrow list route to the main navbar
- improved wallet-panel quick links
- improved mobile nav descriptions for key product routes
- kept product navigation aligned with the actual live escrow workflow

This helped the app feel more complete as a standalone product shell.

---

## 🧠 Key Learnings

### 1. Product Completion Requires Flow Completion, Not Just Screen Completion

By this point the project has enough screens, but the real work is connecting them into a believable journey.

This week reinforced that users care about:

- where they land after creation
- how they find their escrows again
- whether an action is safe and available
- whether the app explains what the contract is actually doing

That means navigation and post-action flow design matter just as much as individual screens.

---

### 2. Runtime Truth Can Still Diverge From Passing Tests

One of the most important lessons this week was that passing tests and typechecks are necessary but not sufficient.

The live refund and release issues showed that runtime behavior can still diverge because of:

- live deployment metadata usage
- lock reconstruction details
- fee completion behavior
- wallet/runtime preparation
- contract verification rules

That reinforced the value of live end-to-end validation against the deployed contract.

---

### 3. Contract-Aligned UX Is a Moving Target

As the product becomes more honest about contract behavior, the UX also needs to evolve.

This week made it clearer that product language, availability states, and error messaging should reflect what is *actually* possible on chain right now — not what seems intuitive from a generic escrow app perspective.

---

## 🚧 Current State

By the end of Week 20, the project now demonstrates:

- a dedicated escrow listing page
- create-to-list navigation flow
- self-escrow prevention in the buyer create path
- stronger routing and navigation consistency
- clearer buyer-facing refund messaging after deadline
- deeper understanding of the remaining contract-facing settlement issues

Still missing:

- final live fix for refund runtime verification
- final live fix for release-funds transaction/dependency behavior
- end-to-end confirmation that all major terminal settlement actions work against the deployed contract

---

## 🔜 Next Steps

- finish debugging refund and release-funds against the live testnet deployment
- complete the remaining settlement/runtime alignment work
- verify all terminal settlement paths end to end
- continue tightening the dedicated escrow list and detail flow after the settlement layer is stable

---

## 💡 Reflection

Week 20 felt like a bridge between product completeness and protocol completeness.

The frontend is much closer to a coherent buyer-facing escrow product now, but the remaining work is increasingly about making sure every runtime action is as correct on chain as it is understandable in the UI. That is a harder stage of development, but it is also where the product becomes real.
