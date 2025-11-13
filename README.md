### 🪙 Blockchain DevOps Demo

This project demonstrates how **DevOps principles** can be applied to **blockchain development** by automating the testing and deployment of an Ethereum smart contract using **GitHub Actions**.
It showcases a CI/CD pipeline that runs tests automatically on every push and deploys the contract to the **Sepolia testnet** when changes are merged into the `main` branch.

---

### ⚙️ Tech Stack

| Component          | Purpose                                                                                 |
| ------------------ | --------------------------------------------------------------------------------------- |
| **Hardhat**        | Ethereum development environment for compiling, testing, and deploying smart contracts. |
| **Solidity**       | Language used to write smart contracts.                                                 |
| **TypeScript**     | Used for Hardhat configuration and scripts.                                             |
| **Mocha / Chai**   | Testing framework for smart contracts.                                                  |
| **GitHub Actions** | CI/CD pipeline automation (build, test, deploy).                                        |
| **Infura**         | RPC provider for connecting to the Sepolia blockchain without running your own node.    |
| **MetaMask**       | Wallet used to manage keys and hold SepoliaETH for deployment gas fees.                 |

---

### 📂 Project Structure

```
blockchain-devops-demo/
├── contracts/          # Solidity smart contracts
│   └── Counter.sol
├── ignition/           # Hardhat Ignition deployment modules
│   └── modules/Counter.ts
├── scripts/
├── test/               # Mocha tests for the contract
├── hardhat.config.ts   # Hardhat configuration file
├── .github/workflows/  # GitHub Actions workflow (CI/CD)
│   └── ci.yaml
└── README.md
```

---

### 🚀 Setup Guide

#### 1. Prerequisites

* Node.js **v22 or later**
* npm or yarn
* MetaMask wallet (with **Sepolia network** selected)
* Some **SepoliaETH** (from a faucet)
* An **Infura account** and project endpoint

#### 2. Clone the repository

```bash
git clone https://github.com/your-username/blockchain-devops-demo.git
cd blockchain-devops-demo
```

#### 3. Install dependencies

```bash
npm install
```

#### 4. Configure environment variables

You have **two options** to securely provide your private key and RPC URL to Hardhat:


##### **Option A — Using a `.env` file**
Create a `.env` file in the project root and add:

```bash
SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/YOUR_INFURA_PROJECT_ID
SEPOLIA_PRIVATE_KEY=your_wallet_private_key
```

> ⚠️ Never commit your private key. Use GitHub Secrets for CI/CD.

##### **Option B — Using the Hardhat Keystore (recommended)**

Hardhat provides an encrypted local keystore where you can securely store secrets.

Store your private key:

```bash
npx hardhat keystore set SEPOLIA_PRIVATE_KEY
```

Store your RPC URL:

```bash
npx hardhat keystore set SEPOLIA_RPC_URL
```

List stored secrets:

```bash
npx hardhat keystore list
```

Remove a key:

```bash
npx hardhat keystore delete SEPOLIA_PRIVATE_KEY
```

This method keeps secrets out of .env files and makes setups more secure.

#### 5. Compile and test

```bash
npx hardhat compile
npx hardhat test
```

#### 6. Deploy locally (optional)

```bash
npx hardhat node
npx hardhat ignition deploy --network localhost ignition/modules/Counter.ts
```

#### 7. Deploy to Sepolia manually

```bash
npx hardhat ignition deploy --network sepolia ignition/modules/Counter.ts
```

---

### 🧩 CI/CD Pipeline

The GitHub Actions workflow performs the following automatically:

1. **Checkout code** on push or PR
2. **Install dependencies**
3. **Run tests** using Hardhat
4. **Deploy** to Sepolia when changes are merged into `main`

The workflow file: `.github/workflows/ci.yaml`
It also sets the environment variable:

```bash
HARDHAT_IGNITION_CONFIRM_DEPLOYMENT=false
```

to skip manual confirmation during automated deployments.

---

### 🧠 Goal of the Demo

* Show how **blockchain projects can benefit from DevOps** automation.
* Demonstrate **continuous integration and deployment** for smart contracts.
* Introduce the role of **RPC providers**, **testnets**, and **automation pipelines** in blockchain development.
