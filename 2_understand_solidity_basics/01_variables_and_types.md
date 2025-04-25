# 01 – Variables and Data Types in Solidity

> 📘 **Goal:** Understand how to declare and use variables in Solidity, and learn about the fundamental value and reference types used in smart contract development.

---

## 🔢 What Are Variables in Solidity?

Variables are used to store and manipulate data in a Solidity smart contract. Based on their lifespan and location, variables fall into two categories:

- **State Variables** – Stored permanently on the blockchain.
- **Local Variables** – Exist temporarily during a function call.

```solidity
// State variable
uint256 public myNumber;

function setNumber(uint256 _num) public {
    // Local variable
    uint256 doubled = _num * 2;
    myNumber = doubled;
}
```

📘 Reference: [Solidity Docs – Types](https://docs.soliditylang.org/en/latest/types.html)

---

## 🧠 Core Solidity Data Types

Solidity offers both **value types** and **reference types**.

### 🔹 Value Types  
Stored directly in memory or storage.

| Type           | Description                           | Example                      |
|----------------|---------------------------------------|------------------------------|
| `uint`         | Unsigned integer (`uint256` default)  | `uint256 age = 30;`          |
| `int`          | Signed integer (`int256` default)     | `int balance = -100;`        |
| `bool`         | Boolean value                         | `bool isActive = true;`      |
| `address`      | Ethereum address                      | `address owner = msg.sender;`|
| `bytes1`–`bytes32` | Fixed-length byte arrays         | `bytes32 hash;`              |
| `enum`         | User-defined enumerated type          | `enum Status { Active, Inactive }` |

📘 Solidity also supports fixed-point decimals (`fixed`, `ufixed`) but they are not fully supported yet.  
📗 More: [Solidity Value Types](https://docs.soliditylang.org/en/latest/types.html#value-types)

---

### 🔸 Reference Types  
Stored by reference in memory or storage.

| Type       | Description                       | Example                                          |
|------------|-----------------------------------|--------------------------------------------------|
| `string`   | UTF-8 encoded dynamic string      | `string name = "Alice";`                         |
| `bytes`    | Dynamic array of bytes            | `bytes data = "0x1234";`                         |
| `array`    | Dynamic or fixed-size sequence    | `uint[] numbers;`                                |
| `mapping`  | Key-value mapping                 | `mapping(address => uint256) balances;`          |
| `struct`   | Custom composite type             | `struct Person { string name; uint age; }`       |

📘 Must specify `memory`, `storage`, or `calldata` for reference types.  
📗 More: [Solidity Reference Types](https://docs.soliditylang.org/en/latest/types.html#reference-types)

---

## 🛠 Declaring Variables: Syntax & Examples

### 🌐 State Variables

Defined outside functions, stored on-chain, persistent.

```solidity
uint256 public counter = 0;
```

### 🔄 Local Variables

Defined within functions, exist only in memory during execution.

```solidity
function demo() public pure returns (uint256) {
    uint256 localVal = 10;
    return localVal;
}
```

⚠️ Constants and Immutables

- constant: Assigned at compile time, never changes.

- immutable: Assigned once at construction, then constant.

```solidity
uint256 public constant FEE = 100;
address public immutable OWNER;

constructor() {
    OWNER = msg.sender;
}
```

📘 **Use `constant` and `immutable` to save gas and ensure immutability.**  
📗 Reference: [Solidity State Variables](https://docs.soliditylang.org/en/latest/contracts.html#state-variables)

---

## 🧾 Data Locations: `memory`, `storage`, `calldata`

Solidity requires explicit data locations for complex types like `string`, `array`, and `struct`.

| Keyword   | Scope        | Mutability | Lifetime                    |
|-----------|--------------|------------|-----------------------------|
| `storage` | Persistent   | Mutable    | Stored on the blockchain    |
| `memory`  | Temporary    | Mutable    | Exists during function call |
| `calldata`| Temporary    | Read-only  | Used for function inputs    |

```solidity
function greet(string memory name) public pure returns (string memory) {
    return name;
}
```


📘 `memory` must be declared for structs, arrays, and strings passed into functions.  
📗 **Reference:** [Solidity Data Locations](https://docs.soliditylang.org/en/latest/types.html#data-location)

---

## ✅ Best Practices

- ✅ Use `uint256` instead of `uint` for clarity.
- ✅ Prefer `constant` or `immutable` when values won’t change.
- ✅ Always specify data locations for reference types (`memory`, `calldata`, `storage`).
- ✅ Name variables clearly and consistently (e.g., `ownerAddress`, `userAge`).

---

## 💡 Mini Exercise

Write the following in a Solidity contract:

1. Declare a `bool` variable named `isActive` and set it to `true`.
2. Create a `string` variable called `username`, assigned to your name.
3. Add an `address` variable named `admin`, and set it to `msg.sender` in the constructor.

---

## ✅ Quiz

**Q1. What type should you use for a non-negative number?**  
✅ A) `uint256`  
B) `int256`  
C) `bytes32`  
D) `string`

**Q2. Which of the following is a valid state variable declaration?**  
A) `public int name = true;`  
✅ B) `uint256 public count = 0;`  
C) `address = msg.sender;`  
D) `bool string = "yes";`

**Q3. Which data location is required for a `string` input in a function?**  
A) `storage`  
✅ B) `memory`  
C) `stack`  
D) `immutable`

---

## 📚 Recommended Reading

- [Solidity Docs – Types](https://docs.soliditylang.org/en/latest/types.html)
- [Solidity Cheatsheet (GitHub)](https://github.com/crytic/solidity-cheatsheet)

---

🎉 **Up Next:** Learn about functions, parameters, and Solidity visibility modifiers in  
[`02_functions_and_visibility.md`](./02_functions_and_visibility.md)


