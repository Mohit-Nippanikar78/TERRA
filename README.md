<div align="center">

# 🏗️ TERRA

### *Decentralized Real Estate Investment Platform*

[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![ethers.js](https://img.shields.io/badge/ethers.js-v6-2535A0?style=for-the-badge)](https://docs.ethers.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![Mantle Network](https://img.shields.io/badge/Mantle_Network-Blockchain-000000?style=for-the-badge)](https://mantle.xyz/)
[![IPFS](https://img.shields.io/badge/IPFS-Pinata-65C2CB?style=for-the-badge&logo=ipfs&logoColor=white)](https://pinata.cloud/)

<br/>

> **TERRA** is a blockchain-powered real estate investment platform that enables fractional property ownership through tokenization, role-based user journeys for builders and investors, and predictive location betting — all running on the Mantle Network.

<br/>

---

</div>

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [User Roles](#-user-roles)
- [Pages & Navigation](#-pages--navigation)
- [Smart Contract](#-smart-contract)
- [IPFS Integration](#-ipfs-integration)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Available Scripts](#-available-scripts)

---

## 🌍 Overview

TERRA bridges traditional real estate with Web3 by enabling:

- **Fractional ownership** — properties are divided into tokens so investors can participate at any scale
- **On-chain builder profiles** — builders register on the Mantle blockchain with IPFS-stored metadata
- **Real estate betting** — users can place market-prediction bets on location-specific price trends
- **Role-based dashboards** — each user type (Builder, Investor, Owner) gets a tailored experience after connecting their MetaMask wallet

---

## ✨ Key Features

### 🏠 Tokenized Real Estate Marketplace
- Browse premium property listings across the US
- Each property is divided into **100 tradable tokens**
- View detailed property stats: token price, available tokens, annual return, rental yield, and appreciation
- Social sharing support (Twitter, Facebook, link copy)

### 👤 Role-Based User System
| Role | Capabilities |
|---|---|
| **Investor** | Browse marketplace, buy property tokens, track portfolio, receive rental income payouts |
| **Builder** | Register on-chain, list properties, manage token sales, view investor breakdown |
| **Owner** | Manage owned properties and listings |

### 📈 Location Betting
- Bet on real estate market trends for specific US locations (Beverly Hills, Manhattan, Miami Beach, etc.)
- Bet types: **Price Increase**, **Price Decrease**, **Popularity Growth**
- Live stats: price change %, current market value, number of active bettors
- Built on top of smart contract infrastructure on Mantle Network

### 🔐 Wallet Authentication
- MetaMask-first wallet connection with multi-provider support (handles MetaMask + Coinbase Wallet coexistence)
- Persistent wallet session via `localStorage`
- Auto-reconnect on page refresh
- Protected routes require both a connected wallet and a selected role

### 📦 IPFS-Backed Builder Profiles
- Builder logos and JSON profile data are uploaded to IPFS via **Pinata**
- Profile CID is stored on-chain through the `BuilderRegistry` smart contract
- Profiles follow a versioned JSON schema (`builder_profile_v1`)

### 📊 Investor Dashboard
- **Portfolio overview** — total investment, current value, and ROI at a glance
- **My Investments** — token holdings per property with appreciation tracking
- **Wallet & Payouts** — view pending/completed rental income distributions with Mantle explorer links

### 🏢 Builder Dashboard
- **Property Listings** — add, edit, and monitor tokenized properties
- **Investor Management** — see who holds tokens for each property, payout history, and ownership %

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Frontend Framework** | React 19 |
| **Build Tool** | Vite 7 |
| **Routing** | React Router DOM 7 |
| **Blockchain Library** | ethers.js v6 |
| **Styling** | Tailwind CSS 4 |
| **Smart Contract Network** | Mantle Network |
| **Decentralized Storage** | IPFS via Pinata |
| **Fonts** | Orbitron (Google Fonts) |
| **Linting** | ESLint 9 |

---

## 📁 Project Structure

```
TERRA/
└── frontend/
    ├── index.html                     # App entry point (Orbitron font, root div)
    ├── vite.config.js                 # Vite + React + Tailwind config
    ├── package.json
    └── src/
        ├── App.jsx                    # Root router with protected route wrappers
        ├── main.jsx                   # React DOM render entry
        ├── index.css                  # Global styles & Tailwind directives
        │
        ├── abi/
        │   └── BuilderRegistry.json   # ABI for the on-chain BuilderRegistry contract
        │
        ├── context/
        │   ├── WalletContext.jsx      # MetaMask connection, persistence & auto-reconnect
        │   └── RoleContext.jsx        # User role selection (Builder / Investor / Owner)
        │
        ├── utils/
        │   ├── contract.js            # ethers.js contract factory (read/write modes)
        │   └── ipfs.js                # Pinata upload helpers (file + JSON)
        │
        ├── components/
        │   ├── ProtectedRoute.jsx     # Route guard (wallet + role required)
        │   ├── Sidebar.jsx            # Collapsible role-aware dashboard sidebar
        │   ├── builder/
        │   │   ├── BuilderRegister.jsx        # On-chain builder registration form
        │   │   ├── BuilderPropertyListings.jsx # Property CRUD + token tracking
        │   │   └── BuilderInvestors.jsx        # Investor breakdown per property
        │   └── investor/
        │       ├── InvestorPortfolio.jsx       # Portfolio stats & overview
        │       ├── MyInvestments.jsx           # Per-property token holdings
        │       └── InvestorWallet.jsx          # Payout history & transactions
        │
        └── pages/
            ├── HomePage.jsx           # Landing page (hero, marketplace preview, betting preview)
            ├── LoginPage.jsx          # MetaMask wallet connect
            ├── RoleSelectionPage.jsx  # Choose Builder / Investor / Owner
            ├── RegisterBuilderPage.jsx
            ├── RegisterInvestorPage.jsx
            ├── RegisterOwnerPage.jsx
            ├── MarketplacePage.jsx    # Full tokenized property listing
            ├── PropertyDetailsPage.jsx # Property detail + token purchase
            ├── BettingPage.jsx        # Location-based market betting
            └── Dashboard.jsx          # Role-specific dashboard shell
```

---

## 👥 User Roles

### 🔨 Builder
Builders are real estate developers who tokenize and list their properties on TERRA.

1. Connect MetaMask wallet
2. Select **Builder** role
3. Complete on-chain registration (company name, email, about, logo → IPFS → contract)
4. Access the builder dashboard to:
   - List new properties with token configuration
   - Track token sales and revenue
   - View each investor's holdings and payout history

### 💰 Investor
Investors browse the marketplace and purchase fractional token ownership.

1. Connect MetaMask wallet
2. Select **Investor** role (available by default — no on-chain registration required)
3. Access the investor dashboard to:
   - View portfolio performance
   - Track individual property tokens
   - Claim and monitor rental income payouts

### 🏡 Owner
Property owners manage their real estate assets on the platform.

1. Connect MetaMask wallet
2. Select **Owner** role and complete registration
3. Manage owned property listings

---

## 🗺 Pages & Navigation

| Route | Component | Access |
|---|---|---|
| `/` | `HomePage` | Public |
| `/login` | `LoginPage` | Public |
| `/marketplace` | `MarketplacePage` | Public |
| `/marketplace/:id` | `PropertyDetailsPage` | Public |
| `/betting` | `BettingPage` | Public |
| `/select-role` | `RoleSelectionPage` | 🔐 Wallet required |
| `/register/builder` | `RegisterBuilderPage` | 🔐 Wallet required |
| `/register/investor` | `RegisterInvestorPage` | 🔐 Wallet required |
| `/register/owner` | `RegisterOwnerPage` | 🔐 Wallet required |
| `/dashboard` | `Dashboard` | 🔐 Wallet + Role required |

---

## 📜 Smart Contract

TERRA uses the **BuilderRegistry** smart contract deployed on the **Mantle Network**.

| Detail | Value |
|---|---|
| **Contract** | `BuilderRegistry` |
| **Default Address** | `0x9833a6ED541DD4B19E5E5F758fC764EEA6318112` |
| **Network** | Mantle Network |
| **Override via** | `VITE_CONTRACT_ADDRESS` env variable |

### Key Events
- `BuilderRegistered(address indexed builder, string cid)` — emitted when a builder profile is registered on-chain with their IPFS CID

### Contract Interaction
```js
// Read-only (no signer needed)
const contract = await getContract(true);

// Write (requires MetaMask signer)
const contract = await getContract();
```

---

## 🗄 IPFS Integration

Builder profile data is stored on IPFS via **Pinata** using two upload utilities:

```js
// Upload a file (e.g., builder logo)
const cid = await uploadFileToPinata(file);

// Upload a JSON object (e.g., builder profile)
const cid = await uploadJSONToPinata({
  schema: "builder_profile_v1",
  builderAddress: "0x...",
  companyName: "...",
  // ...
});
```

The returned IPFS CID is then stored on the smart contract, creating a permanent, tamper-proof link between the wallet address and the builder's profile data.

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- [MetaMask](https://metamask.io/) browser extension
- A [Pinata](https://pinata.cloud/) account for IPFS uploads
- The Mantle Network added to MetaMask

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/TERRA.git
cd TERRA/frontend

# Install dependencies
npm install
```

### Configure Environment

Create a `.env` file in the `frontend/` directory:

```env
VITE_CONTRACT_ADDRESS=0x9833a6ED541DD4B19E5E5F758fC764EEA6318112
VITE_PINATA_JWT=your_pinata_jwt_token_here
```

### Run Development Server

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 🔑 Environment Variables

| Variable | Description | Required |
|---|---|---|
| `VITE_CONTRACT_ADDRESS` | Deployed `BuilderRegistry` contract address on Mantle | Optional (has default) |
| `VITE_PINATA_JWT` | Pinata JWT for IPFS file & JSON uploads | **Required** for builder registration |

---

## 📦 Available Scripts

Run these from inside the `frontend/` directory:

| Script | Description |
|---|---|
| `npm run dev` | Start local development server (Vite HMR) |
| `npm run build` | Create optimized production build in `dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint across all source files |

---

## 🔗 Adding Mantle Network to MetaMask

| Field | Value |
|---|---|
| **Network Name** | Mantle |
| **RPC URL** | `https://rpc.mantle.xyz` |
| **Chain ID** | `5000` |
| **Currency Symbol** | `MNT` |
| **Block Explorer** | `https://explorer.mantle.xyz` |

---

<div align="center">

Built with ❤️ on the **Mantle Network** · Powered by **IPFS** · © 2024 TERRA

</div>
