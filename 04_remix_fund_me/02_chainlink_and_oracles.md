### Chainlink and Oracles

One of the primary limitations of smart contracts is their inability to access external (off-chain) data. Since blockchain systems are *deterministic*,  they are designed to operate solely on data that is already available within the blockchain itself. Data not stored directly on a blockchain is referred to as **off-chain data**, while data that exists on the blockchain is known as **on-chain data**.

To clarify this distinction, consider using data from the Bitcoin blockchain while working on Ethereum. Even though both are blockchain platforms, they operate independently, so any data from Bitcoin is considered off-chain to Ethereum, and vice versa.

This limitation is known as the *Smart Contract Connectivity Problem* or, more commonly, the *Oracle Problem*. **Decentralized Oracle Networks (DONs)** are designed to resolve this issue by securely connecting blockchains to off-chain data sources.

**Chainlink** is a leading DON that provides off-chain data to smart contracts. Chainlink works by aggregating data from multiple off-chain sources using *Chainlink Oracle Nodes*. The collected data is then sent to a **reference contract** on-chain, making it accessible to user-defined smart contracts. To explore how Chainlink functions in practice, you can visit [Chainlink Data Demo Website](https://data.chain.link/).

To test a Chainlink-powered smart contract:
1.  Request test tokens via the [Chainlink Faucet]((https://faucets.chain.link/)) on the Ethereum Sepolia Test Network.
2. Follow the instructions in the [Chainlink Data Feeds documentation.]((https://docs.chain.link/data-feeds/using-data-feeds))
3. Click on Open in Remix to load the `AggregatorV3Interface` contract.
4. Compile and deploy the contract.

After deployment, interact with the `getChainlinkDataFeedLatestAnswer` function to retrieve live price data.
