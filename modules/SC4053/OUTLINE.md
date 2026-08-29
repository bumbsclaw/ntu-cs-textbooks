# SC4053 Blockchain Technology -- Textbook Outline (0->100)

**Code:** SC4053 . **AU:** 3 . **Type:** MPE (4x SC4xxx) . **Prereq graph:** SC2005 -> SC3010 -> SC4053
**Focus:** Decentralised ledgers, consensus, cryptography, smart contracts, scaling and tokenomics -- from hash chains to rollups.
**Position:** Builds on SC2005 (OS, concurrency, storage) and SC3010 (crypto, signatures, hash, threat models) to build trust without a trusted party.
**Sources:** NTU CCDS MPE catalogue, Nakamoto (2008), Wood (Ethereum Yellow Paper), Narayanan et al. -- Bitcoin and Cryptocurrency Technologies (Princeton).

## Prerequisite Graph & Positioning
```
SC1003 -> SC1007 -> SC2001 \
SC1005 -> SC1006 -> SC2005 -> SC3010 -> SC4053  (Systems->Security->Blockchain)
SC2000 + SC1004 -> SC2008 (networking supports P2P intuition)
SC2002 -> SC2006 (software engineering supports contract design)
```
SC4053 is a capstone MPE that synthesises systems, security and networking. Students should have completed SC2005 (processes, threads, storage) and SC3010 (CIA, hash, signatures, authentication) before attempting SC4053; SC2008 (networks) and SC2006 (SE) are recommended co-knowledge for P2P and contract testing.

## Overview
SC4053 constructs a blockchain from scratch. SC2005 taught processes, networking and persistence; SC3010 gave hash functions, signatures and the adversary. SC4053 combines them into an append-only replicated log replicated over an open P2P network where participants may crash, lie, or collude. From zero: hashes, linked lists and public-key intuition are rebuilt before any block is mined. Intuition (story/analogy) -> formal model (definitions/theorems) -> worked example (code/trace) -> exercise (attack/defend/build) per concept. Graduates can read a whitepaper, audit a contract, and reason about finality, MEV and scaling trade-offs. Aligns 1-to-1 with `main.tex` 8-chapter scaffold `ch01-foundations` ... `ch08-applications`.

## Chapter Breakdown (8 chapters, 0->100)

### Ch1 -- Blockchain Foundations & Hash Chains (`ch01-foundations`)
Outcomes: (1) define hash-linked chains and tamper evidence; (2) explain decentralisation vs distribution vs replication; (3) compute genesis->tip verification.
TikZ: (1) hash-chain with prev-hash arrows, tamper ripple in red!15 with legend; (2) centralised vs decentralised vs distributed topology comparison blue!15/green!15/orange!15; (3) block anatomy (header/body/nonce/Merkle root) with fills.
lstlisting: Python -- SHA-256 hash chain builder and tamper detector; Python -- block header serialiser.
Exercises: tamper a middle block and show avalanche; compare Git vs blockchain linking; genesis-block design debate.

### Ch2 -- Consensus: PoW, PoS and BFT (`ch02-consensus`)
Outcomes: (1) derive PoW difficulty and expected block time; (2) contrast PoW/PoS/BFT safety/liveness; (3) explain finality (probabilistic vs deterministic) and nothing-at-stake.
TikZ: (1) mining race with nonce search and difficulty target bar blue!12/red!14; (2) PoS validator lottery vs PoW hash-power pie, with slashing arrow; (3) PBFT 3-phase (pre-prepare/prepare/commit) swimlane green!15/blue!12/orange!15.
lstlisting: Python -- PoW miner loop with target check; Python -- PoS lottery weighted by stake.
Exercises: compute PoW success probability; simulate selfish mining; argue BFT 3f+1 bound.

### Ch3 -- Transactions, UTXO and Account Models (`ch03-transactions`)
Outcomes: (1) model UTXO graphs and double-spend prevention; (2) contrast UTXO vs account model (Ethereum); (3) trace fee, nonce and replay protection.
TikZ: (1) UTXO DAG with inputs/outputs/consumed coins, fills green!15/red!12; (2) account-model state transition (nonce/balance/code) blue!15/yellow!16; (3) mempool -> block packing with fee ordering violet!10.
lstlisting: Python -- UTXO validator (no double-spend, conservation); Python -- account nonce checker and fee estimator.
Exercises: build a UTXO double-spend attempt; replay attack without chain-id; fee-market simulation.

### Ch4 -- Smart Contracts: Solidity and the EVM (`ch04-contracts`)
Outcomes: (1) write/deploy a Solidity contract and trace EVM execution (gas, storage, calldata); (2) explain ABI, events and reentrancy; (3) test with Foundry/Hardhat.
TikZ: (1) EVM stack-machine with gas meter, storage vs memory vs calldata violet!10/orange!15; (2) contract call graph with delegatecall and reentrancy arrow red!15; (3) deployment pipeline (compile->ABI->deploy->verify) blue!12/green!15.
lstlisting: Solidity (via Java highlighting) -- ERC-20 + reentrancy guard; Python -- EVM gas-cost estimator and ABI encoder.
Exercises: exploit and fix reentrancy; estimate gas table; emit and filter events.

### Ch5 -- Cryptography: Signatures, Merkle Trees and Commitments (`ch05-crypto`)
Outcomes: (1) apply ECDSA/secp256k1 signatures and address derivation; (2) prove inclusion with Merkle proofs O(log n); (3) use commitments and zero-knowledge intuition.
TikZ: (1) ECDSA sign/verify flow with keypair -> address via hash, fills blue!15/green!15; (2) Merkle tree with proof path highlighted orange!15/red!12 and legend; (3) commitment open/verify plus ZK intuition (prover/verifier) violet!10.
lstlisting: Python -- ECDSA sign/verify with ecdsa lib + Merkle proof verifier; Python -- Pedersen commitment demo.
Exercises: forge without private key (discrete-log hardness); verify Merkle proof manually; hide-then-reveal commitment game.

### Ch6 -- Scaling: Channels, Rollups and Sharding (`ch06-scaling`)
Outcomes: (1) reason about throughput trilemma; (2) explain payment channels and rollup data (optimistic vs ZK) and fraud/validity proofs; (3) sketch sharding and data availability.
TikZ: (1) payment channel lifecycle (open->off-chain->close/dispute) green!15/blue!12; (2) rollup batching L2->L1 with sequencer, bridge, fraud window orange!15/violet!10; (3) sharding with beacon chain and cross-shard commits yellow!16/red!12.
lstlisting: Python -- payment channel state updates + HTLC; Python -- rollup batch compressor and fraud-proof checker.
Exercises: channel griefing scenario; compare optimistic vs ZK costs; data-availability sampling intuition.

### Ch7 -- Security & Attacks: Double-Spend, MEV and Formal Verification (`ch07-security`)
Outcomes: (1) analyse 51%, eclipse, long-range and MEV/front-running; (2) model double-spend race and confirmations; (3) apply formal verification and audit checklist.
TikZ: (1) double-spend fork race with attacker chain overtaking honest chain red!15/green!15; (2) MEV supply chain (searcher->builder->proposer) with PBS auction blue!15/orange!15; (3) verification pipeline (spec->model->solver) and audit matrix violet!10.
lstlisting: Python -- double-spend simulator with confirmations; Python -- MEV sandwich detector on mempool trace.
Exercises: compute k-confirmation safety; order transactions to extract MEV; write invariant for verification.

### Ch8 -- Applications, Tokenomics and Governance (`ch08-applications`)
Outcomes: (1) map DeFi/NFT/DAO/supply-chain patterns to contract primitives; (2) design tokenomics (supply, inflation, staking, bonding curves); (3) critique governance and regulation trade-offs.
TikZ: (1) DeFi stack (AMM->lending->oracle->aggregator) with token flows blue!15/green!15; (2) bonding curve and vesting schedule orange!15/yellow!16 with legend; (3) DAO governance lifecycle (propose->vote->timelock->execute) violet!10/blue!12.
lstlisting: Python -- AMM constant-product swap + bonding-curve pricer; Python -- DAO voting and timelock simulator.
Exercises: price AMM slippage; design token unlock schedule; analyse a DAO proposal game.

## Cross-Cutting Design
- **0->100 law:** every chapter starts with a concrete story (notebook, lottery, cheque, vending machine, wax seal, cafe tab, shop 0-conf, farmers' market) before formalism.
- **Intuition->Formal->Example->Exercise** enforced per section; 5 exercises per chapter (40 total) with attack/defend/build balance.
- **Prereq reuse:** SC2005 threads/locks motivate reentrancy; SC3010 hash/signature definitions are extended, not re-assumed; SC2008 networking frames P2P gossip.

## TikZ Plan Summary (2-3/ch, 20 total, color + legend)
Scale 0.80-0.90, fills blue!15/green!20/orange!15/violet!10/red!12/yellow!16 where useful; every figure labeled, 0 pgfkeys errors. Hash chains, topology triptych, mining races, BFT swimlanes, UTXO DAGs, EVM stacks, Merkle trees, channel/rollup/shard diagrams, fork races, MEV auctions, DeFi stacks, bonding curves.

## lstlisting Plan (Python + Solidity/Java)
Ch1 Python . Ch2 Python . Ch3 Python . Ch4 Solidity(Java)/Python . Ch5 Python . Ch6 Python . Ch7 Python . Ch8 Python via `\begin{lstlisting}[language=...]` with `lstset` colors (keyword blue!70!black, comment green!50!black, string orange!70!black), `xleftmargin=1.0em` -- never `verbatim`.

## Exercise Themes
Hash tampering labs; mining simulators; UTXO/account traces; Solidity CTF (capture-the-flag); Merkle proof drills; channel/rollup cost sheets; double-spend/MEV game analysis; tokenomics spreadsheets; audit checklists and invariant writing.

## Build Invariants & QA
0->100 ground-up (hashes/lists/signatures first, intuition->formal->example->exercise); color TikZ + highlighted `lstlisting`; small-screen 1.3/1.2 cm, `setstretch 1.20`; `pdflatex x2` -> 0 `!` 0 `pgfkeys` 0 `Overfull>15pt`; adversarial QA compile-checks all figures/code. Prereq chain SC2005->SC3010->SC4053 honoured throughout.
