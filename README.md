# 🎥 Watch2Give

**Watch2Give** is a smart-contract-powered platform that allows advertisers to fund user attention, users to earn and donate crypto rewards, and vendors to create real-world impact — all verified on-chain. Built entirely on the Astar Network using ink! smart contracts, it leverages Wasm execution, DeFi protocols, and AI-driven verification to make every ad engagement meaningful.

---

## 🚀 Key Idea

Watch2Give transforms ad engagement into real-world action. Advertisers pay for attention. Viewers earn and donate rewards. Vendors deliver verified impact. Smart contracts automate the flow, and AI agents ensure trust — all within the Polkadot ecosystem (via Astar).

---

## ⚙️ Smart Contract Architecture (Astar + ink!)

### 1. `watch2give_manager` Contract (Main Logic & Orchestrator)
- Manages:
  - Registered vendors & watchers
  - Engagement records
  - Vendor holding metrics
  - Reward parameters and distribution
  - DeFi deployment data
- Holds:
  - xcUSDT funds from advertisers
  - Yield collected from Astar DeFi protocols
- Core Logic:
  - Engagement validation
  - Reward distribution
  - Cross-contract DeFi interactions
  - Periodic airdrop execution

### 2. `give_token` Contract (PSP22)
- Implements the PSP22 token standard
- Defines the `$GIVE` token
- Minted only by `watch2give_manager`
- Fully backed 1:1 by xcUSDT

---

## 🪙 Tokens Used

| Token      | Role                                                                 |
|------------|----------------------------------------------------------------------|
| `xcUSDT`   | Payment token from advertisers (bridged via XCM to Astar)           |
| `$GIVE`    | Reward/donation token (minted and burned on-chain, PSP22 standard)  |

---

## 🔁 Full Workflow (On-Chain Execution)

### 1. Deployment & Setup
- Deploy `give_token` (PSP22) and `watch2give_manager`
- Configure:
  - Admin roles
  - DeFi protocol whitelisting (e.g. ArthSwap, AstridDAO)
  - Reward parameters
- Fund reward pool with initial $GIVE

### 2. Advertiser Funding
- Advertisers deposit `xcUSDT` via `deposit()` to `watch2give_manager`

### 3. DeFi Vault Deployment
- Admin/keeper triggers `deploy_funds_to_defi()` to earn passive yield
- Contract performs cross-contract call to DeFi protocols

### 4. Yield Harvesting
- Keeper calls `harvest_yield()` periodically
- Contract:
  - Claims or withdraws from DeFi
  - Swaps other tokens to `xcUSDT` or `$GIVE` via DEX if needed

### 5. Engagement Recording
- Off-chain app verifies engagement (e.g. watched ad)
- Backend calls `record_engagement(watcher, vendor, proof)`
- Contract:
  - Checks registration
  - Stores `(watcher, vendor)` + timestamp
  - Allocates $GIVE to selected vendor

### 6. Vendor Holding Metric
- Each vendor's last cashout timestamp is stored
- A live holding score (TSLC: Time Since Last Cashout) is computed via `get_vendor_metric()`
- Watcher rewards are boosted based on this score

### 7. Vendor Cashout
- Vendor approves `GIVE` for swap on ArthSwap (or DEX)
- Swaps `GIVE → xcUSDT`
- Calls `notify_cashout()` to update holding metric

### 8. Airdrop Distribution
- Keeper calls `distribute_airdrops()`
- Contract:
  - Loops through stored engagements
  - Calculates reward amounts based on vendor metrics
  - Transfers $GIVE to watchers from reward pool

---

## 📊 Roles and Components

| Layer              | Responsibility |
|--------------------|----------------|
| **Smart Contracts** | Token management, DeFi, engagement logs, metric calculation, airdrop logic |
| **AI Agents (off-chain)** | Image proof validation, fraud detection, auto-rejection |
| **Keeper Service (off-chain)** | Triggers yield harvesting, airdrops, DeFi deploy |
| **Frontend (Streamlit)** | Admin & user dashboards |
| **Backend (FastAPI)** | Engagement verification, wallet integration, trigger coordination |

---

## ✅ Advantages of Astar-Driven Design

- Fully on-chain engagement and donation logic
- Minimal off-chain trust assumptions
- Yield from DeFi protocols directly feeds rewards
- Real value for real actions — no simulation, no middlemen

---

## 📁 Project Structure (Planned)

watch2give/
├── contracts/
│   ├── watch2give_manager/   # ink! smart contract logic
│   └── give_token/           # PSP22 $GIVE token
├── whitepaper.md             # Full protocol explanation
├── backend/                  # FastAPI orchestration
├── frontend/                 # Streamlit admin/user dashboards
├── docs/                     # Diagrams, tokenomics, design specs
└── README.md                 # You’re here!
<!--
**Watch2Give/Watch2Give** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
