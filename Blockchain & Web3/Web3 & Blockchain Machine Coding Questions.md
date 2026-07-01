# Web3 & Blockchain Machine Coding Interview Questions

This repository contains a curated list of machine coding and hands-on implementation questions for Web3 and Blockchain Engineer roles. It is split into **Core Blockchain & Cryptography**, **Smart Contracts (Solidity)**, and **dApp Frontend/Integration**.

---

## 🚀 1. Core Blockchain & Cryptography (Data Structures & Infra)

These problems are typically solved using general-purpose languages like TypeScript, Go, Python, or Rust to test your foundational understanding of how blockchains operate under the hood.

### Q1: Implement a Merkle Tree
* **Problem:** Build a basic Merkle Tree data structure. 
* **Requirements:**
    * Accept an array of string data (leaf nodes).
    * Compute the cryptographic Merkle Root using `SHA-256`.
    * Handle an odd number of leaf nodes by duplicating the last node.
    * Write a function to generate a Merkle Proof (proof of inclusion) for a given leaf.
    * Write a verification function `verifyProof(leaf, proof, root)` that returns a boolean.

### Q2: Blockchain Chain Reorganization (Reorg) Simulator
* **Problem:** Write a conflict resolution module that simulates how a node handles network forks.
* **Requirements:**
    * Given a current `Main Chain` (linked list/array of blocks) and a competing `Forked Branch`.
    * Implement the **Longest Chain Rule** (or Heaviest Chain Rule) to determine validity.
    * If the fork is longer, execute a reorg: roll back transactions from the orphaned blocks and apply transactions from the new winning chain.

### Q3: UTXO Transaction Validator
* **Problem:** Simulate a simplified Bitcoin-style UTXO (Unspent Transaction Output) tracking system.
* **Requirements:**
    * Define a `Transaction` schema consisting of `Inputs` and `Outputs`.
    * Write a function `validateTransaction(tx, utxoPool)` that ensures:
        1. All referenced inputs exist in the pool and are unspent.
        2. Total input value $\ge$ Total output value.
        3. Signatures on inputs are cryptographically valid.
    * Update the global UTXO pool state upon successful validation.

### Q4: HD Wallet (Hierarchical Deterministic) Key Derivation
* **Problem:** Implement a module that derives child public/private keys from a seed phrase.
* **Requirements:**
    * Use BIP-39 to convert a mnemonic phrase into a binary seed.
    * Use BIP-32/BIP-44 standards to derive child keys along a path (e.g., `m/44'/60'/0'/0/0` for Ethereum).
    * Properly implement `HMAC-SHA512` hashing to split keys into private keys and chain codes.

---

## 📜 2. Smart Contracts (Solidity / EVM)

These machine coding questions evaluate your capability to write gas-optimized, secure, and exploit-resistant smart contracts.

### Q5: ERC-20 Token with Vesting Schedules
* **Problem:** Write a standard ERC-20 token contract that natively includes linear vesting for early investors.
* **Requirements:**
    * Implement an admin function `addVestingSchedule(address beneficiary, uint256 totalAmount, uint256 startTime, uint256 cliffDuration, uint256 totalDuration)`.
    * Modify the standard `transfer` and `transferFrom` functions to ensure users can only transfer tokens that have fully passed their cliff and vested linearly over time.

### Q6: Multi-Signature Wallet
* **Problem:** Create a secure, shared wallet contract (`MultiSigWallet.sol`).
* **Requirements:**
    * Initialized with an array of `owners` addresses and a `required` number of confirmations ($M$-of-$N$).
    * Functions: `submitTransaction`, `confirmTransaction`, and `executeTransaction`.
    * Ensure strict access control, protection against double-confirmations, and proper state updates before sending funds (to prevent reentrancy).

### Q7: Automated Market Maker (AMM) / Constant Product Pool
* **Problem:** Build a barebones decentralized exchange pool for two ERC-20 tokens using the $x \cdot y = k$ formula.
* **Requirements:**
    * `addLiquidity(uint256 amountA, uint256 amountB)`: Mints LP tokens to the provider proportional to their share.
    * `removeLiquidity(uint256 lpTokens)`: Burns LP tokens and returns underlying assets.
    * `swap(address tokenIn, uint256 amountIn)`: Calculates exact `amountOut` applying the constant product invariant formula, accounting for a $0.3\%$ pool fee.

### Q8: Secure Decentralized Auction (Preventing Denial of Service)
* **Problem:** Code an auction contract where users send ETH to bid. The highest bidder wins, and outbid users get refunded.
* **Requirements:**
    * **Crucial:** Do *not* push refunds automatically inside the `bid()` function (avoids DoS via external contract fallback rejection).
    * Implement the **Pull-over-Push pattern** via a separate `withdrawRefund()` function for outbid accounts.

---

## 🌐 3. dApp Integration & Frontend Coding (Web3.js / Ethers.js / Viem)

These tasks evaluate your ability to link a UI or backend script to live blockchain nodes and contract states.

### Q9: Event Listener and Indexer Script
* **Problem:** Write a Node.js script using `ethers.js` or `viem` to poll and parse real-time logs.
* **Requirements:**
    * Connect to a public RPC provider websocket or HTTP endpoint.
    * Listen for `Transfer` events from a specific ERC-721 (NFT) contract.
    * Parse the indexed parameters (`from`, `to`, `tokenId`).
    * Write the filtered data stream cleanly into a local SQLite/JSON file database.

### Q10: Custom Gas Estimator & Multi-Call Aggregator
* **Problem:** Build a utility service that batches multiple read operations into one RPC call to optimize network roundtrips.
* **Requirements:**
    * Implement a script that accepts an array of contract addresses and token IDs.
    * Use an EVM `Multicall` architecture to fetch balances or URIs for all entries simultaneously.
    * Dynamically fetch the historical base fee from the last 5 blocks to suggest `maxFeePerGas` and `maxPriorityFeePerGas`.

### Q11: Wallet Connect & Signature Authentication Flow
* **Problem:** Create a minimal client-side app (React/Vanilla JS) for Sign-In with Ethereum (SIWE).
* **Requirements:**
    * Provide a button to connect MetaMask / WalletConnect.
    * Request a cryptographically random challenge/nonce from a backend server.
    * Prompt the user to sign a structured message (containing the nonce and timestamp) via their wallet.
    * Forward the cryptographic signature to the backend server for public key verification using `ecrecover`.





    ---

## 🔒 4. Advanced Security, DeFi, & Protocol Logic

These questions simulate advanced infrastructure scenarios, MEV (Maximal Extractable Value) concepts, and complex financial mechanisms frequently encountered in Senior Web3 Engineer interviews.

### Q12: Flash Loan Receiver & Arbitrage Executer
* **Problem:** Write a Solidity smart contract (`FlashLoanArbitrage.sol`) that interfaces with a lending protocol (like Aave) to execute a risk-free cross-dex arbitrage.
* **Requirements:**
    * Implement the protocol's required callback function (e.g., `executeOperation`).
    * The workflow must:
        1. Borrow Asset X from the lending pool.
        2. Swap Asset X for Asset Y on AMM A.
        3. Swap Asset Y back to Asset X on AMM B where the price is higher.
        4. Repay the original flash loan principal + premium fee.
    * Ensure the entire transaction reverts if the final profit is negative (fails to cover the flash loan fee or gas).

### Q13: TWAP (Time-Weighted Average Price) Oracle Observer
* **Problem:** Build a mechanism to resist price manipulation attacks by tracking cumulative price assets over time.
* **Requirements:**
    * Create a contract that samples the price of an AMM pool at regular, checkpointed intervals.
    * Implement cumulative price variables that increment by $\text{price} \times \text{time elapsed}$ since the last update.
    * Write a public function `getTwapPrice(uint256 period)` that securely computes the average asset price over the designated lookback window.

### Q14: ERC-4337 Account Abstraction Wallet (Minimalist Smart Wallet)
* **Problem:** Implement a minimal smart contract wallet that adheres to the ERC-4337 Account Abstraction standard.
* **Requirements:**
    * Replace traditional ECDSA EOA (Externally Owned Account) validation with a programmable verification function.
    * Code a `validateUserOp` function that accepts a `UserOperation` struct, validates a custom signature (e.g., a multisig signature or passkey), pays the bundler for gas fees using the wallet's deposit, and returns a validation status code.

### Q15: Gasless Meta-Transaction Handler (ERC-2771 Compliant)
* **Problem:** Implement a system where users can interact with your dApp contracts without paying gas, delegating the gas payment to a trusted forwarder/relayer network.
* **Requirements:**
    * Modify a target smart contract to inherit from or support `ERC2771Recipient`.
    * Implement custom internal functions `_msgSender()` and `_msgData()` that strip the appended origin address if called by the trusted forwarder.
    * Write a backend Node.js script that signs the native transaction data EIP-712 payload and submits it via a relayer address.

---

## 🛠️ 5. Systems, Storage, & L2 Scaling Solutions

These problems cover integration with decentralized filesystems and the structural layers of optimistic and zero-knowledge rollups.

### Q16: Decentralized IPFS Content Pinning & Metadata Generator
* **Problem:** Code a production-grade asset pipeline that uploads dynamic NFT collections to decentralized storage.
* **Requirements:**
    * Write a script using the IPFS HTTP Client or Helia.
    * Accept a folder of local high-resolution raw images.
    * Sequentially upload the images to IPFS, capture their Content Identifiers (CIDs), and dynamically generate valid ERC-721 JSON metadata schemas referencing those CIDs.
    * Batch upload the resulting metadata directory to IPFS and output the root CID directory string.

### Q17: Rollup State Transition & Fraud Proof Verifier
* **Problem:** Write a lightweight execution environment simulating an Optimistic Rollup's L1 fraud proof challenger challenge loop.
* **Requirements:**
    * Define a basic state machine where state is tracked by a simple root hash (e.g., tracking account balances).
    * Accept a batch of off-chain state transitions (transactions).
    * Write a verification function `verifyStateTransition(bytes32 preStateRoot, bytes32 postStateRoot, Transaction[] txs, MerkleProof[] proofs)` that validates if the off-chain sequencer processed the state transitions accurately according to L1 rules. Return an explicit fraud alert if any invalid transition is found.

### Q18: Gas-Optimized Token Airdrop Distributor (Bitmap vs Merkle)
* **Problem:** Design an efficient system to distribute tokens to $100,000+$ eligible user addresses on-chain.
* **Requirements:**
    * Compare a naive approach (mapping lookups) against a Merkle Tree distribution system.
    * Implement a gas-optimized tracking system using a **BitMap** (`uint256` slots) inside the claim verification function to store the claim status of each index.
    * Show how tracking claims via bits drastically cuts storage write ($SSTORE$) costs on the EVM compared to using a `mapping(address => bool)`.




    ---

## 🏗️ 6. Cross-Chain & Interoperability Protocols

These problems evaluate your ability to handle multi-chain architectures, state synchronization, and secure cross-chain messaging patterns.

### Q19: Cross-Chain Bridge Token Wrapper
* **Problem:** Build a secure, bidirectional token bridge contract mechanism (Lock/Mint and Burn/Release model).
* **Requirements:**
    * Create a `BridgeSource.sol` contract on Chain A that locks native tokens and emits a `TokensLocked` event with a unique nonce, destination address, and amount.
    * Create a `BridgeDestination.sol` contract on Chain B that accepts a signed proof from a decentralized relayer network to mint corresponding wrapped tokens (`wToken`).
    * Implement a replay protection tracking system using cryptographic nonces to ensure no bridge message can be executed more than once.

### Q20: Cross-Chain Messaging via LayerZero / CCIP
* **Problem:** Implement a cross-chain state synchronizer that sends a payload from a contract on Polygon to a contract on Arbitrum.
* **Requirements:**
    * Interface with a major cross-chain messaging standard (e.g., Chainlink CCIP or LayerZero).
    * Implement the receiving contract interface to parse incoming bytes payloads securely.
    * Add custom access control layers ensuring the destination contract *only* accepts execution calls originating from the specific trusted source contract address on the source chain.

---

## 🧪 7. Tips for Cracking Web3 Machine Coding Interviews

When faced with these problems in a live setting, remember to focus on the following:

* **Security First:** Always check for common vulnerabilities like reentrancy, integer overflows/underflows (if using Solidity <0.8), front-running, and unauthorized access control (`msg.sender` validation).
* **Gas Optimization:** In Solidity, storage operations ($SSTORE$) are incredibly expensive. Use memory or calldata arrays, cache state variables locally, pack storage variables ($uint128$ side-by-side), and use bitmaps when applicable.
* **Comprehensive Testing:** Be prepared to write custom deployment scripts and unit test suites using frameworks like **Foundry** (Solidity) or **Hardhat** (TypeScript) to verify edge cases such as zero-address transfers and boundary values.


