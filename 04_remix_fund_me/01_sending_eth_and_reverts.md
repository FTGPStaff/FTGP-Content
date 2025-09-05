### Sending ETH through a Function and Reverts

In Solidity, a transaction (Tx) certain data fields as follows:
- **Nonce:** Tx count for the account
- **Gas Price:** Price per unit of gas in wei
- **Gas Limit:** Maximum gas amount that the Tx can consume
- **To:** Tx recipient address
- **Value:** Tx amount to send, in wei
- **Data:** The payload sent to the recipient, which may be a function call or a contract deployment request
- **v, r, s:** Components of Tx signature

On Ethereum, a transaction can either be a simple ETH transfer or a function call. When transferring ETH, the required fields are  `To` and `Value`; the others are optional.However, when making a function call, the transaction must include `Gas Limit`, `To` and `Data`. The `Gas Limit` defines maximum computational effort allowed, expressed in units of gas.

To define a function that can receive ETH, it must be marked as  `payable`

```solidity
    function fund() public payable{

    }
```

Smart contracts, like user accounts, can hold ETH.

To check the amount of ETH sent with a transaction in Solidity, use `msg.value`.  Additionally, you can use the `require(CONDITION, REVERT MESSAGE)` statement to ensure that certain conditions are met before proceeding. If the condition fails, the transaction is reverted, none of the subsequent code is executed, and all unused gas (except what was consumed up to the revert point) is refunded.

For example, to ensure that the sent amount is at least 1 ETH (1 ETH = 1e18 wei; see [ETH Converter](https://eth-converter.com)), you can use the following approach.

Create a new contract in Remix IDE and name it `FundMe.sol`.  Copy and paste the code below, then compile and deploy the contract.

```solidity
    pragma solidity ^0.8.8;

    contract FundMe{

        uint256 public number;

        function fund() public payable{
            number = 5;
            require(msg.value > 1e18, 'Minimum required amount is 1ETH.');
        }
    }
    
```
AAfter deploying the contract, call the `fund` function with less than 1ETH. You will notice that Remix IDE displays an error. Despite the revert, some gas is still consumed—specifically by the line that sets the `number` variable. You can experiment by adding more lines of code before `require` to observe how much gas each operation consumes.

For a complete list of `OPCODES` (Ethereum Virtual Machine instructions), see [Ethereum Opcodes Documentation.](https://ethereum.org/en/developers/docs/evm/opcodes/)