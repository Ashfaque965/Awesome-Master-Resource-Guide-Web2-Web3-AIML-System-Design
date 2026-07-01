

### low-level design (LLD) problems



# Blockchain & Web3 Machine Coding Round Questions

This repository/list covers low-level design (LLD) problems, smart contract architectures, algorithms, and dApp infrastructure components frequently tested during Web3 and Blockchain Machine Coding rounds.

---

## 🛠️ Category 1: Core Blockchain & Cryptographic Data Structures
*Implement these using standard programming languages (JavaScript/TypeScript, Python, Rust, Go, etc.) without external blockchain libraries.*

### 1. Build a Mini Proof-of-Work Blockchain
Design and implement an in-memory blockchain ledger framework from scratch.
* **Requirements:**
    * Define a `Block` structure containing: `index`, `timestamp`, `transactions` (array), `previousHash`, `hash`, and `nonce`.
    * Implement a cryptographic hashing function (using SHA-256) to compute block hashes.
    * Implement a mining method (`mineBlock(difficulty)`) that finds a hash with a specific number of leading zeros.
    * Implement a `Blockchain` class with an `addBlock()` mechanism and a `isChainValid()` function that validates data immutability and hash links.

### 2. Merkle Tree & Whitelist Verification 
Implement a complete Merkle Tree structure used widely for airdrops and NFT whitelists.
* **Requirements:**
    * Write a class `MerkleTree` that takes an array of leaf strings (e.g., wallet addresses) and builds the tree hierarchy.
    * Generate the `getMerkleRoot()`.
    * Implement a `getProof(leaf)` function that returns the cryptographic proof path for a given leaf node.
    * Implement a standalone `verifyProof(leaf, proof, root)` function that returns a boolean.

### 3. UTXO (Unspent Transaction Output) Account Engine
Simulate the transactional architecture powering networks like Bitcoin.
* **Requirements:**
    * Define data models for `Transaction`, `TxInput` (referencing a previous transaction hash and output index), and `TxOutput` (amount and recipient public key).
    * Implement a processing pool that takes new incoming transactions, validates that inputs are unspent and their sums match or exceed the outputs, and updates an internal global `UTXOPool` state.

---

## 📜 Category 2: Smart Contract Systems (Solidity / Vyper / Rust)
*These challenges test gas optimization, security modifiers, structural state layouts, and protocol economics.*

### 4. Architectural Implementation of an ERC-20 Token Engine
Write an asset-compliant token engine featuring standard conditional validations.
* **Requirements:**
    * Maintain an internal tracking of `balances` and `allowances`.
    * Implement state change mechanics: `transfer`, `approve`, and `transferFrom`.
    * **Bonus / Advanced Constraint:** Add an internal governance snapshot feature or an optimized tracking logic preventing overflow/underflow patterns manually (simulate old environments or custom custom-safe logic).

### 5. Multi-Signature (Multi-Sig) Wallet Engine
Design an ecosystem vault requiring collective consensus for operations.
* **Requirements:**
    * Create a wallet initialized with an array of `owners` addresses and a required confirmation threshold `K` (e.g., 3 out of 5).
    * Implement `submitTransaction(destination, value, data)` returning a transaction ID.
    * Implement `confirmTransaction(txId)` and `revokeConfirmation(txId)`.
    * Implement `executeTransaction(txId)` which automatically checks if the confirmation count $\ge K$ before executing an internal low-level call. Prevent double execution.

### 6. Automated Market Maker (AMM) - Constant Product Pool
Implement a minimalist decentralized exchange (DEX) liquidity pool modeled after Uniswap V2 formulas.
* **Requirements:**
    * Enforce the constant product invariant formula: 
        $$x \cdot y = k$$
    * Implement `addLiquidity(amountA, amountB)` which mints LP tokens proportionally.
    * Implement `removeLiquidity(lpTokenAmount)` returning underlying token assets back to the liquidity provider.
    * Implement a `swap(tokenIn, amountIn)` function that dynamically calculates output fees and adjustments using the constant product model.

### 7. Decentralized Lending & Borrowing System (DeFi Minimal Engine)
Implement a raw architectural backbone for a collateralized pool (like a simplified Aave).
* **Requirements:**
    * Users can `deposit(token, amount)` to earn conceptual interest.
    * Users can `borrow(token, amount)` if they have deposited a separate collateral token type.
    * Enforce a Collateral Factor rule (e.g., users can borrow up to **80%** value of their deposited collateral asset).
    * Implement a public `liquidate(user)` function that evaluates if a user's health factor drops below 1, allowing arbitragers to repay debt in exchange for discounted collateral.

---

## 🌐 Category 3: Web3 Infrastructure & dApp Frontend Systems
*Focused on integration patterns using Ethers.js, Viem, Web3.js, or backend event consumers.*

### 8. Real-time Blockchain Event Indexer & Cache Engine
Build a standalone middleware application using Node.js/TypeScript or Python that handles smart contract event data tracking.
* **Requirements:**
    * Connect to a mock public JSON-RPC endpoint provider.
    * Poll or listen to raw Transfer events from a specific ERC-20 contract address.
    * Process and structure incoming raw hex logs into an optimized SQL/NoSQL schema or in-memory array data format.
    * Handle edge cases involving network drops or chain reorganization re-orgs (tracking block confirmations).

### 9. Multi-Wallet Transaction Batching Utility
Design a system or frontend component that orchestrates multiple transactions systematically.
* **Requirements:**
    * Accept an array of arbitrary target transaction objects.
    * Dynamically fetch the active nonces and calculate real-time gas limits (`eth_estimateGas`) sequentially.
    * Serialize, sign, and broadcast transactions safely, preventing transaction blockage if an early operation fails or experiences structural delays.



    ---

## ⚡ Category 4: Advanced DeFi & MEV (Maximal Extractable Value)
*These problems evaluate your understanding of asynchronous execution, transaction ordering, and algorithmic arbitrage.*

### 10. Multi-Hop Arbitrage Router (Flash Loan Execution)
Design a routing engine that identifies and executes cross-pool price discrepancies.
* **Requirements:**
    * Create a function `findArbitrageOpportunity(poolA, poolB, tokenPair)` that evaluates structural price divergence between two distinct AMM pools.
    * Implement a mock smart contract method `executeArbitrage()` that utilizes a **Flash Loan** (borrowing capital with 0 upfront collateral, provided it is paid back within the same transaction atomic block).
    * Ensure the engine calculates and factors in transaction gas fees dynamically before determining if the net profit is greater than zero ($Profit_{net} > 0$).

### 11. Mempool Transaction Sandbox (Front-running Simulator)
Build a JavaScript/Python script that acts as an isolated block-builder framework to simulate a front-running bot.
* **Requirements:**
    * Maintain a simulated queue of pending transactions ("Mempool") containing properties like `gasPrice`, `value`, `sender`, and `targetFunction`.
    * Write an algorithm that scans the mempool for large-volume target buy orders on an AMM.
    * Automatically inject a "front-run" buy transaction with higher `gasPrice` and a "back-run" sell transaction directly behind it, computing the precise slippage and extracted profit.

---

## 🔒 Category 5: Zero-Knowledge & Privacy Primitives
*Focused on cryptographic privacy engineering and identity patterns.*

### 12. Minimalist Crypto Mixer (Tornado Cash Architecture)
Implement a basic cryptographic mixer using commitments to anonymize token ownership.
* **Requirements:**
    * **Deposit Stage:** A user deposits a fixed asset amount and provides a secret cryptographic hash (`commitment = hash(nullifier, secret)`). The commitment is added to an on-chain Merkle tree.
    * **Withdrawal Stage:** To withdraw to a completely fresh, unlinked address, the user must provide a valid cryptographic proof showing they know a secret corresponding to an unspent commitment leaf in the tree without revealing *which* leaf it is.
    * Maintain an on-chain registry of spent `nullifiers` to completely prevent double-spending attacks.

---

## 🏗️ Category 6: Web3 System Design & State Architecture
*Broad systems problems requiring structured architecture diagrams, API paths, and state machine layout description.*

### 13. High-Throughput Gas Relayer & Account Abstraction (ERC-4337)
Design the end-to-end backend architecture for a Gas Relayer system that allows users to pay for gas using stablecoins (e.g., USDC) instead of native gas tokens (e.g., ETH).
* **System Components to Define:**
    * **User Operations:** The structure of a pseudo-transaction intent (`UserOperation`).
    * **Bundler Node:** A mempool aggregator that bundles multiple UserOperations into a single native transaction.
    * **Paymaster Contract:** The on-chain entity verifying the user has enough stablecoin balance to cover the gas before sponsoring the actual native transaction execution.
    * **Rate Limiting & DDOS Protection:** How to prevent malicious users from spamming invalid operations that drain the Bundler’s native gas during simulation.

### 14. Multi-Chain Cross-Bridge Monitor & Watcher Service
Design a resilient distributed microservice network tasked with watching bridging transactions across an L1 (e.g., Ethereum) and an L2 (e.g., Arbitrum).
* **System Components to Define:**
    * **Event Listeners:** Independent workers polling logs for `LockAsset` and `BurnAsset` events.
    * **Consensus/Validation Layer:** A distributed cluster of nodes that sign off on transactions to verify validity before executing a `MintAsset` on the destination chain.
    * **Failure Recovery Queue:** A persistent queue handling state synchronization if the destination chain RPC experiences downtime, preventing dual-spend or lost-mint anomalies.

---

## 🏁 Evaluation Matrix for Machine Coding Rounds

When writing code for these prompts in an interview setting, production-grade readiness is judged on the following framework:

| Metric | Junior Engineer Expectation | Senior / Lead Engineer Expectation |
| :--- | :--- | :--- |
| **Security** | Avoids basic bugs. | Implements Reentrancy Guards, Access Controls (`onlyOwner`), and defends against flash-loan oracle manipulation. |
| **Gas Efficiency** | Functional code logic. | Uses `calldata`, avoids storage loops, packs variables structurally, uses custom errors over string reverts. |
| **Edge Cases** | Basic validation. | Explicit handling of overflow/underflows, 0-address inputs, zero-liquidity pools, and network RPC drops. |
| **Testing** | Manual testing logs. | Comprehensive unit tests covering both positive paths and deliberate exploit simulations (e.g., using Foundry or Hardhat). |




---

## 🧪 Category 7: Upgradability & Advanced Proxy Patterns
*Focused on smart contract lifecycle management, storage slot collisions, and initialization state preservation.*

### 15. Transparent Proxy Pattern (TPP) Engine
Implement the low-level architectural pattern used to upgrade smart contracts without changing their deployment address.
* **Requirements:**
    * Create a `Proxy` contract and an `Implementation` contract (V1).
    * Write the custom assembly fallback function (`fallback()`) inside the proxy using `delegatecall` to forward all execution data to the implementation contract while preserving `msg.sender` and `msg.value`.
    * Enforce strict caller segregation: if the `ProxyAdmin` calls the proxy, it interacts with upgrade functions; if any other address calls it, the call is immediately delegated.
    * Implement an upgrade mechanism to point the proxy safely to an `ImplementationV2` contract without corrupting existing storage slots.

### 16. Diamond Pattern Multi-Facet Router (ERC-2535)
Design a highly modular smart contract system that bypasses the 24KB EVM contract size limit by mapping functions to specific facet addresses.
* **Requirements:**
    * Create a central `Diamond` contract that maintains a single registry map: `bytes4 selector => address facetAddress`.
    * Write a clean dynamic routing mechanism within the `fallback()` function that parses incoming `msg.sig` data, lookups the corresponding facet, and executes a `delegatecall`.
    * Implement an internal administrative framework (`diamondCut`) to add, replace, or remove function selectors dynamically while keeping storage layouts perfectly aligned.

---

## 🧮 Category 8: Advanced Algorithms & Native Protocol Math
*Deep optimization logic handling raw data processing, curve calculations, and scaling.*

### 17. Fixed-Point Math Engine for DeFi Pricing
Raw EVM does not support floating-point numbers (`float` or `double`). Implement a custom mathematical library designed to handle precision calculations safely.
* **Requirements:**
    * Establish a base scale standard (e.g., Wad with 18 decimals, or Ray with 27 decimals).
    * Write a `wadMul(uint256 x, uint256 y)` function that computes $(x \cdot y) / 10^{18}$ with proper geometric rounding logic to prevent dust leakages.
    * Write a `wadDiv(uint256 x, uint256 y)` function that computes $(x \cdot 10^{18}) / y$ while proactively validating that $y \neq 0$ and checking for potential overflows before execution.

### 18. Dynamic Gas-Optimized Order Book Matcher
Build an on-chain/hybrid limit order book engine optimized to match buyers and sellers with minimal gas loops.
* **Requirements:**
    * Design a data structure to store buy and sell limit orders using a combination of mapping and doubly-linked lists sorted by price-time priority.
    * Implement a `submitOrder(side, price, amount)` function.
    * Implement a matching execution loop that walks down the opposite side of the book to clear orders if prices cross. 
    * **Gas Constraints:** Ensure that removing or inserting elements into the sorted queue is an $O(1)$ operation to prevent out-of-gas errors when the order book grows large.

---

## 🏁 How to Ace the Machine Coding Round: Step-by-Step Execution Playbook

When handed your prompt during an active 60-to-90-minute coding session, follow this structural workflow to maximize your score:

### 1. The Clarification Phase (First 5-10 Minutes)
Never start coding instantly. Clarify architectural bounds with the interviewer:
* *“Should I write this as a pure local runtime module using in-memory variables, or should I structure it fully as valid Solidity/Hardhat environment code?”*
* *“Do we need to handle full mathematical precision tracking (like custom 18-decimal scaling), or can we assume standard safe integer limits for the sake of the MVP time constraint?”*

### 2. Scaffold the Interfaces
Draft the programmatic signatures first. If you are writing a smart contract, lay out the state variables, events, and explicit interface methods (`external`, `public`, `view`). This proves you understand the programmatic layout before worrying about the internal loops.

### 3. Write Core Business Logic & Defensive Guards
Implement the happy path first, but interleave structural invariants directly.
* Use `require()` or custom `error` statements to enforce access control (`onlyOwner`) and state correctness early in the function execution lifecycle.
* Strictly adhere to the **Checks-Effects-Interactions (CEI)** pattern: modify internal state structures *before* making any external calls or token transfers to systematically eliminate reentrancy vulnerabilities.


---

## 🏗️ Category 9: Layer 2, Cross-Chain, and Rollup State Verifiers
*Focused on cross-L1/L2 messaging patterns, state roots, and fraud/validity verification architectures.*

### 19. Optimistic Rollup Fraud Proof Window Simulator
Build a localized state validation engine that simulates how an L1 smart contract arbitrates state disputes from an L2 sequencer.
* **Requirements:**
    * Design an `L1RollupMock` contract that accepts batch submissions (`submitBatch(stateRoot, txMerkleRoot, blockNumber)`) from a designated `Sequencer` address.
    * Implement a challenge window mechanism (e.g., a 7-day timestamp lock) during which any `Validator` can call `challengeBatch(blockNumber, proof)`.
    * Implement the settlement logic: if a proof successfully proves a state mismatch using a step-by-step execution trace evaluation, slash the sequencer’s bond and revert the state root.

### 20. Cross-Chain Messaging Bridge Relayer (Lock-and-Mint)
Implement the core smart contract primitives required to pass assets safely between an Origin chain and a Destination chain.
* **Requirements:**
    * **BridgeSource (Chain A):** Implement a `lockTokens(address token, uint256 amount, uint256 targetChainId, address recipient)` function that transfers tokens to the bridge contract and emits a detailed `TokensLocked` event log.
    * **BridgeDestination (Chain B):** Implement a `mintWrappedTokens(bytes32 transactionHash, bytes signatures, address recipient, uint256 amount)` function.
    * **Security Constraint:** Ensure the destination contract tracks processed transaction hashes to guarantee **strict replay protection**, ensuring a single bridge transaction cannot be used to mint assets multiple times.

---

## 💻 Category 10: Advanced Frontend & Provider Performance Engineering
*Focused on high-performance Web3 UI engineering, RPC lifecycle optimization, and wallet state syncs.*

### 21. Multi-RPC Failover and Race Provider Engine
In production dApps, relying on a single RPC endpoint (like Infura or Alchemy) can lead to intermittent downtime or rate-limiting. Build a custom wrapper class using TypeScript or Python.
* **Requirements:**
    * Initialize the engine with an array of 3–5 different RPC provider URLs.
    * Implement a fallback strategy: if a request fails or timeouts ($> 2000\text{ ms}$), automatically route the call to the next available provider.
    * **Advanced Constraint (Race Condition Mode):** Implement a `fetchFastestBlock()` method that fires the same request to *all* provided RPCs simultaneously, returning the data from whichever provider responds first, while gracefully canceling the remaining pending promises.

### 22. Infinite-Scroll Event Log Virtualizer
Design the core component logic for an Etherscan-like frontend dashboard that reads and renders thousands of historical token transfer events smoothly without lagging the browser DOM.
* **Requirements:**
    * Implement a pagination block crawler that fetches historical events via JSON-RPC in optimized chunk sizes (e.g., 50,000 blocks per request).
    * Feed incoming event arrays into a virtualized list indexer that only renders items visible within the viewport.
    * Cache historical data locally in `IndexedDB` or `localStorage` to avoid duplicate RPC calls when the user refreshes the page or scrolls backward.

---

## 🛠️ The Local Production Setup Checklist

When entered into a machine coding environment, you are typically expected to configure your environment swiftly. Use this checklist to set up your boilerplate in under 3 minutes:

### For Smart Contract Challenges (Hardhat / Foundry)
* **Foundry (Recommended for Speed):** ```bash
  forge init --vscode