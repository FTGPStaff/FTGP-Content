### Inheritance

Inheritance in Solidity allows you to **reuse and extend** existing smart contracts. This is a powerful tool for building modular and maintainable systems. Unlike using only the `import` keyword — which allows you to use another contract as how it is defined — inheritance allows you to **modify and enhance** the behaviour of functions from a base (parent) contract in a child contract.

#### Keywords:
- **`is`** — Used to specify that one contract inherits from another.
- **`override`** — Indicates that a function is being **redefined** in the child contract.
- **`virtual`** — Applied to a function in the parent contract to **allow it to be overridden**.

Let’s now create a new contract that **inherits** from `SimpleStorage.sol` and overrides one of its functions.
 Create a new smart contract and name it `ExtraStorage.sol` and copy and paste the code given below.

```solidity
    // SPDX-License-Identifier: MIT

    pragma solidity ^0.8.7;

    import "./SimpleStorage.sol";

    contract ExtraStorage is SimpleStorage {
        /// overriding the store function
        function store(uint256 _favoriteNumber) public override {
            favoriteNumber = _favoriteNumber + 5;
        }
    }
```

Now that you can **compile**, **deploy**, and **interact** with `ExtraStorage.sol` smart contract. After deploying the smart contract
- Use the `store()` function to input a value (e.g., `10`).
- Then click on `retrieve()` to fetch the stored value.
- You should see the result as `15` (because `10 + 5 = 15`).

---