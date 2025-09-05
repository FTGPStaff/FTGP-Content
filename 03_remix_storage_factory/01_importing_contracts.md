# Importing Contracts

```solidity
    // SPDX-License-Identifier: MIT

    pragma solidity 0.8.8;
    // pragma solidity ^0.8.0;
    // pragma solidity >=0.8.0 <0.9.0;

    contract SimpleStorage {

        uint256 favoriteNumber;

        struct People {
            uint256 favoriteNumber;
            string name;
        }
        // uint256[] public anArray;
        People[] public people;

        mapping(string => uint256) public nameToFavoriteNumber;

        function store(uint256 _favoriteNumber) public virtual{
            favoriteNumber = _favoriteNumber;
        }
        
        function retrieve() public view returns (uint256){
            return favoriteNumber;
        }

        function addPerson(string memory _name, uint256 _favoriteNumber) public {
            people.push(People(_favoriteNumber, _name));
            nameToFavoriteNumber[_name] = _favoriteNumber;
        }
    }
```
In Solidity, the **ability of smart contracts to interact with one another** is known as **composability**. Composability is a powerful feature that allows developers to build **modular and reusable** components. This becomes especially important in building complex systems such as **DeFi (Decentralised Finance)** applications, where smart contracts often need to call and rely on each other’s functionality.

Arrays in Solidity are used to store multiple values in a single variable. You can declare them using square brackets:

```solidity
    uint[] myArray;
```

To use another smart contract inside your own, Solidity provides the **import** keyword. You must specify the path to the contract file, including its name and **.sol** extension as shown below.

```solidity
    import "./SimpleStorage.sol";
```

Create a new contract in Remix IDE and name it *StorageFactory.sol*. Then copy and paste the code given below.

```solidity

    //SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;

    /// importing a smart contract exist outside of this smart contract
    import "./SimpleStorage.sol";

    contract StorageFactory {

        /// A new array object from another smart contract is declared below
        SimpleStorage[] public simpleStorageArray;

        /// Below function uses an external contract
        function createSimpleStorageContract() public { ///public Identifier for anyone to call this function
            SimpleStorage simpleStorage = new SimpleStorage(); ///Creating a SimpleStorage object
            simpleStorageArray.push(simpleStorage); /// Storing the created object into the array defined above.

        }
    }

```