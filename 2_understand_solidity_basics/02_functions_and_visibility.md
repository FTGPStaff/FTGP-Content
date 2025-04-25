# 02 – Functions and Visibility in Solidity

> 📘 **Goal:** Learn how to write functions in Solidity, understand visibility modifiers, and when to use them.

---

## 🌐 What Is a Function?

A **function** in Solidity is a reusable block of code that performs a specific task. Functions can:

- Accept input parameters
- Return values
- Read from or write to the blockchain state

### ✨ Basic Function Example

```solidity
function add(uint256 x, uint256 y) public pure returns (uint256) {
    return x + y;
}
```

- `public`: **Visibility modifier** – controls who can call the function (explained below)
- `pure`: **Function type** – does not read or modify blockchain state
- `returns`: **Return type** – defines what the function gives back


## 💡 Function Visibility

Solidity functions must declare a **visibility modifier** to control who can access the function.

| Modifier   | Who Can Access                         | Use Case Example                   |
|------------|----------------------------------------|------------------------------------|
| `public`   | Anyone (external + internal)           | External interface, internal reuse |
| `external` | Only from outside the contract         | APIs meant to be called externally |
| `internal` | Only inside the contract or children   | Internal logic, helpers            |
| `private`  | Only inside the current contract       | Hidden helper functions            |

### 🔍 Example with All Visibilities

```solidity
contract VisibilityExample {
    uint256 private data;

    function setData(uint256 _data) public {
        data = _data;
    }

    function getData() external view returns (uint256) {
        return data;
    }

    function doubleData() internal view returns (uint256) {
        return data * 2;
    }

    function halfData() private view returns (uint256) {
        return data / 2;
    }
}
```

- `public` functions can be called from anywhere (even other contracts).  
- `private` functions are hidden from derived contracts.

---

## 🏠 Function Types: `view`, `pure`, `payable`

| Keyword   | Reads State | Modifies State | Receives ETH |
|-----------|-------------|----------------|--------------|
| `view`    | ✅ Yes       | ❌ No           | ❌ No         |
| `pure`    | ❌ No        | ❌ No           | ❌ No         |
| `payable` | ✅ Optional  | ✅ Yes/No       | ✅ Yes        |

### 🎯 Examples

```solidity
// Just reads a state variable
function getCount() public view returns (uint256) {
    return count;
}

// Pure math function
function multiply(uint256 a, uint256 b) public pure returns (uint256) {
    return a * b;
}

// Can receive ETH
function receivePayment() public payable {
    // Do something with msg.value
}
```

## 🎓 Best Practices

✅ Always mark your function visibility (`public`, `internal`, etc.)  
✅ Use `view` or `pure` when possible to reduce gas costs  
✅ Use `payable` only for functions that accept ETH  
✅ Keep functions short and focused on one task  
✅ Use `returns` with clearly defined types and names  

---

## 🧪 Mini Exercise

Create a contract with the following:

- A `public` function to store a number  
- A `view` function to return the stored number  
- A `pure` function to square a given number  
- A `payable` function to receive ETH  

---

## ✅ Quiz

**Q1. Which function type allows receiving ETH?**  
A) `view`  
B) `pure`  
C) `external`  
✅ D) `payable`  

**Q2. Which visibility only allows internal and derived access?**  
A) `external`  
B) `private`  
✅ C) `internal`  
D) `public`  

**Q3. What does a `pure` function mean?**  
A) Reads state only  
B) Writes state only  
C) Receives ETH  
✅ D) Doesn't read or write state  

---

## 📚 Resources

- [Solidity Functions – Official Docs](https://docs.soliditylang.org/en/latest/contracts.html#functions)
- [Solidity Function Visibility](https://docs.soliditylang.org/en/latest/contracts.html#visibility-and-getters)

---

## 🎉 Next Up

Learn about comments and style in  
[`03_comments_and_style.md`](./03_comments_and_style.md)
