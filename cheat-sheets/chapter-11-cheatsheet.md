## Chapter 11 Cheat Sheet: Quantum & Post-Quantum Crypto (8% domain)

### Quantum Algorithm Threats
| Algorithm | Targets | Effect |
|---|---|---|
| Shor's algorithm | RSA (factoring), DH/ECC (discrete log) | Breaks completely in polynomial time |
| Grover's algorithm | Symmetric ciphers (AES), hash functions | Quadratic speedup — halves effective key strength in bits |

**Key rule:** Shor = breaks asymmetric math. Grover = weakens symmetric key search (doesn't break it outright).

### Symmetric Key Sizing Post-Grover
| Cipher | Classical strength | Quantum-effective strength | Adequate long-term? |
|---|---|---|---|
| AES-128 | 128-bit | 64-bit | No |
| AES-256 | 256-bit | 128-bit | Yes |

### NIST Post-Quantum Standards (finalized Aug 2024)
| Standard | FIPS # | Former name | Function | Hard problem |
|---|---|---|---|---|
| ML-KEM | FIPS 203 | CRYSTALS-Kyber | Key encapsulation | Module-LWE (lattice) |
| ML-DSA | FIPS 204 | CRYSTALS-Dilithium | Digital signatures | Module-LWE/SIS (lattice) |
| SLH-DSA | FIPS 205 | SPHINCS+ | Digital signatures | Hash-function security |

Additional draft standard: FN-DSA (Falcon) — lattice/NTRU-based signatures, smaller than ML-DSA.

### PQC Family Comparison
| Family | Example | Pros | Cons |
|---|---|---|---|
| Lattice-based | ML-KEM, ML-DSA, Falcon | Efficient, small keys/sigs | Newer assumptions |
| Hash-based | SLH-DSA | Very conservative security | Larger signatures, slower |
| Code-based | Classic McEliece | Long-studied hardness | Very large public keys |

### Quantum Basics
- **Qubit**: quantum bit, can be in **superposition** of 0 and 1 until measured.
- **Entanglement**: correlated qubit states, distinct from superposition.
- **QKD / BB84**: distributes symmetric keys using photon polarization in non-orthogonal bases; no-cloning theorem makes eavesdropping detectable. Physics-based security, not computational.

### Migration Guidance
- **Harvest-now-decrypt-later**: adversaries capture ciphertext today to decrypt once quantum computers mature — mitigate NOW, not later.
- **Hybrid key exchange** (e.g., X25519 + ML-KEM-768) recommended during transition — retains classical guarantee, adds quantum resistance.
- QKD ≠ replacement for PQC signatures; QKD only distributes symmetric keys, doesn't authenticate/sign.

### Exam Traps
1. Confusing Shor's (asymmetric) with Grover's (symmetric) targets.
2. Thinking AES-128 is quantum-safe (it isn't — only 64-bit effective).
3. Assuming larger RSA/ECC key sizes fix quantum vulnerability (they don't — Shor breaks any size in polynomial time relative to key size).
4. Mixing up ML-KEM (encapsulation) vs ML-DSA (signatures) functions.
5. Believing QKD alone provides full PKI replacement (it doesn't provide signatures).
