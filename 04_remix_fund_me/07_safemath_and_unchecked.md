### SafeMath, Overflow Checking and the "unchecked" Keyword

SafeMath is one of the most commonly used libraries in Solidity to ensure that mathematical operations stay within the valid value range of a data type, helping to prevent `overflow` or `underflow` vulnerabilities.

Create a new file in Remix IDE and name it `SafeMathTester.sol`. Then, copy and paste the code below into the contract. Note that for this demonstration, you must use a Solidity version earlier than *0.8.0*, as overflow and underflow checks were not enforced by default in earlier versions.

```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.6.0;

    contract SafeMathTester{
            // uint8 type objects can have values in [0, 255]. Anything above or below causes error.
            uint8 public bigNumber = 255;

            function add() public {
                bigNumber = bigNumber + 1;
            }
    }
```
After deploying the contract:
1. Check the value of bigNumber.
2. Call the add() function.
3. Check the value again.

What did you notice? The value wrapped around to 0, this is known as an `overflow`.

`Overflow` occurs when a variable exceeds its maximum allowed value and wraps around to the minimum value.

`Underflow` occurs when a variable goes below its minimum value and wraps around to the maximum. Below code results in an underflow.

```solidity
    uint8 public smallNumber = 0;
    smallNumber = smallNumber - 1;
```

Starting from Solidity version *0.8.0*, arithmetic operations automatically include overflow and underflow checks. If an operation would result in an invalid value, the transaction is **reverted**.

However, the `unchecked` keyword disables overflow and underflow checks within the block. This can be used for **gas optimization** in performance-critical sections of code where the risk is managed and intentional. Use it cautiously, only when you are certain the operation will not cause unexpected behavior.

You can test these by changing the Solidity version to *^0.8.0* or using the updated code below:

```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;

    contract SafeMathTester{
            uint8 public bigNumber = 255;
            uint8 public bigNumberUnchecked = 255;

            function add() public {
                bigNumber = bigNumber + 1; // This will revert on overflow
                unchecked {bigNumberUnchecked = bigNumberUnchecked + 1}; // This will overflow silently
            }
    }
```