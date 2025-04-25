# 06 – Mappings and Lookups in Solidity

> 📘 **Goal:** Understand how to use `mapping` in Solidity to store key-value pairs and perform efficient lookups.

---

## 🔑 What Is a Mapping?

A `mapping` in Solidity is a data structure used to store key-value pairs, similar to a dictionary or hash table.

```solidity
mapping(KeyType => ValueType) visibility identifier;
```

- Keys must be value types (e.g., `address`, `uint`, `bool`)

- Values can be any type, including structs, arrays, or other mappings

Example:

```solidity
mapping(address => uint256) public balances;
```
This mapping associates an Ethereum address with a balance.

## 🔎 Why Use Mappings?

Mappings are optimized for fast access. They provide:

- Efficient lookups (constant time)
- Easy key-to-value associations
- Flexibility for creating registries, user data stores, etc.

Mappings are ideal for use cases like:

- Balances
- Ownership
- User profiles
- Whitelists

---

## 🛠 Declaring and Using a Mapping

```solidity
mapping(string => uint256) public nameToAge;

function addPerson(string memory _name, uint256 _age) public {
    nameToAge[_name] = _age;
}
```

- You declare the mapping with the desired key and value types.

- You assign values using bracket notation (`nameToAge[key] = value`).

- Since the mapping is `public`, Solidity automatically creates a getter function.

## ⚠️ Notes About Mappings

- Mappings do **not** keep track of keys.
- There is **no way** to iterate through a mapping.
- All keys that haven’t been assigned explicitly return the default value of the value type.

---

## 📦 Full Contract Example with Lookup

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract PeopleDirectory {
    struct Person {
        string name;
        uint256 age;
    }

    mapping(string => uint256) public nameToAge;
    mapping(string => Person) public nameToPerson;

    function addPerson(string memory _name, uint256 _age) public {
        nameToAge[_name] = _age;
        nameToPerson[_name] = Person(_name, _age);
    }

    function lookupAge(string memory _name) public view returns (uint256) {
        return nameToAge[_name];
    }

    function lookupPerson(string memory _name) public view returns (string memory, uint256) {
        Person memory person = nameToPerson[_name];
        return (person.name, person.age);
    }
}
```

## 🔍 Code Breakdown (Detailed)

- `mapping(string => uint256) nameToAge;`  
  Associates a name with a number (e.g., an age).

- `mapping(string => Person) nameToPerson;`  
  Associates a name with a `Person` struct.

- `addPerson()`  
  Adds a person to both mappings.

- `lookupAge()` and `lookupPerson()`  
  Demonstrates how to look up values by key.

📘 The **lookup** concept refers to retrieving values from a mapping using the key. In the above functions, we perform lookups by accessing `nameToAge[_name]` or `nameToPerson[_name]`.

---

## 🎯 Mini Exercise

Write a contract that:

- Defines a `Student` struct with `name` and `grade`
- Uses `mapping(uint => Student)` to store students by ID
- Has a function to add a new student
- Has a function to look up a student by ID

---

## ✅ Quiz

**Q1. What does a mapping do in Solidity?**  
✅ A) Associates a key with a value  
B) Loops through a list  
C) Stores fixed-size arrays  
D) Sorts data automatically  

**Q2. What happens when you access a key that hasn’t been set?**  
✅ A) It returns the default value of the value type  
B) It throws an error  
C) It returns zero gas  
D) It creates the key automatically  

**Q3. Which of the following is NOT true about mappings?**  
A) They provide fast access  
B) They are unordered  
✅ C) They support iteration  
D) They can store structs as values  

---

## 📚 Further Reading

- [Solidity Docs – Mappings](https://docs.soliditylang.org/en/latest/types.html#mappings)
- [Solidity by Example – Mappings](https://solidity-by-example.org/mapping/)

---

🎉 **Next Up:** Practice combining arrays and mappings in `03_example_peoplebook.md`



