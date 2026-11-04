## Chapter 11: Quantum Computing Threats and Post-Quantum Cryptography — Practice Questions

**Q1.** A bank's PKI relies entirely on RSA-2048 for key exchange and ECDSA P-256 for signatures. A CISO must justify a migration budget to the board by explaining the quantum threat. Which explanation is technically accurate?

A) Grover's algorithm will factor the RSA modulus in polynomial time, breaking key exchange immediately
B) Shor's algorithm solves the integer factorization and discrete logarithm problems in polynomial time on a sufficiently large quantum computer, breaking both RSA and ECDSA
C) Quantum computers only threaten symmetric ciphers like AES, so RSA and ECDSA are already quantum-safe
D) QKD must be deployed on all existing RSA links to make them quantum-resistant without any algorithm changes

<details>
<summary>Answer</summary>

**Correct: B**

Shor's algorithm gives a polynomial-time solution to integer factorization (breaks RSA) and discrete logarithm (breaks DH and ECC/ECDSA), which are exponential-time problems for classical computers.

**Why the others are wrong:**
- Grover's algorithm targets symmetric key search, not factoring — this swaps the two algorithms' purposes
- This is backwards: symmetric ciphers are only weakened (not broken) by Grover; asymmetric RSA/ECDSA are completely broken by Shor
- QKD distributes symmetric keys over quantum channels; it does not repair or replace the underlying RSA/ECDSA math, and doesn't retrofit onto existing algorithms

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A security architect is selecting a symmetric cipher for data that must remain confidential for 30+ years against future quantum adversaries. Which choice BEST accounts for Grover's algorithm?

A) AES-128, since Grover's algorithm only affects asymmetric algorithms
B) AES-256, since Grover's quadratic speedup reduces its effective security to 128 bits, still adequate
C) 3DES, since triple encryption compensates for quantum speedup
D) RSA-4096 used symmetrically after key derivation

<details>
<summary>Answer</summary>

**Correct: B**

Grover's algorithm provides a quadratic speedup for brute-forcing symmetric keys, effectively halving the key strength in bits. AES-256 drops to an effective 128-bit quantum security level, which remains acceptable long-term.

**Why the others are wrong:**
- Grover's algorithm directly threatens symmetric ciphers by halving their effective key strength; AES-128 would drop to only 64-bit quantum security, considered inadequate
- 3DES has a small effective key size (~112 bits classically) and is deprecated; quantum speedup makes it far worse, not compensated
- RSA is asymmetric and broken outright by Shor's algorithm — it cannot be repurposed as a quantum-safe symmetric primitive

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An organization wants to detect any eavesdropping attempt on a fiber link used to distribute a symmetric key, leveraging the physical properties of quantum states rather than computational hardness assumptions. Which technology BEST meets this requirement?

A) ML-KEM (Kyber) key encapsulation over the fiber link
B) Elliptic Curve Diffie-Hellman with ephemeral keys
C) SLH-DSA hash-based signatures applied to the transmitted key
D) Quantum Key Distribution using the BB84 protocol

<details>
<summary>Answer</summary>

**Correct: D**

BB84 uses photons encoded in non-orthogonal polarization bases; the no-cloning theorem and measurement disturbance mean any eavesdropping attempt introduces detectable errors in the key exchange, providing physics-based (not computational) security.

**Why the others are wrong:**
- ML-KEM is a post-quantum computational scheme (lattice-based); it provides no physical eavesdropping detection
- ECDH is a classical asymmetric scheme broken by Shor's algorithm and offers no eavesdropper detection
- SLH-DSA is a signature scheme for authenticity/integrity, not a key distribution mechanism with eavesdrop detection

</details>

---

**Q4.** Which pairing correctly matches the NIST-selected post-quantum algorithm with its primary function and underlying hard problem?

A) ML-DSA (Dilithium) — key encapsulation — based on code-based cryptography
B) ML-KEM (Kyber) — key encapsulation — based on lattice (Module-LWE) problems
C) ML-KEM (Kyber) — digital signatures — based on hash-based cryptography
D) SLH-DSA (SPHINCS+) — key encapsulation — based on lattice problems

<details>
<summary>Answer</summary>

**Correct: B**

ML-KEM, standardized as FIPS 203, is a key encapsulation mechanism derived from CRYSTALS-Kyber, and its security rests on the hardness of the Module Learning With Errors (Module-LWE) lattice problem.

**Why the others are wrong:**
- ML-DSA (Dilithium, FIPS 204) is a digital signature scheme based on lattice problems, not key encapsulation, and not code-based
- ML-KEM's function is key encapsulation, not signatures, and it is lattice-based, not hash-based
- SLH-DSA (SPHINCS+, FIPS 205) is a hash-based signature scheme, not a key encapsulation mechanism and not lattice-based

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** An engineer configuring a TLS 1.3 server for post-quantum readiness must choose a key exchange group. Which single configuration choice provides quantum-resistant key establishment per current NIST guidance?

A) Configure the server to use x25519 exclusively for forward secrecy
B) Configure the server to disable key exchange and rely solely on RSA-4096 certificates
C) Configure the server to use SLH-DSA as the key exchange mechanism
D) Configure the server to negotiate a hybrid group combining X25519 with ML-KEM-768

<details>
<summary>Answer</summary>

**Correct: D**

Hybrid key exchange (e.g., X25519 combined with ML-KEM-768) is the recommended transitional configuration: it preserves classical security guarantees while adding quantum resistance from the lattice-based KEM, protecting against harvest-now-decrypt-later attacks.

**Why the others are wrong:**
- X25519 alone is elliptic-curve based and fully broken by Shor's algorithm on a sufficiently powerful quantum computer
- RSA-4096 is also broken by Shor's algorithm; larger key size does not confer quantum resistance for factoring-based schemes
- SLH-DSA is a signature algorithm, not a key exchange/encapsulation mechanism, and cannot be used for key establishment

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A developer is told the qubit register in a target quantum algorithm exhibits superposition. Which statement correctly describes this property in the context of the exam's quantum computing coverage?

A) The qubit can only be in state 0 or state 1 at any measured instant, identical to a classical bit
B) A qubit can represent a combination of both 0 and 1 states simultaneously until measured, enabling parallel evaluation of possibilities
C) Superposition means multiple qubits are physically entangled and cannot be measured independently
D) Superposition refers to the classical technique of pipelining instructions in parallel CPU cores

<details>
<summary>Answer</summary>

**Correct: B**

Superposition allows a qubit to exist in a linear combination of |0> and |1> states simultaneously, and this property underlies the parallel evaluation that gives quantum algorithms like Shor's and Grover's their speedup, collapsing to a definite state only upon measurement.

**Why the others are wrong:**
- This describes a classical bit's behavior, the opposite of superposition
- This describes entanglement, a related but distinct quantum property, not superposition
- This confuses a classical computer architecture concept (instruction pipelining) with a quantum mechanical property

</details>

---

**Q7.** A company needs to select a long-term digital signature algorithm for firmware signing that must survive both classical and quantum cryptanalysis, minimizing reliance on newer, less-analyzed mathematical assumptions, even at the cost of larger signature sizes. Which solution BEST meets these requirements?

A) ECDSA P-384 for its widely-implemented efficient signatures
B) SLH-DSA (SPHINCS+), a hash-based signature scheme relying only on the security of an underlying hash function
C) ML-DSA (Dilithium) using lattice-based Module-LWE/Module-SIS assumptions
D) RSA-PSS with 4096-bit keys for backward compatibility

<details>
<summary>Answer</summary>

**Correct: B**

SLH-DSA (SPHINCS+) is hash-based, deriving security purely from the collision/preimage resistance of the underlying hash function — a well-studied, conservative assumption — making it the preferred choice when minimizing reliance on newer number-theoretic assumptions is the priority, despite larger signature sizes.

**Why the others are wrong:**
- ECDSA relies on elliptic curve discrete logarithm hardness, which Shor's algorithm breaks entirely — not quantum-safe
- ML-DSA is quantum-resistant but relies on comparatively newer lattice assumptions, which the requirement explicitly wants to minimize
- RSA-PSS relies on integer factorization, broken by Shor's algorithm regardless of key size

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** During an audit, a security team observes that all outbound TLS sessions use ECDHE-RSA cipher suites with no post-quantum hybrid support. An adversary is suspected of recording encrypted traffic today to decrypt later once quantum computers mature. Which attack model does this describe, and which mitigation is MOST appropriate?

A) This is a replay attack; mitigate by adding nonces to each TLS session
B) This is a man-in-the-middle attack; mitigate by pinning the RSA certificate
C) This is a harvest-now-decrypt-later attack; mitigate by deploying hybrid post-quantum key exchange (e.g., X25519+ML-KEM) now
D) This is a downgrade attack; mitigate by disabling TLS 1.2 fallback only

<details>
<summary>Answer</summary>

**Correct: C**

Harvest-now-decrypt-later describes adversaries capturing quantum-vulnerable encrypted traffic today with intent to decrypt it once cryptographically-relevant quantum computers exist; the appropriate mitigation is adopting quantum-resistant or hybrid key exchange immediately, since current traffic recorded now remains exposed regardless of future patches.

**Why the others are wrong:**
- Replay attacks involve re-sending captured messages for reuse, not future decryption of confidentiality-protected data
- Certificate pinning addresses impersonation/MITM risk, not the long-term confidentiality exposure from quantum-capable decryption
- Downgrade attacks target protocol version negotiation; disabling TLS 1.2 doesn't address the quantum-vulnerable key exchange math used even in TLS 1.3 ECDHE-RSA

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

