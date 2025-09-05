### Interfaces and Price Feeds

To interact with external smart contracts in Solidity, you need both the **ABI (Application Binary Interface)** and the contract address. For Chainlink price feeds, you can find contract addresses listed on the [Chainlink website](https://docs.chain.link/data-feeds/price-feeds/addresses?page=1).

Although copying the ABI directly from the Chainlink site is possible, it is generally discouraged, as it increases the size and complexity of your code. Instead, you can use an `interface`, a special Solidity construct that defines the functions of an external contract without implementing them. You can find an example of an interface for Chainlink price feeds here [AggregatorV3Interface.sol on GitHub](https://github.com/smartcontractkit/chainlink/blob/develop/contracts/src/v0.8/shared/interfaces/AggregatorV3Interface.sol)

You have two main options for using this interface:

- Copy the interface directly into your contract file – This works but can clutter your code.

- Use the `import` keyword with the interface’s address and repository path – This is the cleaner and more scalable approach, especially in larger projects. An example code snippet will be provided below to demonstrate how this is done.

#### Type Casting

**Type casting** is used to explicitly convert one data type into another. This is especially useful when working with functions or operations that require specific types. For instance, converting from `int` to `uint`, or from smaller integer types like uint8 to larger ones like uint256, ensures compatibility and prevents errors during execution. In Solidity, type casting must be done explicitly as Solidity does not automatically convert types.


For example,if you have a variable declared as int256 and want to use it where a uint256 is required, you can convert it like this:
```solidity
    uint256(myInteger);
```

Copy and paste the below code into `FundMe.sol`; and then compile and deploy the contract. 

```solidity
    pragma solidity ^0.8.8;

    import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

    contract FundMe{

        uint256 public minimumUSD = 50 * 1e18; // Converting USD 

        function fund() public payable{
            
            number = 5;

            require(msg.value >=  minimumUSD, 'Minimum required amount is 1ETH.');
        }

        function getPrice() public view returns(uint256){
            // ETH-USD Chainlink smart contract address on Sepolia testnet: 0x694AA1769357215DE4FAC081bf1f309aDC325306
            AggregatorV£Interface priceFeed = AgregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306);
            
            // to store all data returned from latestRound() remove the comment in the following line.
            /// (uint80 roundID, int price, uint startedAt, uint timeStamp, uint80 answeredInRound) =  priceFeed.latestRound();

            //However we only need price data therefore;
            (,int256 price,,,) =  priceFeed.latestRound();

            /// ETH price in USD multiplied the return value to 1e10 to get the actual price in Wei
            return uint256(price*1e10);
            

        }

        function getVersionRate(uint256 ethAmount) public view returns(uint256){
            uint256 ethPrice = getPrice();
            /// The ethAmountInUsd is divided by 1e18 to get the actual price in USD as 1 ETH = 1e18 Wei
            uint256 ethAmountInUsd = (ethPrice * ethAmount) / 1e18;
            return ethAmountInUsd;
        }
    }
    
```