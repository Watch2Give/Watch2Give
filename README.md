# Watch2Give — Transforming Attention into Real Impact

**Watch2Give** is a fully on-chain, Polkadot-native dApp that connects advertisers, viewers, and real-world vendors through smart contracts, enabling ad engagement to fund verified donations.

Built entirely on **Astar Network** using **ink!** smart contracts and Rust-based infrastructure (via `cargo`), this project is designed for **long-term decentralization**, **on-chain trust**, and **cross-chain scalability** — going beyond simulation or short-term proof-of-concepts.

---

## What Makes It Special

- Viewers **earn** tokens by watching ads
- They can **donate** tokens to local vendors (like snack carts, schools, shelters)
- Vendors **redeem** tokens for stablecoins after submitting **photo proof**
- Airdrops are triggered based on **vendor holding metrics**
- All transactions, proofs, and flows are **recorded on-chain**

---

## Why We Built It with Cargo & Ink!

While hackathon guides recommended using **Remix**, we faced limitations for long-term vision:

✅ **We chose `cargo` and `ink!` for full control** over the smart contract suite  
✅ **Deployed on Polkadot-native chains (AssetHub/Astar)**  
✅ **Tightly integrated with off-chain AI verification and backend orchestration**

It took extra time, but this decision future-proofs Watch2Give for real-world deployment and ecosystem growth.

---

## Smart Contract Architecture

### 🔹 1. `watch2give_manager` (Main Logic)
- Registers vendors and watchers
- Logs engagements + proof hashes
- Distributes rewards
- Interfaces with DeFi (e.g. ArthSwap)
- Calculates holding metrics and triggers airdrops

### 🔹 2. `give_token` (PSP22)
- A standard ink! PSP22 token (`$GIVE`)
- Minted/burned only by `watch2give_manager`
- Used for donations and airdrop rewards

---

## 🪙 Token Flow

| Token      | Role                                                  |
|------------|-------------------------------------------------------|
| `xcUSDT`   | Advertiser deposits (via XCM to Astar)                |
| `$GIVE`    | Minted reward token, used to donate and claim airdrops|

---

## Full Flow

1. **Advertisers deposit** `xcUSDT`
2. Smart contract **mints $GIVE** for users
3. **Viewers watch ads → earn tokens**
4. They **donate** tokens to vendors
5. **Vendors submit photo proof** (verified via AI)
6. Contract **logs timestamp, updates metrics**
7. Vendors **redeem** tokens → stablecoin
8. **Airdrops** go back to viewers based on vendor engagement

---

## On-Chain Methods

| Function | Role |
|----------|------|
| `record_engagement(watcher, vendor, proof)` | Logs viewer-vendor donation |
| `notify_cashout()` | Vendor redeems, updates holding score |
| `distribute_airdrops()` | Distributes tokens to watchers |
| `deploy_funds_to_defi()` | Moves xcUSDT to yield vault |
| `mint(to, amount)` | Mints new GIVE tokens |
| `get_vendor_metric()` | Computes TSLC (Time Since Last Cashout) |

---

## AI-Driven Verification

✅ Photo validation using image classification  
✅ Proof hash recorded on-chain  
✅ Smart contract emits `ProofSubmitted` event for backend/frontend to listen

---

## Components Overview

| Layer          | Tool/Language     | Purpose                            |
|----------------|-------------------|-------------------------------------|
| Smart Contracts | ink! (Rust)       | $GIVE token, engagement tracking    |
| Backend        | FastAPI (Python)  | Agent orchestration, API endpoints  |
| AI Agents      | Python (TensorFlow)| Image proof validation, fraud logic |
| Frontend       | Streamlit         | Viewer/vendor dashboards            |
| Transfer       | Polkadot.js + Script | Send transactions on AssetHub   |

---

## ✅ Polkadot-Only Commitment

We did **not** use Moonbeam, Remix, or Ethereum-based tooling. Everything is:

- 🧬 Built for Polkadot (AssetHub/Astar)
- 💡 On-chain logic in ink!
- 🔁 Transfers via Polkadot.js API
- 📦 Deployed via `cargo-contract` and Substrate-compatible node

---

## 📁 Project Structure

watch2give/ ├── contracts/ │ ├── give_token/ # ink! PSP22 contract ($GIVE) │ └── watch2give_manager/ # Main orchestrator contract ├── backend/ # FastAPI backend (agent controller) ├── frontend/ # Streamlit UI (admin & viewer) ├── scripts/ # Polkadot.js API transfer logic ├── ai-monitoring/ # AI image verification pipeline ├── proof-of-giving/ # Proof validation microservice ├── vendor-dashboard/ # Vendor dashboard (streamlit) ├── gamification-api/ # Rewards engine & badge tracking ├── whitepaper.md # Full protocol design & tokenomics └── README.md # You’re here!


---

---

Thank you!
