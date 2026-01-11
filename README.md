# SP1 Privacy Mixer 🌪️

> **Status:** 🚧 Under Development (Week 0/8)
> **Goal:** POC of a non-custodial mixer leveraging zkVM (SP1) for off-chain computation and Groth16 for on-chain verification.

## 📐 Architecture

This project moves away from traditional circuit-DSL (Circom/Halo2) to a **Rust-native zkVM approach**. It aims to demonstrate the efficiency of small-field arithmetic (Goldilocks) for privacy-preserving protocols on Ethereum.

### Core Components
1.  **The Program (Guest):** Written in Rust. Handles the Merkle Tree insertion logic, secret management, and nullifier generation.
2.  **The Prover (Host):** Generates the SP1 STARK proof of correct execution.
3.  **The Verifier (On-Chain):**
    * **Layer 1:** SP1 STARK proof verification (Off-chain / Recursive).
    * **Layer 2:** Groth16 wrapper (SNARK) for cheap EVM gas verification.

## 🛠️ Tech Stack & Rationales

* **Language:** Rust 🦀 (Safety & Performance).
* **zkVM:** [SP1](https://github.com/succinctlabs/sp1) (Write Rust, prove execution).
* **Arithmetic Backend:** [Plonky3](https://github.com/Plonky3/Plonky3) (Leveraging Small Fields / Goldilocks Field for performance).
* **Hashing Strategy:** Comparative analysis of **Poseidon2** vs **Monolith**.
    * *Goal:* Benchmark cycle counts within SP1 (RISC-V) to determine the most efficient primitive for Merkle Tree operations over the Goldilocks field vs standard Keccak256 costs.

## 🗺️ Roadmap (8-Week Sprint)

- [ ] **Week 1-2:** Core Primitives (Poseidon2/Monolith benchmarking, Sparse Merkle Tree implementation in Rust).
- [ ] **Week 3-4:** Mixer Logic (Deposit/Withdraw circuits in SP1, Nullifier constraints).
- [ ] **Week 5:** Recursive Proving (STARK -> SNARK wrapping).
- [ ] **Week 6:** Solidity Verifier, Gas Optimization & EIP-4844 Blob integration study.
- [ ] **Week 7:** Frontend & CLI Integration.
- [ ] **Week 8:** Mainnet/Testnet Deployment & Technical Deep-Dive Write-up.

## 📚 References
* *Tornado Cash Whitepaper*
* *SP1 Documentation*
* *Ethereum Protocol Fellowship Wiki (Execution Layer Specs)*
* *Plonky3 Repository*

---
*Independent research project by hs1167, math student at Sorbonne University.*
