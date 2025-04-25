# 03 – Comments and Code Style in Solidity

> 📘 **Goal:** Learn how to use comments for documentation and follow style conventions for writing clean, readable Solidity code.

---

## ✏️ Why Comments Matter

Comments help you (and others) understand what your code does.

### Types of Comments

| Type        | Syntax             | Purpose                                |
|-------------|--------------------|----------------------------------------|
| Single-line | `// comment`       | Brief explanation of a line or logic   |
| Multi-line  | `/* comment */`    | Longer descriptions or block comments  |

### ✉️ Example:

```solidity
// This function stores a value in favoriteNumber
function store(uint256 _num) public {
    favoriteNumber = _num; // Update state variable
}

/*
This contract demonstrates:
- State variables
- Simple setter/getter functions
- Usage of view functions
*/
```

## 🔧 Code Style Best Practices

Following a consistent coding style improves readability and reduces bugs.

---

### 🔢 Naming Conventions

| Item Type         | Convention  | Example                          |
|-------------------|-------------|----------------------------------|
| Variables & Params| `camelCase` | `favoriteNumber`                 |
| Constants         | `UPPER_CASE`| `MAX_SUPPLY`                     |
| Functions         | `camelCase` | `getBalance()`                   |
| Contracts         | `PascalCase`| `SimpleStorage`                  |
| Structs & Enums   | `PascalCase`| `struct User`, `enum Role`       |

---

### ✍️ Indentation & Braces

- Use **4 spaces** for indentation (avoid tabs)
- Place the opening brace `{` **on the same line** as the declaration
- Align the closing brace `}` with the **start of the block**

```solidity
function add(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
}
```

---

## ❌ Avoid

- Unused variables
- Long lines of code (wrap after ~100 characters)
- Deep nesting (prefer using helper functions)

---

## 🔹 Recommended Tools

- [Prettier Plugin for Solidity](https://github.com/prettier-solidity/prettier-plugin-solidity): Automatically formats your code
- [Solhint](https://github.com/protofire/solhint): Linter and style checker for Solidity

---

## 💡 Mini Exercise

📝 Add inline and block comments to describe what the following contract does:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract Profile {
    // Declare user's name
    string name;

    // Declare user's age
    uint256 age;

    // Set the user's profile data
    function setProfile(string memory _name, uint256 _age) public {
        name = _name; // Update name
        age = _age;   // Update age
    }

    // Get the stored age
    function getAge() public view returns (uint256) {
        return age;
    }
}
```
---

## ✅ Quiz

**Q1. What is the correct syntax for a single-line comment?**  
A) `<!-- comment -->`  
B) `# comment`  
✅ C) `// comment`  
D) `** comment **`

**Q2. What naming style should be used for constants?**  
A) `camelCase`  
B) `PascalCase`  
✅ C) `UPPER_CASE`  
D) `kebab-case`

**Q3. Why are comments important?**  
A) They increase gas usage  
B) They confuse the compiler  
✅ C) They document the code for readers  
D) They execute faster

---

## 📖 Further Reading

- 📘 [Solidity Style Guide (Official)](https://docs.soliditylang.org/en/latest/style-guide.html)
- 🔍 [Solhint Rules](https://protofire.github.io/solhint/)

---

## 🎉 Next Up

Learn about gas optimization and transaction costs in  
[`04_gas_and_transaction_basics.md`](./04_gas_and_transaction_basics.md)
