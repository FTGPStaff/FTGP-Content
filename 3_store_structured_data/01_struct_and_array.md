# 05 – Structs and Arrays in Solidity

> 📘 **Goal:** Learn how to store structured data in Solidity using `struct` and `array`, and how to manipulate these types effectively.

---

## 🔍 What Are Structs and Arrays?

### 🧱 Structs
A `struct` in Solidity is a custom data type that allows grouping of related data. It's like creating your own data type composed of different variables.

```solidity
struct Person {
    string name;
    uint256 age;
}
```
- Useful for representing complex entities (e.g., a user, product, or vote)

- Allows logical grouping of variables into a single object

## 📚 Arrays
An array is a collection of items of the same type. It can be:

- **Fixed-size**: size set at declaration
- **Dynamic**: size can grow or shrink during execution

```solidity
uint256[] public numbers; // dynamic array
Person[] public people;   // dynamic array of Person structs
```

## 🔢 Why Use Structs and Arrays?

Smart contracts often need to track multiple values (e.g., name + age) or store lists (like a user registry). Solidity offers:

- `struct` to group related data
- `array` to store sequences of items (including structs)

These two features combined allow us to efficiently manage complex information in a decentralized app.

---

## 🛠 Declaring Structs and Arrays

### Example: Defining a `Person` Struct

```solidity
struct Person {
    string name;
    uint256 age;
}
```

### Example: Declaring an Array of `Person` 

```solidity
Person[] public people;
```

- `people` is a dynamic array that can grow

- `public` auto-generates a getter to access items by index

## ➕ Using Structs and Arrays

### Adding Items to an Array

You can add a new `Person` to the array using `.push()`:

```solidity
function addPerson(string memory _name, uint256 _age) public {
    people.push(Person(_name, _age));
}
```
📘 `memory` is required for string parameters in functions.

### Accessing Items in an Array

You can access specific elements using their index:

```solidity
function getPerson(uint256 index) public view returns (string memory, uint256) {
    Person memory p = people[index];
    return (p.name, p.age);
}
```
## 📦 Full Contract Example
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

contract PeopleList {
    struct Person {
        string name;
        uint256 age;
    }

    Person[] public people;

    function addPerson(string memory _name, uint256 _age) public {
        people.push(Person(_name, _age));
    }

    function getPerson(uint256 index) public view returns (string memory, uint256) {
        Person memory person = people[index];
        return (person.name, person.age);
    }
}
```
## 🔍 Code Breakdown (Detailed)

- `struct Person`:Defines a composite type with `name` (string) and `age` (uint256). Each `Person` groups related user information together.


- `Person[] public people;`:Declares a public dynamic array that stores multiple `Person` objects.  Since it's public, Solidity auto-generates a getter that accepts an index and returns a `Person` struct.

- `addPerson(string memory _name, uint256 _age)`: A public function that takes a name and age as input, creates a `Person`, and adds it to the `people` array using `.push()`.The keyword `memory` tells the compiler the string data is temporary and only used during function execution.


- `getPerson(uint256 index)`: A public `view` function that returns a specific `Person` from the array.  It uses the array index to fetch the struct and returns both `name` and `age`.



This example demonstrates how to model and store structured data on-chain using a combination of structs and arrays.

---

## 🎯 Mini Exercise

Write a contract that:

- Defines a `Book` struct with `title` and `author`
- Stores multiple books in an array
- Has a function to add a new book
- Has a function to get details of a book by index

---

## ✅ Quiz

**Q1. What is a `struct` in Solidity?**  
A) A type of array  
✅ B) A custom composite data type  
C) A function modifier  
D) A built-in data type  

**Q2. What keyword is required for `string` parameters in a function?**  
A) storage  
✅ B) memory  
C) calldata  
D) immutable  

**Q3. What does `.push()` do in Solidity?**  
A) Removes last item in array  
B) Updates existing entry  
✅ C) Adds a new item to an array  
D) Clears the array  

---

## 📚 Further Reading

- [Solidity Docs – Structs](https://docs.soliditylang.org/en/latest/types.html#structs)
- [Solidity Docs – Arrays](https://docs.soliditylang.org/en/latest/types.html#arrays)

---

🎉 **Next Up:** Learn how to map key-value pairs and implement fast lookups in `02_mapping_and_lookup.md`


