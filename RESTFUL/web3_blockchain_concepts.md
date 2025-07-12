# Web3 and Blockchain Concepts

## Core Platforms & Use Cases

### **Ethereum**

* **Purpose**: A decentralized platform for creating and running smart contracts and decentralized applications (dApps).
* **Popular Use Cases**:

  * Decentralized Finance (DeFi)
  * Non-Fungible Tokens (NFTs)
  * Tokenized assets
* **Example**: Building a decentralized marketplace where users trade digital assets through automated smart contracts.

### **Filecoin**

* **Purpose**: A blockchain-based decentralized storage network.
* **Functionality**: Incentivizes users to provide unused storage in exchange for cryptocurrency.
* **Example**: Storing large media files (e.g., videos) off-chain while referencing them on-chain in a Web3 application.

### **Polkadot**

* **Purpose**: A multi-chain protocol designed for interoperability among different blockchains.
* **Functionality**: Enables data and asset transfers across chains.
* **Example**: Connecting an Ethereum-based dApp with a Binance Smart Chain application for cross-chain token transactions.

**Key Insight**:

* **Ethereum** – Smart contracts and dApps
* **Filecoin** – Decentralized storage
* **Polkadot** – Blockchain interoperability

---

## Smart Contracts

### **Definition**

Smart contracts are self-executing programs stored on a blockchain that automatically perform actions when predefined conditions are met. They are decentralized, immutable, and transparent.

### **Key Features**

* **Decentralized**: Run on blockchain nodes instead of centralized servers.
* **Automated**: Triggered automatically when conditions are met.
* **Language-Specific**: Written in languages like **Solidity** (Ethereum) or **Rust** (Solana).
* **Immutable**: Cannot be changed after deployment.

### **Common Misconceptions**

* They **do not** run on centralized servers.
* They are **not** written in traditional languages like Java.
* They **do not** require human intervention once deployed.

### **Example**

A smart contract for crowdfunding automatically releases funds to a project only when its funding goal is met. Otherwise, it refunds contributors.

---

## Off-Chain Data Storage

### **Why Use Off-Chain Storage?**

Blockchains have limited and expensive storage. Off-chain solutions store large data (like images or documents) externally, while storing references (hashes) on-chain.

### **IPFS (InterPlanetary File System)**

* A decentralized, peer-to-peer file storage protocol.
* Files are distributed across nodes and identified by unique content-based hashes.
* Frequently used in Ethereum-based applications to store NFT metadata or datasets.

### **Clarifications**

* **Web3.js**: JavaScript library for interacting with Ethereum (not used for storage).
* **Solidity**: Language for writing smart contracts (not for storing data).
* **Truffle**: Development framework for Ethereum (not a storage tool).

### **Example**

In an NFT marketplace, the image is stored on IPFS while the IPFS hash is saved on the Ethereum blockchain, linking the token to its off-chain asset.