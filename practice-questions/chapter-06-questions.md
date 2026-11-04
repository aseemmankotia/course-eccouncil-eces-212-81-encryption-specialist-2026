## Chapter 6: RSA, Diffie-Hellman, DSA, ElGamal, and ECC — Practice Questions

**Q1.** A company needs to establish a shared secret key over an untrusted network but is concerned about a man-in-the-middle intercepting the exchange and impersonating both parties. Which approach BEST addresses this requirement?

A) Standard Diffie-Hellman key exchange using only the agreed prime and generator
B) Diffie-Hellman combined with digital certificates to authenticate both parties (e.g., DHE-RSA/DHE-DSS)
C) ElGamal encryption of the session key using a randomly generated key pair
D) Increasing the Diffie-Hellman prime modulus to 4096 bits

<details>
<summary>Answer</summary>

**Correct: B**

Diffie-Hellman provides no built-in identity authentication, so it must be paired with signed certificates (DHE-RSA, DHE-DSS, or ECDHE with certs) to bind the exchange to verified identities and prevent MITM.

**Why the others are wrong:**
- Plain DH has no authentication mechanism at all — this is the exact vulnerability described in the scenario.
- ElGamal encryption alone still requires the recipient's authenticated public key; without authentication it has the same MITM weakness.
- A larger modulus increases brute-force resistance but does nothing to authenticate the parties in the exchange.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An organization currently uses RSA-2048 for key exchange and wants to migrate to ECC while maintaining an equivalent security strength. Per NIST SP 800-57 guidance, which ECC key size should be selected?

A) ECC 160-bit
B) ECC 224-bit
C) ECC 256-bit
D) ECC 384-bit

<details>
<summary>Answer</summary>

**Correct: B**

RSA-2048 corresponds to roughly 112 bits of security, which matches ECC-224 in the NIST equivalence table.

**Why the others are wrong:**
- ECC-160 corresponds to RSA-1024 (80-bit security), a weaker level than RSA-2048.
- ECC-256 corresponds to RSA-3072 (128-bit security), stronger than required and not the direct equivalent.
- ECC-384 corresponds to RSA-7680 (192-bit security), far exceeding the RSA-2048 baseline.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A developer implements ElGamal encryption and notices the resulting ciphertext is exactly twice the size of the original plaintext message. Is this expected behavior?

A) No, ElGamal ciphertext should equal plaintext size like RSA
B) No, this indicates the ephemeral key was reused and must be regenerated
C) Yes, ElGamal always produces two ciphertext components (c1, c2), doubling the output size
D) Yes, but only when the message length exceeds the modulus size

<details>
<summary>Answer</summary>

**Correct: C**

ElGamal ciphertext consists of two components (c1 = g^k mod p, c2 = m·y^k mod p), inherently doubling the ciphertext size relative to plaintext — this is a well-known property tested on the exam.

**Why the others are wrong:**
- RSA ciphertext size equals the modulus size, not the plaintext size directly, and ElGamal is expected to expand output, unlike RSA.
- Ciphertext expansion is a structural property of the algorithm, not a symptom of key reuse (though key reuse is a separate serious flaw).
- The 2x expansion occurs for every ElGamal encryption regardless of message length relative to the modulus.

</details>

---

**Q4.** Which asymmetric algorithm listed below was designed by NIST specifically for digital signatures ONLY and cannot be used for encryption?

A) RSA
B) ElGamal
C) DSA
D) ECC (generic curve arithmetic)

<details>
<summary>Answer</summary>

**Correct: C**

DSA (Digital Signature Algorithm), defined in FIPS 186, was purpose-built for signing and verification only — it has no encryption/decryption function.

**Why the others are wrong:**
- RSA supports both encryption/decryption and signing/verification using the same key pair mechanics.
- ElGamal has both an encryption variant and a distinct signature variant, so it is not signature-only.
- ECC is a mathematical framework used to build both encryption (ECIES) and signature (ECDSA) schemes — it is not restricted to signatures.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A security architect needs a public-key encryption scheme that is provably secure against adaptive chosen-ciphertext attacks (IND-CCA2) without relying on the random oracle model. Which cryptosystem meets this requirement?

A) RSA-OAEP
B) ElGamal
C) Standard Diffie-Hellman
D) Cramer-Shoup

<details>
<summary>Answer</summary>

**Correct: D**

Cramer-Shoup was the first practical public-key cryptosystem proven IND-CCA2 secure under standard assumptions, without invoking the random oracle model.

**Why the others are wrong:**
- RSA-OAEP achieves CCA2 security but its security proof relies on the random oracle model.
- Basic ElGamal is only secure against chosen-plaintext attacks (IND-CPA), not chosen-ciphertext attacks.
- Diffie-Hellman is a key-exchange protocol, not an encryption scheme, and has no chosen-ciphertext security notion of its own.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** During RSA key generation, why is the public exponent e commonly set to 65537 (0x10001) rather than a very small value like 3?

A) 65537 is required by the RSA patent specification
B) 65537 produces a larger modulus n automatically
C) 65537 eliminates the need to compute a private exponent d
D) 65537 is prime, has only two 1-bits for fast modular exponentiation, and avoids known low-exponent attacks that affect very small e values

<details>
<summary>Answer</summary>

**Correct: D**

65537 is prime (ensuring it's coprime to φ(n) for virtually any p, q), and its binary form (2^16 + 1) allows fast exponentiation via repeated squaring, while avoiding vulnerabilities like Håstad's broadcast attack associated with e=3.

**Why the others are wrong:**
- There is no patent requirement dictating the exponent value; 65537 is a practical/security convention.
- The exponent choice has no bearing on the size of the modulus n, which is determined by the chosen primes p and q.
- d must always be computed as the modular inverse of e mod φ(n) regardless of which e is chosen.

</details>

---

**Q7.** In DSA, the same per-signature random value k is accidentally reused when signing two different messages with the same private key. What is the consequence?

A) No impact — DSA signatures remain secure regardless of k reuse
B) An attacker can algebraically recover the signer's private key from the two signatures
C) The signature verification will simply fail for both messages
D) The public key becomes invalid and must be regenerated

<details>
<summary>Answer</summary>

**Correct: B**

Reusing k in DSA (or ECDSA) across two signatures leaks enough information for an attacker to solve for k and then derive the private key x through simple modular arithmetic — a well-documented, exam-tested vulnerability.

**Why the others are wrong:**
- K reuse is a critical, well-known break of DSA security, not a non-issue.
- Both signatures will still verify correctly against the public key; the flaw is invisible to normal verification.
- The public key itself remains mathematically valid; it is the private key that becomes compromised, not the public key.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the fundamental difference between a True Random Number Generator (TRNG) and a Pseudo-Random Number Generator (PRNG)?

A) A TRNG derives randomness from physical/environmental entropy sources; a PRNG uses a deterministic algorithm seeded with an initial value
B) A TRNG uses a mathematical seed and algorithm; a PRNG uses physical entropy sources
C) TRNGs and PRNGs are functionally identical but differ only in output speed
D) A PRNG can never be used in cryptographic applications

<details>
<summary>Answer</summary>

**Correct: A**

TRNGs harvest entropy from unpredictable physical phenomena (thermal noise, radioactive decay, timing jitter), while PRNGs generate output through a deterministic algorithm from a seed — given the same seed, a PRNG always produces the same sequence.

**Why the others are wrong:**
- This reverses the definitions — TRNGs use physical entropy, PRNGs use algorithms and seeds.
- The core difference is the source of randomness (physical vs. algorithmic), not merely output speed.
- Cryptographically secure PRNGs (CSPRNGs) are widely and correctly used in cryptography when properly seeded with sufficient entropy.

</details>

---

