# 🧱 Foundry + Story Protocol Project

This repository sets up a smart contract development environment using **Foundry** and integrates **Story Protocol** for IP asset registration and licensing on-chain.

---

## 📦 Setup Guide

### ✅ Prerequisites

- [Foundry](https://book.getfoundry.sh/) (install via Git Bash or WSL on Windows)
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/) (⚠️ required — avoid npm due to resolution issues)

---

### 🔧 Installation & Initialization

#### 1. Install Foundry

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

#### 2. Initialize Project

```bash
forge init
cd your-project
yarn init
```

#### 3. Replace `foundry.toml`

```toml
[profile.default]
out = 'out'
libs = ['node_modules', 'lib']
cache_path  = 'forge-cache'
gas_reports = ["*"]
optimizer = true
optimizer_runs = 20000
test = 'test'
solc = '0.8.26'
fs_permissions = [{ access = 'read', path = './out' }, { access = 'read-write', path = './deploy-out' }]
evm_version = 'cancun'
remappings = [
    '@openzeppelin/=node_modules/@openzeppelin/',
    '@storyprotocol/core/=node_modules/@story-protocol/protocol-core/contracts/',
    '@storyprotocol/periphery/=node_modules/@story-protocol/protocol-periphery/contracts/',
    'erc6551/=node_modules/erc6551/',
    'forge-std/=lib/forge-std/src/',
    'ds-test/=node_modules/ds-test/src/',
    '@storyprotocol/test/=node_modules/@story-protocol/protocol-core/test/foundry/',
    '@solady/=node_modules/solady/'
]
```

#### 4. Remove Example Contracts

```bash
rm src/Counter.sol script/Counter.s.sol test/Counter.t.sol
```

---

### 📚 Install Dependencies

```bash
# Core & Periphery Modules
yarn add @story-protocol/protocol-core@https://github.com/storyprotocol/protocol-core-v1
yarn add @story-protocol/protocol-periphery@https://github.com/storyprotocol/protocol-periphery-v1

# Supporting Libraries
yarn add @openzeppelin/contracts
yarn add @openzeppelin/contracts-upgradeable
yarn add erc6551
yarn add solady

# Dev Dependencies
yarn add -D https://github.com/dapphub/ds-test
yarn add -D github:foundry-rs/forge-std#v1.7.6
```

---

## ❗ Troubleshooting & IDE Issues

You might face IDE issues like:

```solidity
import {Test} from "forge-std/Test.sol";
```

showing red squiggly lines. **This is not a syntax error.** It's due to the IDE not resolving remappings.

✅ **Fix it:**

```bash
forge remappings > remappings.txt
```

---

## 🧪 Story Protocol Test Suite

This repo contains Foundry tests for interacting with [Story Protocol](https://docs.story.foundation/) on the Aeneid Testnet.

### 1. `test/0_IPARegistrar.t.sol`

Tests:

- Deploying SPG NFT via `RegistrationWorkflows`
- Minting NFTs
- Registering IP Assets

**Run:**

```bash
forge test --fork-url https://aeneid.storyrpc.io/ --match-path test/0_IPARegistrar.t.sol
```

---

### 2. `test/1_LicenseTerms.t.sol`

Tests:

- Registering PIL license terms
- Setting revenue token & royalty policies

**Run:**

```bash
forge test --fork-url https://aeneid.storyrpc.io/ --match-path test/1_LicenseTerms.t.sol
```

---

## 🔗 Aeneid Testnet Contract Addresses

| Contract              | Address                                      |
| ---------------------|----------------------------------------------|
| IPAssetRegistry       | `0x77319B4031e6eF1250907aa00018B8B1c67a244b` |
| RegistrationWorkflows | `0xbe39E1C756e921BD25DF86e7AAa31106d1eb0424` |
| PILicenseTemplate     | `0x2E896b0b2Fdb7457499B56AAaA4AE55BCB4Cd316` |
| RoyaltyPolicyLAP      | `0xBe54FB168b3c982b7AaE60dB6CF75Bd8447b390E` |
| MERC20 Token          | `0xF2104833d386a2734a4eB3B8ad6FC6812F29E38E` |

---

## 🗂 File Structure

```
tests/
├── 0_IPARegistrar.t.sol       # Register IP asset
└── 1_LicenseTerms.t.sol       # Register license terms
```

---

## 🚀 Quick Start

```bash
forge install
forge test --fork-url https://aeneid.storyrpc.io/
```

---

## 🙋‍♂️ Author

**Tushar Pamnani** — [@tusharpamnani](https://github.com/tusharpamnani)

