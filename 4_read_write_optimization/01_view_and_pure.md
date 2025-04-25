# 🔍 View and Pure Functions in Solidity

> 📘 **Goal:** Understand how `view` and `pure` function types work in Solidity, and how they help reduce gas consumption.

---

## 💡 What are View and Pure Functions?

Solidity supports different types of functions that define how they interact with the blockchain state:

| Type   | Reads State | Modifies State | Accepts ETH | Use Case                        |
|--------|-------------|----------------|-------------|---------------------------------|
| `view` | ✅ Yes      | ❌ No          | ❌ No       | Read-only access to state       |
| `pure` | ❌ No       | ❌ No          | ❌ No       | Pure logic, no state interaction |

---

## 🧪 Example Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract GasExample {
    uint256 public favoriteNumber;

    // Writing to state - costs gas
    function store(uint256 _number) public {
        favoriteNumber = _number;
    }

    // Reading state is free (no gas if called externally)
    function retrieve() public view returns (uint256) {
        return favoriteNumber;
    }

    // Pure logic - no state interaction
    function add(uint256 a, uint256 b) public pure returns (uint256) {
        return a + b;
    }
}
```

## 🔍 Explanation of `retrieve()` Function:

- `public`: Can be called from inside or outside the contract.
- `view`: This function promises not to modify the blockchain state.
- `returns (uint256)`: It returns an unsigned integer.

---

## 💡 Why It Doesn't Cost Gas When Called Externally

If you call a `view` or `pure` function from an external source (like **Remix**, a frontend dApp, or via `eth_call`), **no transaction is created** — therefore, **no gas is used**.

However, if these functions are called from **within another function** that sends a transaction, they **will consume gas** as part of that transaction.

---

## 📊 How to Check Gas Cost in Remix

1. Open the **Deploy & Run Transactions** plugin (🪧 icon)
2. Deploy your contract using **JavaScript VM**
3. Click a function like `store()` or `retrieve()`
4. Check the **Remix terminal** at the bottom:
   - Look for the **`transact to`** or **`call to`** log
   - `execution cost`: actual gas used by the function logic
   - `transaction cost`: gas used including transaction overhead


💡 Use the **Gas Profiler** plugin in Remix for line-by-line breakdowns.

---

## 💸 How to Reduce Gas Costs

| Technique                        | Description                                          |
|----------------------------------|------------------------------------------------------|
| Use `view` or `pure`             | Avoid unnecessary writes to state                   |
| Use `uint256`                    | Prevents padding issues and is EVM-native           |
| Avoid unnecessary storage writes | Only write when values truly change                 |
| Use `constant` or `immutable`    | Saves gas at runtime by avoiding storage reads      |
| Pack variables                   | Combine small variables to save storage (advanced)  |

---

## 🎯 Practical Comparison

Try comparing the gas usage of these two functions:

```solidity
// More expensive - writes to blockchain
function increment() public {
    favoriteNumber = favoriteNumber + 1;
}

// Cheaper - does not interact with storage
function addOne(uint256 x) public pure returns (uint256) {
    return x + 1;
}
```
Deploy and test both in Remix.  
Use the **Deploy & Run** tab to view **execution cost** and **transaction cost**.

---

## 🎓 Best Practices

✅ Use `view` or `pure` whenever you don’t need to modify state  
✅ Avoid writing to storage unless necessary  
✅ Use `pure` for math helpers or logic-only functions  
✅ Mark getters as `view` or `pure` to save gas  

---

## 💡 Mini Exercise

Create a contract with:

- A `public` function `writeNumber(uint256)` to store a state variable  
- A `view` function `readNumber()` to return the stored number  
- A `pure` function `getDouble(uint256)` that returns double the input  

Use Remix to test which functions consume gas.

---

## ✅ Quiz

**Q1. Which function type requires gas to call?**  
A) pure  
B) view  
✅ C) A function that writes to state  
D) internal  

**Q2. What does "gas used" represent?**  
A) Max gas allowed  
B) Gas left over  
✅ C) Actual gas spent during execution  
D) ETH paid in fees  

**Q3. Which keyword saves gas by preventing unnecessary storage?**  
A) storage  
B) payable  
✅ C) constant  
D) fallback  

---

## 📓 Further Reading

- [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf)  
- [Solidity Docs – Functions](https://docs.soliditylang.org/en/latest/contracts.html#functions)  
- [Remix Gas Profiler Plugin](https://remix-ide.readthedocs.io/en/latest/plugin_gasprofiler.html)  

---

🎉 **Next Up:** Learn how to use `memory` and `calldata` in function parameters in `02_memory_vs_calldata.md`
