### Constructor in Solidity

A constructor in Solidity is a special function that is automatically executed once, when the contract is deployed. It is typically used to initialize contract state such as setting the contract owner or configuring default values.

`constructor` keyword is used to create a constructor. Here is an example in which the constructor runs automatically during deployment and performs any necessary setup.

```solidity
    contract contractName{
        constructor(){
            // Initialization code
        }
    }
```

#### Modifiers in Solidity

A modifier is a special function type used to change or extend the behavior of other functions without modifying their code directly. Modifiers are commonly used to:
- Control access to functions, for example only allowing the owner to call a function
- Perform input validation
- Prevent `reentrancy` attacks

Modifiers are created using `modifer` keyword. An example of modifier creation is given below.

```solidity
    function myFunction() public modifierName{

    }

    modifier modifierName() {
        require(requiredCondition, "Condition is not met");
        _;
    }
```
The underscore `_` represents where the body of the modified function will be inserted during execution.
- If `_` is after the require, the condition is checked before the function runs.
- If `_` is before the require, the condition is checked after the function runs which is rarely desirable.

Instead of using `modifer`, you can also apply access control directly inside the function:

```solidity
    function myFunction() public modifierName{
        require(msg.sender == owner , "Only the owner of the contract can withdraw");
        }
    
```
However, if this logic is repeated across multiple functions, the code becomes harder to maintain. Using a modifier keeps your code **clean**, **reusable**, and **easier to read**.



In the previous `FundMe.sol` contract, anyone could call the `withdraw()` function. That is a **security flaw**. To fix this, we define an *owner* and restrict *withdraw()* so that only the owner can execute it.

Copy and paste the updated contract below into your `FundMe.sol` file, then compile and deploy it.

```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.8;

    import "./PriceConverter.sol";

    contract FundMe{
        /// For all objects in type of uint256 PriceConverter library functions will be available with the code below.
        using PriceConverter for uint256;

        uint256 public minimumUSD = 50 * 1e18;
        address[] public funders;
        mapping(address => uint256) public addressToAmountFunded;

        /// Global owner variable to store owner's address to allow only owner to withdraw
        address public owner;

        // Constructor sets the deployer as the contract owner
        constructor(){
            owner = msg.sender;
        }

        function fund() public payable{
            require(msg.value.getConversationRate() >=  minimumUSD, 'Minimum required amount is 1ETH.');
            funders.push(msg.sender);
            addressToAmountFunded[msg.sender] = msg.value;
        }

        function withdraw() public onlyOwner{
            for(uint256 funderIndex = 0; funderIndex < funders.length; funderIndex++){
                address funder = funders[funderIndex];
                addressToAmountFunded[funder] = 0;

            } 
            funders = new address[](0);
            (bool callSuccess, bytes memory dataReturned) = payable(msg.sender).call{value:address(this).balance}("");
            require(callSuccess, "Call failed.");
        }

        modifier onlyOwner(){
            require(msg.sender == owner , "Only the owner of the contract can withdraw");
            _;
        }
    }
```