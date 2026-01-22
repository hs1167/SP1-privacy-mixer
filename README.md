# SP1 Privacy Mixer 🌪️

> **Status:** 🚧 Under Development (Week 2/10)
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

🗺️ Project Roadmap (10-Week Sprint)
This roadmap follows a strict linear progression: mastering the language first, then building the cryptographic primitives, and finally integrating the ZK logic.

🏗️ Phase 1: The Foundation (Weeks 2-3)
🎯 Current Status: 🟩🟩🟩🟩⬜⬜⬜⬜⬜⬜ 40%

Context: Before tackling the ZK-specific architecture, I am executing a high-intensity "Rust for Cryptography" sprint. I am strictly focusing on low-level safety to ensure production-grade hygiene.

Immediate Objectives:

[x] Ownership Semantics: Mastering move semantics to prevent secret leakage in memory.

[x] Core Implementation: Implementing Hash wrappers & Merkle structures from scratch in native Rust.

[wip] Custom Error Handling: Building robust Result types for cryptographic failures.

[ ] Trait Bounds & Generics: Essential for writing abstract, reusable ZK circuits.


🚀 Phase 2: The SP1 Build (Weeks 4-10)
Transitioning from native Rust to the SP1 zkVM environment.

Core Engineering (Weeks 4-5)

[ ] Benchmarking: Compare Poseidon2 vs Monolith performance inside the SP1 zkVM.

[ ] Data Structures: Implementation of a Sparse Merkle Tree (SMT) optimized for the Goldilocks field.

Mixer Logic & Constraints (Weeks 6-7)

[ ] Deposit Circuit: Note commitment generation logic.

[ ] Withdraw Circuit: SP1 program for Merkle inclusion proofs.

[ ] Constraint Security: Implementing Nullifier logic to strictly prevent double-spending.

Proving Architecture (Week 8)

[ ] Recursion: Implement the STARK -> SNARK wrapper (Groth16) for on-chain verification efficiency.

On-Chain Integration (Week 9)

[ ] Solidity Verifier: Deploying the auto-generated Groth16 verifier contract.

[ ] Optimization: Gas cost analysis & EIP-4844 Blob integration study for data availability.

Frontend & Release (Week 10)

[ ] CLI Integration: Building the user interface for note generation and proof submission.

[ ] Deployment: Mainnet/Testnet launch & Technical Deep-Dive write-up.

## 📚 References
* *Tornado Cash Whitepaper*
* *SP1 Documentation*
* *Ethereum Protocol Fellowship Wiki (Execution Layer Specs)*
* *Plonky3 Repository*

---
*Independent research project by [hs1167](https://github.com/hs1167), math student at Sorbonne University.*
