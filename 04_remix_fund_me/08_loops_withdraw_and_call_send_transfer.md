### Loops in Solidity
Loops are powerful tools in programming used to iterate over a set of values or perform repeated operations. In Solidity, the `for` loop is commonly used for this purpose.

You can define a loop using the `for` keyword. Here is a basic loop that logs a message ten times:
```solidity
    /// for(StartingIndex; EndingIndex; StepAmount)
    for (uint i = 0; i < 10; i = i+1) {
        emit LogMessage("Hello, world!");
    }

    /// i = i+1 has the same impact as i++
    for (uint i = 0; i < 10; i++) {
        emit LogMessage("Hello, world!");
    }
```
The expression *i++* is shorthand for *i = i + 1*.


#### Token Transfers in Solidity
When transferring ETH or interacting with external contracts, Solidity provides three common methods, each with distinct characteristics:

1. `transfer (2300 Gas, Throws on Error)`: Costs exactly 2,300 gas and reverts the transaction if it fails.

2. `send (2300 Gas, Returns Boolean)`: Costs exatly 2,300 gas and returns a boolean indicating success (true) or failure (false). Does not revert automatically.

3. `call (All Gas / Custom Gas, Returns Boolean & Data)`: A low-level and flexible method. It returns two values:
    1. **bool success** whether the call was successful,
    2. **bytes memory data** any returned data from the external call. Since bytes is a dynamic array, it must be stored in `memory`.


Copy and paste below code into your `FundMe.sol` smart contract, then compile and deploy it.

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

        function withdraw() public{
            // Resetting the funded amounts for each funder
            for(uint256 funderIndex = 0; funderIndex < funders.length; funderIndex++){
                //Retrieving the address of the current funder
                address funder = funders[funderIndex];
                //Resetting the funded amount
                addresstoAmountFunded[funder] = 0;

            } 

            // Resetting the funders array
            funders = new address[](0);

            // 1.Transfer
            payable(msg.sender).transfer(address(this).balance);
            // 2.Send
            bool sendSuccess = payable(msg.sender).send(address(this).balance);
            require(sendSuccess, "Send failed."); 
            /// 3.Call
            /// Calling the function with the value field assigned to the balance
            /// Call function returns two pieces of data. First is whether the calling process was successful and the second is the any data return from this calling process in bytes. 
            (bool callSuccess, bytes memory dataReturned) = payable(msg.sender).call{value:address(this).balance}("");
            require(callSuccess, "Call failed.");
        }
    }
```