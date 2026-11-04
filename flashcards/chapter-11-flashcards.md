## Chapter 11: Quantum Computing Threats and Post-Quantum Cryptography — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | What does Shor's algorithm break, and why? | Breaks RSA (factoring), DH and ECC (discrete log) by solving both problems in polynomial time on a quantum computer. Exam tip: Shor = asymmetric crypto killer. |
| 2 | What does Grover's algorithm do to symmetric key search? | Provides quadratic speedup, effectively halving key strength in bits (AES-128 -> 64-bit quantum security). Exam tip: Grover = symmetric weakener, not breaker. |
| 3 | Recommended AES key size for long-term post-quantum security? | AES-256 (drops to effective 128-bit security under Grover, still adequate). AES-128 drops to 64-bit, considered inadequate long-term. |
| 4 | ML-KEM — what is it, formerly known as, and FIPS number? | Key Encapsulation Mechanism, formerly CRYSTALS-Kyber, standardized as FIPS 203. Based on Module-LWE lattice problem. |
| 5 | ML-DSA — what is it, formerly known as, and FIPS number? | Digital Signature Algorithm, formerly CRYSTALS-Dilithium, standardized as FIPS 204. Based on Module-LWE/Module-SIS lattice problems. |
| 6 | SLH-DSA — what is it, formerly known as, and FIPS number? | Stateless Hash-Based Digital Signature Algorithm, formerly SPHINCS+, standardized as FIPS 205. Security based purely on hash function properties, not lattice math. |
| 7 | What is BB84? | First Quantum Key Distribution (QKD) protocol (Bennett & Brassard, 1984). Uses photon polarization in two non-orthogonal bases; eavesdropping introduces detectable errors due to no-cloning theorem. |
| 8 | What is superposition in quantum computing? | A qubit can represent a combination of 0 and 1 simultaneously until measured. Enables quantum parallelism used by Shor's and Grover's algorithms. |
| 9 | Lattice-based vs hash-based vs code-based PQC — main tradeoff? | Lattice (ML-KEM/ML-DSA): efficient, smaller sizes, newer assumptions. Hash-based (SLH-DSA): conservative security, larger signatures. Code-based (e.g., Classic McEliece): large public keys, very mature hardness assumption. |
| 10 | What is 'harvest-now-decrypt-later'? | Adversary records quantum-vulnerable encrypted traffic today to decrypt once quantum computers are cryptographically relevant. Mitigation: deploy hybrid PQC key exchange now. |
| 11 | What is a common hybrid TLS key exchange configuration for PQC transition? | X25519 combined with ML-KEM-768 — preserves classical security while adding quantum resistance during migration period. |
| 12 | Why can't QKD (BB84) replace ML-KEM/ML-DSA for authentication? | QKD distributes symmetric keys via physics-based eavesdrop detection but requires dedicated quantum channels and doesn't provide digital signatures/authentication — PQC signature algorithms (ML-DSA, SLH-DSA) are still needed. |
