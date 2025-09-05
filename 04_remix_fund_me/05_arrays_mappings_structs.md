### Arrays and Structs in Solidity
In Solidity, arrays are used to store multiple values of the same type. You can define them using the syntax `objectType []`. For example, you can create arrays to store `address` and `int256` values as shown below:

 ```solidity
    address[] public funders;
    int256[] public tokenAmounts;
 ```


The `msg.sender` global variable returns the address of the user who called the function. In the code below, it represents the address of the user invoking the `fund()` function.

Solidity also provides a powerful feature called **mapping**, which maps one type to another—commonly used to associate user addresses with the amount of tokens they have contributed. You can think of a mapping as a dictionary: the key is the word, and the value is its definition. To insert data into a mapping, both the key and value must be specified.

Here is an example:
```solidity
    mapping(address => uint256) public addressToAmountFunded;
    addressToAmountFunded[0x1234567890aBcDEF1234567890aBcDEF12345678] = 10;
```

In Solidity, you can define custom data types using the `struct` keyword. A **struct** allows you to group related variables under a single name, making your code more organized and readable. This is particularly useful when representing complex data objects that have multiple properties.

For example, in the context of a funding contract, you can define a **Funder struct** to store both the address of a funder and the amount they contributed. Here is an example:

```solidity
    struct Funder {
        address funderAddress;
        uint256 amountFunded;
    }
```

Copy and paste the below code into `FundMe.sol`; and then compile and deploy the contract. 

```solidity
    pragma solidity ^0.8.8;

    import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

    contract FundMe{
        uint256 public minimumUSD = 50 * 1e18;
        address[] public funders;
        mapping(address => uint256) public addressToAmountFunded;

        function fund() public payable{
            number = 5;
            require(msg.value >=  minimumUSD, 'Minimum required amount is 1ETH.');

            //Storing the funder's address into funders list defined above
            funders.push(msg.sender);
            addressToAmountFunded[msg.sender] = msg.value;
        }

        function getPrice() public view returns(uint256){
            AggregatorV£Interface priceFeed = AgregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306);
            (,int256 price,,,) =  priceFeed.latestRound();
            return uint256(price*1e10);
        }

        function getVersionRate(uint256 ethAmount) public view returns(uint256){
            uint256 ethPrice = getPrice();
            uint256 ethAmountInUsd = (ethPrice * ethAmount) / 1e18;
            return ethAmountInUsd;
        }
    }
    
```