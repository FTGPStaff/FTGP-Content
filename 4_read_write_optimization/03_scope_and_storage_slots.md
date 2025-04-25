# 📦 Storage Scope & Storage Slots in Solidity

## 📘 Goal
Understand how Solidity stores variables in contract storage, learn about storage slot allocation, and avoid common pitfalls with variable overwriting and packing.

---

## 🔍 What is Contract Storage?

In Solidity, **storage** refers to the persistent on-chain state. Each contract has its own storage layout, and variables are stored in **256-bit slots**.

- Each slot is **32 bytes (256 bits)**
- Simple variables like `uint256`, `address`, `bool` each take up **one slot** (or share one if packed)
- **Storage is expensive**, so managing layout efficiently can reduce gas costs

📘 Reference: [Solidity Docs - Storage Layout](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html)

---

## 📐 Storage Slot Allocation

Variables are stored sequentially by default, **according to their declaration order**.

```solidity
uint256 public a;      // Slot 0
bool public b;         // Slot 1
uint256 public c;      // Slot 2
```

🔸 `bool` still uses a full 256-bit slot if not packed, wasting space.

---

## 📦 Variable Packing for Gas Optimization

Solidity can **pack multiple smaller variables into the same slot** if:

- They are **declared together**
- Their **combined size is ≤ 32 bytes**

```solidity
uint128 public x;  // 16 bytes
uint128 public y;  // 16 bytes → fits with `x` in same slot
```

🧠 **Tip**: Always declare smaller variables next to each other to benefit from packing.

❌ **If declared apart:**

```solidity
uint128 public x;
uint256 public z;
uint128 public y;  // now y is in a new slot
```

## 🧪 Check Storage Layout in Remix

1. Open the **Solidity Compiler** plugin  
2. Compile your contract  
3. Go to the **"Compilation Details"**  
4. Look for the **"Storage Layout"** section



---

## 🧪 Practical Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract StoragePacking {
    uint128 public x = 1;
    uint128 public y = 2;
    uint256 public z = 3;
}
```

✅ `x` and `y` will share **slot 0**  
✅ `z` will go into **slot 1**

> Check this in Remix to confirm the storage layout.

---

## ⚠️ Scoping & Shadowing

Be careful of **variable shadowing**, especially in inheritance or within functions:

```solidity
uint256 data;

function update() public {
    uint256 data = 123; // shadows the state variable!
}
```

🔍 The above local variable hides access to the state variable, and does **not modify it**.

✅ Avoid using the same name for local and state variables to reduce bugs.

---

## 🎓 Best Practices

✅ Pack variables for gas efficiency  
✅ Declare similar-sized variables together  
✅ Avoid shadowing state variables  
✅ Use Remix storage layout viewer when optimizing  
✅ Use meaningful and unique variable names

---

## 💡 Mini Exercise

Create a contract that:

- Has two `uint128` variables and one `uint256` variable  
- Arrange them for **optimal storage packing**  
- Use **Remix** to view the storage layout and confirm your packing worked

---

## ✅ Quiz

**Q1. How large is a Solidity storage slot?**  
✅ A) 32 bytes  
B) 64 bytes  
C) 16 bytes  
D) Depends on the type

**Q2. What helps multiple variables share a single storage slot?**  
A) Declaring them in a different order  
✅ B) Keeping them together and using small types  
C) Making them private  
D) Using calldata

**Q3. What is variable shadowing?**  
✅ A) Hiding state variables behind local variables of the same name  
✅ B) Declaring a local variable that masks a state variable  
C) Making variables invisible  
D) None of the above

---

## 📚 Further Reading

- [Solidity Docs – Storage Layout](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html)  
- [Solidity by Example – Storage](https://solidity-by-example.org/storage/)  
- [Remix Storage Visualizer](https://remix.ethereum.org/)

---

## 🎉 Next Up

Learn how to apply your knowledge with cost analysis in `04_cost_analysis_example.md`


