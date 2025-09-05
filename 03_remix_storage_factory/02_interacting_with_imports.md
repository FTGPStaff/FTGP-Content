### Interacting with Imported Smart Contracts

To interact with an **imported smart contract**, you can create an **object (instance)** of that contract within your own contract. This object acts as a reference, allowing you to call the external contract's functions.

There are **two main ways** to use an external contract in Solidity:

1. **By importing the contract's source file using the `import` keyword.**
2. **By referencing a deployed contract's address and its Application Binary Interface (ABI).**

#### What is an ABI?
The **Application Binary Interface (ABI)** defines how to interact with a smart contract, including:
- The list of functions it contains
- Functions' input parameters and return types
The ABI is required when you want to interact with a deployed contract **without importing the source code** directly.

#### How to Find the ABI and Address in Remix IDE?
After compiling a smart contract in **Remix IDE**:
1. Scroll down to the **"Compilation Details"** section in the compiler tab.
2. Click it to view the contract's:
   - **Deployed address**
   - **ABI** (in JSON format)

You will need both of these if you are interacting with the contract **externally**, such as from another contract that does not import its source file.

Add the following code to your `StorageFactory.sol` smart contract **just after** the `createSimpleStorageContract()` function.

```solidity

    function sfStore(uint256 _simpleStorageIndex, uint256 _simpleStorageNumber) public {

        // simpleStorage object stored in simpleStorageArray at _simpleStorageIndex is assigned to a new object to access the functions in the imported smart contract
        SimpleStorage simpleStorage = simpleStorageArray[_simpleStorageIndex];

        simpleStorage.store(_simpleStorageNumber);
    }

    function sfGet(uint256 _simpleStorageIndex) public view returns(uint256){
        /// Assigning the simpleStorage object stored at index _simpleStorageIndex to a new simpleStorage object
        SimpleStorage simpleStorage = simpleStorageArray[_simpleStorageIndex];

        /// Returning the value stored in this object    
        return simpleStorage.retrieve();
    }

```

#### Testing Your Contract: Calling External Functions

Now that you have added the interaction logic, you can call these functions to interact with the imported smart contract **`SimpleStorage.sol`** through **`StorageFactory.sol`**.

#### Step-by-Step Instructions

1. **Call `createSimpleStorageContract()`**
   - This will create a new instance of the `SimpleStorage` contract.
   - You should see an entry appear in the `storageContracts` array.

2. **Call `sfStore()`**
   - Provide two arguments:
     - The **index** of the contract instance (e.g., `0` if it’s the first one you created).
     - The **value** you want to store (e.g., `7`).
   - Example input:  
     ```
     sfStore(0, 7)
     ```

3. **Call `sfGet()`**
   - Provide the **same index** you used in `sfStore`.
   - This function will retrieve the stored value from that particular contract instance.
   - Example input:
     ```
     sfGet(0)
     ```
   - Expected output: `7`