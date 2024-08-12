# Intents: User-Defined Conditions for Executing Transactions

Intents allow for executing transactions automatically when certain criteria are met. The complexity of the current transaction-based systems in Web3 often results in an inefficient user experience. This document explores the challenges of the transaction-based model and the potential of transitioning to an intents-centric paradigm.

## The Complexity of Transaction-Based Systems

In Web3, users frequently face challenges due to the complexity of transaction-based systems. This often leads to inefficiency and user frustration. Consider the following scenario:

### User Scenario: Interacting with a dApp on the Arbitrum Network

A user intends to interact with a decentralized application (dApp) on the Arbitrum network, but their funds are currently on the Ethereum blockchain. The user must:

1. Visit the dApp website.
2. Attempt to connect their wallet to Arbitrum, discovering no available funds.
3. Open a new tab to explore bridging options for transferring funds.
4. Navigate to a bridge website.
5. Connect their wallet to the Ethereum blockchain.
6. Initiate the bridging process to transfer funds from Ethereum to Arbitrum.
7. Wait for the bridging transaction to complete.
8. Return to the original tab.
9. Switch their wallet back to Arbitrum.

Only after completing these steps can the user finally interact with the dApp on Arbitrum. This complexity is exacerbated in a world of multiple rollups, where similar challenges arise frequently.

## Transitioning to a Declarative Paradigm

The shift from a transaction-based (imperative) model to a more user-friendly (declarative) approach can be understood through the concept of Account Abstraction (AA). In Ethereum, there are two types of addresses: externally-owned accounts (EOAs) and smart contracts. EOAs initiate transactions, while smart contracts cannot. This limitation requires EOAs to trigger transactions for smart contract wallets (SCWs), despite SCWs' ability to execute complex logic.

### Account Abstraction Explained

Account Abstraction, as introduced by ERC-4337, seeks to streamline this process by enabling SCWs without requiring separate EOAs. This is achieved through a new transaction type called User Operation (UserOp) and the introduction of "Bundlers." Additionally, ERC-1271 provides a standard method for contracts to validate signatures, enhancing SCW functionality.

The AA process involves:

1. Users signing a UserOp, specifying their desired operation.
2. UserOps being sent to an alternative mempool, where executors and bundlers bundle them together and submit them as bundles to an entry point contract.
3. The entry point contract communicating with the SCW, which validates and executes the operations.

One key benefit of AA is gas abstraction, simplifying the gas payment process. Paymasters, acting as intermediaries, cover gas costs on behalf of users. This eliminates the need for users to manage gas costs directly, enhancing the user experience.

However, AA has limitations, particularly in supporting cross-chain paymasters. For instance, if a user wants to cover transaction costs on Arbitrum using USDC from Ethereum, the cross-chain transaction becomes challenging.

![Account Abstraction](assets/AA.jpg "Account Abstraction")

## Introducing Intents

In the current transaction model, validators follow specific computational paths based on transaction signatures and incentives. In contrast, intents allow any path that meets specific conditions. Users can sign and share intents, granting recipients the authority to choose computational paths on their behalf. This flexibility enhances gas and economic efficiency.

Intents allow for multiple actions in a single transaction, enabling efficient netting of overlapping intents. They also offer more flexible gas payments, such as third-party sponsorship or accepting payments in different tokens. UserOps, while not intents, enable wallets to express simple intents through validation logic.

### Intent-Specific Applications

Account Abstraction facilitates user-centric objectives through intent-specific applications:

- **Limit Orders**: Users can specify conditions for asset exchanges.
- **Gas Sponsorship**: Users can opt to pay transaction fees in tokens like USDC.
- **Delegation**: Restrictions can be placed on account interactions.
- **Transaction Batching**: Multiple intents can be batched for gas efficiency.
- **Aggregators**: Users can specify optimal prices or yields for actions.

Despite these advancements, AA faces challenges in multi-chain environments, where discovering optimal solutions requires manual effort. A comprehensive language for intents is needed to scale across multiple chains effectively.

## General-Purpose Solutions for Intent-Centric Systems

In an intents-centric world, users declare preferences, and third-party actors (solvers/executors) execute these preferences. The innovation lies in the network of specialized third parties providing optimized outcomes.

For example, if a user wants to purchase a specific token using liquidity from multiple rollups, a sophisticated solver can efficiently find the best solution. This approach eliminates the impracticality of single companies integrating with all new rollups and domains.

The ideal infrastructure for intents should minimize Miner Extractable Value (MEV), maximize censorship resistance, and optimize cross-domain interactions. It should balance granular user intent communication with user experience, addressing unanswered questions like optimal execution and cross-domain intent posting.

### Examples of General-Purpose Solutions

Several projects are vying to establish an intent layer for blockchains:

- **Anoma**: A unified architecture for decentralized applications, focusing on intent-centricity and homogeneous architecture.
  - [Whitepaper](https://github.com/anoma/whitepaper/blob/main/whitepaper.md)

## Conclusion

The shift from a transaction-based to an intents-centric paradigm in Web3 holds the potential to revolutionize user experience and execution efficiency. By enabling users to express preferences and leveraging specialized third parties for optimized execution, the blockchain ecosystem can evolve towards a more seamless and user-friendly environment. However, significant challenges remain in building scalable and versatile intent layers, necessitating continued innovation and collaboration within the industry.

## References

- [Intent-Based Architectures and Projects Experimenting with Them](https://bwetzel.medium.com/intent-based-architectures-and-projects-experimenting-with-them-c3ee63ae24c)
- [Anoma Whitepaper](https://github.com/anoma/whitepaper/blob/main/whitepaper.md)
- [What are Blockchain Intents with SEDA](https://sedaprotocol.medium.com/what-are-blockchain-intents-with-seda-a64e2274e1e7)
