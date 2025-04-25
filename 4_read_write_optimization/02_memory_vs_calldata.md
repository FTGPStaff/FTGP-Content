# 02 – memory vs calldata in Solidity

> 📘 **Goal**: Understand the difference between `memory` and `calldata` in Solidity, and when to use each for reference types like strings, arrays, and structs.

---

## 📦 Why Do We Need Data Locations?

In Solidity, reference types (like `string`, `array`, `struct`, `mapping`) require a data location to specify where and how the data is stored or passed.

The three major data locations are:

| Keyword   | Scope                     | Mutability     | Gas Cost      |
|-----------|---------------------------|----------------|---------------|
| `storage` | Persistent (on-chain)     | Mutable        | Expensive     |
| `memory`  | Temporary (RAM)           | Mutable        | Cheaper       |
| `calldata`| Temporary (external input)| Read-only      | Cheapest      |

---

## 🧠 memory vs calldata

### 🔹 memory
- Temporary and mutable
- Used in most internal function calls and computations
- Exists during function execution

```solidity
function greetMemory(string memory name) public pure returns (string memory) {
    return name;
}
```

### 🔸 calldata

- Temporary but **read-only**
- Used only for `external` function parameters
- More gas efficient than `memory`
- Cannot be modified

```solidity
function greetCalldata(string calldata name) external pure returns (string calldata) {
    return name;
}
```

### ✍️ Example: Comparing `memory` vs `calldata`

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract MemoryCalldataExample {

    // Uses memory - input is copied and modifiable
    function processMemory(string memory input) public pure returns (string memory) {
        string memory copy = input;
        return copy;
    }

    // Uses calldata - input is not copied or modifiable
    function processCalldata(string calldata input) external pure returns (string calldata) {
        return input;
    }
}
```

### 🔍 When Should You Use Each?

| Use Case                                      | Recommended Location |
|----------------------------------------------|-----------------------|
| External function parameters (strings, arrays, structs) | `calldata`            |
| Internal function parameters or temporary variables     | `memory`              |
| Persistent storage (contract-level variables)           | `storage`             |

---

### 🎓 Best Practices

✅ Use `calldata` for external function inputs to save gas  
✅ Use `memory` when modifying data inside a function  
✅ Never omit the data location on reference types — the compiler will throw an error  
✅ Only `storage` and `memory` are valid in `public` and `internal` functions  

---

### 💡 Mini Exercise

Create a contract with:

- A function that accepts a `string memory` input and returns it
- An external function that uses `string calldata` as input
- Try to modify the `calldata` string and observe the compiler error

---

### ✅ Quiz

**Q1. What happens if you omit data location for a string parameter?**  
✅ A) Compiler throws an error  
B) It defaults to memory  
C) It becomes a global variable  
D) It reverts at runtime  

**Q2. Which data location is read-only and used for external inputs?**  
A) memory  
✅ B) calldata  
C) storage  
D) heap  

**Q3. Why is calldata more gas-efficient than memory?**  
✅ A) It avoids copying data into memory  
B) It precomputes gas refunds  
C) It compresses data  
D) It allocates storage slots  

---

### 📚 Further Reading

- [Solidity Docs – Data Locations](https://docs.soliditylang.org/en/latest/types.html#data-location)
- [Solidity by Example – Memory vs Calldata](https://solidity-by-example.org/data-locations/)

🎉 **Next Up:** Learn about advanced storage slot layouts and variable packing in `03_scope_and_storage_slots.md`
