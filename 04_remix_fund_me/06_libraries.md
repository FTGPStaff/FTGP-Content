### Libraries

In Solidity, libraries are similar to external smart contracts but with a few key differences:
- You cannot declare state variables inside a library.
- You cannot send or receive Ether within a library.
- If all library functions are marked `internal`, the library is embedded into the calling contract at compile time.
- If a library contains external functions, it must be deployed and linked before the main contract is deployed.

To define a library, use the `library` keyword; similar to how you define a contract or a function.

In Remix IDE, create a new smart contract named `PriceConverter.sol`. Copy and paste the code below into that file.

```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.8;
    
    import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

    library PriceConverter{

        function getPrice() internal view returns(uint256){
            AggregatorV£Interface priceFeed = AgregatorV3Interface(0x694AA1769357215DE4FAC081bf1f309aDC325306);
            (,int256 price,,,) =  priceFeed.latestRound();
            return uint256(price*1e10);
        }

        function getVersionRate(uint256 ethAmount) internal view returns(uint256){
            uint256 ethPrice = getPrice();
            uint256 ethAmountInUsd = (ethPrice * ethAmount) / 1e18;
            return ethAmountInUsd;
        }
    }

```
 Now, you need to remove the equivalent functions from the `FundMe.sol` contract and import `PriceConverter.sol` library instead.

 TTo do this, open your `FundMe.sol` contract, and copy and paste the updated code shown below. This will import the library and refactor your code to use it. Organizing logic into a library improves both the readability and maintainability of your smart contracts.

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

        function fund() public payable{
            require(msg.value.getConversationRate() >=  minimumUSD, 'Minimum required amount is 1ETH.');
            funders.push(msg.sender);
            addressToAmountFunded[msg.sender] = msg.value;
        }
    
```