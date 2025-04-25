# 📊 Gas Cost Analysis Example

## 📘 Goal

Understand how gas usage varies depending on how your smart contract is written. Learn to test and compare functions to improve efficiency.

---

## 🌟 Scenario Overview

Let’s say we want to increment a counter.  
We’ll compare three implementations:

- **Unoptimized**: Simple state update  
- **Optimized View**: Read-only call  
- **Pure**: Stateless arithmetic  

---

## 🔍 Step 1: The Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract GasComparison {
    uint256 public counter;

    // 1. Writes to storage (costs gas)
    function increment() public {
        counter = counter + 1;
    }

    // 2. Reads from storage (view, no gas externally)
    function getCounter() public view returns (uint256) {
        return counter;
    }

    // 3. Does not touch storage (pure)
    function addOne(uint256 x) public pure returns (uint256) {
        return x + 1;
    }
}
```

## 📈 Step 2: Deploy and Test in Remix

1. Open **Remix**
2. Paste the contract into a new `.sol` file
3. Compile using version `0.8.8`
4. Deploy to **JavaScript VM**
5. Open the **Terminal** panel
6. Call each function and observe the **gas used**

---

## ⌛ Comparing Gas Usage

| Function      | Action             | Gas Used (approx)     |
|---------------|--------------------|------------------------|
| `increment()` | Write to storage   | ~21,000+               |
| `getCounter()`| View from storage  | 0 (external call)      |
| `addOne(x)`   | Pure calculation   | ~400                   |

---

## 💡 Tips to Save Gas

| Technique                  | Description                             |
|----------------------------|-----------------------------------------|
| Use `view` or `pure`       | Skip unnecessary storage interaction    |
| Avoid extra storage writes | Only write if value truly changed       |
| Pack small variables       | Use smaller types back-to-back          |
| Use `immutable` or `constant` | Avoid runtime storage lookup       |

---

## 🎓 Mini Exercise

Write a contract that includes:

- A function `doubleWrite(uint256)` that **writes to the same variable twice**
- A function `checkGas(uint256)` that returns `2 * input` **without touching storage**

> Use **Remix** to compare their gas costs!

---

## ✅ Quiz

**Q1. Which of the following uses the most gas?**  
A) `view` function  
B) `pure` function  
✅ C) Function that **writes to storage**  
D) Function with `require` only

**Q2. What does "execution cost" measure?**  
✅ A) The **actual gas used** during logic execution  
B) The total ETH sent  
C) The max gas limit allowed  
D) The return data length

**Q3. What does `pure` mean in Solidity?**  
A) Can access state but not write it  
✅ B) Cannot read or write state  
C) Can modify but not read state  
D) Only reads from calldata

---

## 📚 Further Reading

- [Solidity Docs – Functions](https://docs.soliditylang.org/en/latest/contracts.html#functions)
- [Ethereum Gas Costs – Cheatsheet](https://github.com/miguelmota/ethereum-gas-costs)
- [Remix Gas Profiler Plugin](https://remix.ethereum.org/)

---


