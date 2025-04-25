# 01 – What is a Smart Contract?

> 📘 **Objective**: Learn what a smart contract is, why it's important, and what it can do.

---

## 🧠 What Is a Smart Contract?

A **smart contract** is a program that runs on the blockchain. It defines a set of **rules and behaviors**, and once deployed, it executes automatically when conditions are met.

> ✅ Think of it like an unchangeable robot agreement that lives on the blockchain.

### ✨ Key Features:

| Feature      | Description                                              |
|--------------|----------------------------------------------------------|
| 🔒 Immutable | Once deployed, code cannot be changed.                   |
| 🔍 Transparent | Anyone can read and verify the logic.                  |
| ⚙️ Autonomous | Automatically executes without intermediaries.          |

---

## ⚖️ Real-World Example vs Smart Contract

| Scenario       | Traditional Way                          | Smart Contract Way                      |
|----------------|-------------------------------------------|-----------------------------------------|
| Voting         | Manual paper ballots, counted by people  | Call `vote()` function on a contract    |
| Rent Payment   | Bank transfer + manual confirmation      | Call `payRent()` → funds sent instantly |
| Ownership      | Government land registry                 | `ownerOf(propertyId)` on-chain forever  |
| Digital Rights | Copyright registration or platforms      | NFT ownership recorded on-chain         |

---

## 💼 What Can Smart Contracts Do?

Smart contracts are the backbone of Web3 and can be used for:

- 💸 Automating payments (e.g. salaries, rewards)
- 🎨 Managing NFTs and digital ownership
- 🏦 Decentralized finance (DeFi) protocols
- 🗳 DAO voting and governance
- 🎮 Blockchain games (e.g. item trading, upgrades)

---

## 🧪 Examples of Smart Contracts in Use

| Project      | Description                                          |
|--------------|------------------------------------------------------|
| [Uniswap](https://uniswap.org)     | Decentralized exchange powered by smart contracts |
| [Aave](https://aave.com)           | Lending and borrowing through smart contracts     |
| [OpenSea](https://opensea.io)      | NFT marketplace using contract-based ownership    |
| [ENS](https://ens.domains)         | Human-readable domain names on Ethereum           |
| [MakerDAO](https://makerdao.com)   | Stablecoin protocol backed by smart contracts     |

---

## 🆚 Smart Contracts vs Traditional Code

| Feature             | Traditional App             | Smart Contract               |
|---------------------|-----------------------------|------------------------------|
| Can be altered?     | ✅ Yes (server-side)         | ❌ No (unless designed so)   |
| Requires trust?     | ✅ Yes                       | ❌ No – code is the law      |
| Transparent?        | ❌ No                        | ✅ Yes – on-chain            |
| Executed where?     | Central servers             | Blockchain (e.g. EVM)        |

---

## 💬 What Language Do They Use?

Smart contracts on Ethereum are written in:

### 🔤 Solidity
- High-level, statically-typed language inspired by JavaScript
- Compiles to bytecode for the Ethereum Virtual Machine (EVM)
- The primary language used in this course

📖 **Learn more**: [Solidity Official Docs](https://docs.soliditylang.org)

---

## 📎 Additional Resources

- [Solidity by Example](https://solidity-by-example.org)
- [Ethereum Developer Docs](https://ethereum.org/en/developers/docs/smart-contracts/)
- [Dune Analytics](https://dune.com) – Explore real smart contract usage
- [Chainlink Use Cases](https://chain.link/use-cases) – Practical smart contract applications

---

## ✅ Quiz: Check Your Understanding

> Select the best answer for each question.

**1. What makes smart contracts "immutable"?**  
- [ ] They are encrypted with SHA256  
- [x] Once deployed, the code cannot be changed  
- [ ] Only admins can change them with a private key  
- [ ] They use zero-knowledge proofs

---

**2. Which of the following is NOT a typical smart contract application?**  
- [ ] NFT ownership  
- [x] Antivirus software updates  
- [ ] DAO governance  
- [ ] DeFi lending

---

**3. Where are smart contracts executed?**  
- [ ] Local machine  
- [ ] AWS Cloud  
- [x] Blockchain virtual machine (e.g. EVM)  
- [ ] GitHub servers

---

**4. Why is transparency important in smart contracts?**  
- [ ] So only developers can debug it  
- [ ] To reduce gas fees  
- [x] So anyone can verify and audit the logic  
- [ ] To prevent people from calling functions

---

**5. What language will we use in this course to write smart contracts?**  
- [ ] Java  
- [x] Solidity  
- [ ] Python  
- [ ] Rust

---



### ▶️ Next: [02 – Intro to Remix IDE](02_intro_to_remix.md)
