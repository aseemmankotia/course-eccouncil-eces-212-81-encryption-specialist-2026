## Chapter 5: Number Theory Foundations for Asymmetric Crypto — Practice Questions

**Q1.** During RSA key generation you select primes p=61 and q=53. What is φ(n)?

A) 3233
B) 3172
C) 3120
D) 3060

<details>
<summary>Answer</summary>

**Correct: C**

φ(n) = (p-1)(q-1) = 60 × 52 = 3120.

**Why the others are wrong:**
- 3233 is n = p×q, not φ(n) — a classic mix-up between modulus and totient.
- 3172 results from mistakenly computing p×(q-1) = 61×52 instead of (p-1)(q-1).
- 3060 results from computing (p-1)(q-2) = 60×51 instead of the correct formula.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A researcher wants to find a collision in SHA-256 (256-bit output) using a birthday attack. Approximately how many hash computations are needed for a 50% chance of success?

A) 2^256
B) 2^64
C) 2^128
D) 2^32

<details>
<summary>Answer</summary>

**Correct: C**

The birthday bound for an n-bit hash is roughly 2^(n/2), so 256/2 = 128.

**Why the others are wrong:**
- 2^256 is the preimage-resistance strength, not the collision (birthday) bound.
- 2^64 is the birthday bound for a 128-bit hash like MD5, not SHA-256.
- 2^32 has no relevance to a 256-bit hash's security bound.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which cryptographic scheme's security relies directly on the hardness of the Discrete Logarithm Problem?

A) Diffie-Hellman Key Exchange
B) RSA
C) AES
D) SHA-256

<details>
<summary>Answer</summary>

**Correct: A**

Diffie-Hellman security depends on the infeasibility of computing discrete logs modulo a large prime.

**Why the others are wrong:**
- RSA's hardness assumption is integer factorization, not discrete log.
- AES is a symmetric block cipher with no number-theoretic hardness assumption.
- SHA-256 is a hash function; its security relies on collision/preimage resistance, not discrete log.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** DSA (Digital Signature Algorithm) bases its security on which hard problem, distinguishing it from RSA-based signatures?

A) Integer factorization
B) Birthday paradox
C) Elliptic curve point multiplication
D) Discrete logarithm problem

<details>
<summary>Answer</summary>

**Correct: D**

DSA's security is based on the discrete logarithm problem in a finite field (mod p group).

**Why the others are wrong:**
- Integer factorization is the hardness assumption underlying RSA, not DSA.
- The birthday paradox concerns hash collisions, unrelated to DSA's signature security.
- Elliptic curve point multiplication underlies ECDSA specifically, not classic DSA over Z_p*.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Using the Extended Euclidean Algorithm, find the modular inverse d of e=7 mod φ(n)=40.

A) 13
B) 17
C) 33
D) 23

<details>
<summary>Answer</summary>

**Correct: D**

7 × 23 = 161 = 4×40 + 1, so 161 mod 40 = 1, satisfying e·d ≡ 1 (mod φ(n)).

**Why the others are wrong:**
- 7 × 13 = 91, 91 mod 40 = 11, not 1.
- 7 × 17 = 119, 119 mod 40 = 39, not 1.
- 7 × 33 = 231, 231 mod 40 = 31, not 1.

</details>

---

**Q6.** Which primality testing algorithm is preferred in practice because it can adjust its error probability arbitrarily low, unlike an older test that falsely reports Carmichael numbers as prime?

A) Fermat primality test
B) AKS primality test
C) Miller-Rabin primality test
D) Trial division

<details>
<summary>Answer</summary>

**Correct: C**

Miller-Rabin is a probabilistic test used widely (e.g., in OpenSSL) with a controllable, low error rate and avoids the Carmichael number pitfall.

**Why the others are wrong:**
- The Fermat primality test incorrectly reports Carmichael numbers (e.g., 561) as probably prime — a known exam trap.
- AKS is a deterministic polynomial-time test but is too slow for practical key generation at RSA-sized primes.
- Trial division is exhaustive and computationally infeasible for large cryptographic primes.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A company sends the same RSA-encrypted message (e=3, no padding) to three different recipients using different moduli. What attack becomes feasible?

A) Birthday attack
B) Discrete log attack
C) Hastad's broadcast attack
D) Extended Euclidean attack

<details>
<summary>Answer</summary>

**Correct: C**

With a small exponent like e=3 sent unpadded to 3+ recipients, an attacker can recover the plaintext using CRT — Hastad's broadcast attack.

**Why the others are wrong:**
- A birthday attack targets hash collisions, not RSA's small-exponent weakness.
- A discrete log attack applies to DH/DSA-style schemes, not RSA's factorization-based structure.
- 'Extended Euclidean attack' is not a recognized attack; the algorithm is a tool for computing modular inverses, not an exploit.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Approximately how many people must be in a room for there to be a greater than 50% probability that two share the same birthday (365-day year)?

A) 23
B) 183
C) 50
D) 365

<details>
<summary>Answer</summary>

**Correct: A**

The birthday paradox formula ~1.25×√n gives 1.25×√365 ≈ 23.9, so 23 people already exceed 50% probability.

**Why the others are wrong:**
- 183 (half of 365) reflects a naive but incorrect intuition about how the paradox scales.
- 50 people yields a much higher probability (~97%), far more than needed to just cross 50%.
- 365 guarantees a 100% match by the pigeonhole principle only with 366 people, not the answer to the 50% threshold question.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

