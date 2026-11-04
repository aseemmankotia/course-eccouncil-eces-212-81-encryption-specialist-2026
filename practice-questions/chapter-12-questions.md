## Chapter 12: Full 212-81 Exam Simulation and Time-Management Strategy — Practice Questions

**Q1.** A financial application must encrypt data at rest using a 256-bit block cipher key. The mode must prevent identical plaintext blocks from producing identical ciphertext AND must detect tampering without a separate MAC step. Which mode BEST meets these requirements?

A) GCM
B) ECB
C) CBC
D) CTR

<details>
<summary>Answer</summary>

**Correct: A**

GCM is an AEAD mode — it combines CTR-style encryption (no identical ciphertext for identical blocks, no padding) with a built-in authentication tag, satisfying both confidentiality and integrity in one pass.

**Why the others are wrong:**
- ECB always produces identical ciphertext for identical plaintext blocks — the classic 'penguin image' gotcha.
- CBC requires padding and needs a separate MAC for integrity; it does not authenticate on its own.
- CTR solves the identical-block problem but provides NO authentication — tampering goes undetected.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A user needs to prove a message came from a specific sender and that its content was not altered, without any pre-shared secret between the parties. Which technique should be used?

A) HMAC with a shared secret
B) AES-GCM with a pre-shared key
C) Digital signature using the sender's private key
D) Diffie-Hellman key exchange alone

<details>
<summary>Answer</summary>

**Correct: C**

A digital signature (sign with private key, verify with public key) provides both authenticity and integrity with no shared secret required.

**Why the others are wrong:**
- HMAC requires a pre-shared secret, which the scenario explicitly rules out.
- AES-GCM is symmetric and also requires a shared key in advance.
- Diffie-Hellman establishes a shared secret but by itself does not authenticate the sender's identity.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An organization needs a key exchange method over an untrusted network that provides perfect forward secrecy without relying on static pre-shared keys. Which should be selected?

A) Static RSA key transport
B) Kerberos ticket exchange
C) AES Key Wrap
D) ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)

<details>
<summary>Answer</summary>

**Correct: D**

ECDHE generates a new ephemeral key pair per session, so compromise of a long-term key does not expose past session keys — the definition of forward secrecy.

**Why the others are wrong:**
- Static RSA key transport reuses the same key pair, so compromising the private key exposes all past sessions — no forward secrecy.
- Kerberos relies on a trusted KDC and shared secrets, not a public-key forward-secret exchange.
- AES Key Wrap protects a key in transit but does not perform key agreement or provide forward secrecy.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A system must handle data classified as Top Secret per common government cryptographic guidance (CNSA/Suite B). Which AES key size is the minimum required?

A) 256-bit
B) 128-bit
C) 192-bit
D) 512-bit

<details>
<summary>Answer</summary>

**Correct: A**

CNSA/Suite B guidance mandates AES-256 for Top Secret data; AES-128 is only approved up to Secret classification.

**Why the others are wrong:**
- AES-128 is only sufficient for Secret-level data, not Top Secret.
- 192-bit is a valid AES key length but is not the classification threshold tested — 256-bit is the answer the exam expects.
- 512-bit is not a valid AES key size (AES only supports 128/192/256).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which of the following BEST describes a birthday attack in cryptography?

A) Exploiting IV reuse in a stream cipher
B) Brute-forcing a symmetric key by trying every possible value
C) Exploiting the pigeonhole-principle probability of hash collisions with fewer attempts than expected
D) Factoring an RSA modulus to recover the private key

<details>
<summary>Answer</summary>

**Correct: C**

A birthday attack exploits the birthday paradox: collisions in an n-bit hash occur with 50% probability after roughly 2^(n/2) attempts, far fewer than the full 2^n keyspace.

**Why the others are wrong:**
- IV reuse is a stream-cipher/CTR-mode weakness, unrelated to the birthday paradox.
- Brute force targets the full keyspace (2^n), not the reduced collision space (2^(n/2)).
- Factoring the modulus is an RSA-specific attack, not a hash collision technique.

</details>

---

**Q6.** An attacker intercepts RSA ciphertext and discovers that the same modulus N was used to encrypt the same plaintext under two different public exponents e1 and e2. Which attack applies to this scenario?

A) Common Modulus Attack
B) Man-in-the-middle attack
C) Birthday attack
D) Meet-in-the-middle attack

<details>
<summary>Answer</summary>

**Correct: A**

When the same message is encrypted under a shared modulus N with two coprime exponents, the plaintext can be recovered mathematically without factoring N — this is the Common Modulus Attack.

**Why the others are wrong:**
- Man-in-the-middle requires active interception/alteration of a key exchange, not shared-modulus reuse.
- Birthday attacks target hash collisions, not RSA modulus reuse.
- Meet-in-the-middle targets double encryption schemes (e.g., 2DES), not shared moduli.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A company wants email where only the intended recipient can decrypt the content and the sender's identity is cryptographically verifiable via signature, using a CA-based trust model. Which technology fits?

A) S/MIME using the recipient's public key for encryption and the sender's private key for signing
B) TLS with AES-GCM
C) HMAC-SHA256 with a shared password
D) Kerberos ticket exchange

<details>
<summary>Answer</summary>

**Correct: A**

S/MIME uses PKI/CA-issued certificates: the sender encrypts with the recipient's public key and signs with their own private key, satisfying both requirements.

**Why the others are wrong:**
- TLS secures a transport channel, not persistent email messages at rest.
- HMAC requires a pre-shared secret and provides no CA-based identity trust.
- Kerberos is for network authentication/ticketing, not email encryption.

</details>

---

**Q8.** What is the output size of SHA-256 compared to SHA3-256?

A) SHA-256 is 128-bit, SHA3-256 is 256-bit
B) Both are 256-bit
C) SHA-256 is 256-bit, SHA3-256 is 512-bit
D) Both are 160-bit

<details>
<summary>Answer</summary>

**Correct: B**

Despite different internal constructions (Merkle-Damgård vs. sponge/Keccak), SHA-256 and SHA3-256 both produce a 256-bit digest — the '256' in the name refers to output size, not internal structure.

**Why the others are wrong:**
- SHA-256 is not 128-bit; 128-bit is associated with older/weaker hashes like MD5.
- SHA3-256 is not 512-bit — that describes SHA-512 or SHA3-512, a common naming-confusion distractor.
- 160-bit describes SHA-1, not either SHA-2 or SHA-3 variant named '256'.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

