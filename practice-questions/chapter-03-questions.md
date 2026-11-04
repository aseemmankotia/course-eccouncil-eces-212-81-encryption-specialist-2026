## Chapter 3: Cipher Modes, Key Scheduling, and Key Management — Practice Questions

**Q1.** A developer encrypts a bitmap image using AES in ECB mode. When the resulting ciphertext file is viewed as an image, the outline of the original picture is still visible. What is the root cause?

A) AES key size was too short for the image data
B) Identical plaintext blocks always produce identical ciphertext blocks under the same key
C) The IV was reused across multiple encryption operations
D) The image file header was not encrypted

<details>
<summary>Answer</summary>

**Correct: B**

ECB encrypts each block independently with no chaining or IV, so identical plaintext blocks (large flat-color regions in an image) always map to identical ciphertext blocks, preserving visual patterns — the classic 'ECB penguin' problem.

**Why the others are wrong:**
- Key size affects brute-force resistance, not pattern leakage; a longer key would show the same penguin
- ECB uses no IV at all, so IV reuse is not the mechanism here
- Header encryption is irrelevant to block-level pattern repetition in the pixel data

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A web application decrypts CBC-mode ciphertext and returns distinct error messages for 'invalid padding' versus 'valid padding, invalid MAC.' An attacker exploits this to decrypt traffic without the key. What attack is this?

A) Birthday attack
B) Meet-in-the-middle attack
C) Padding oracle attack
D) Related-key attack

<details>
<summary>Answer</summary>

**Correct: C**

Distinguishable padding error responses in CBC mode let an attacker send crafted ciphertext blocks and use the oracle's yes/no padding feedback to recover plaintext byte by byte (e.g., POODLE, Lucky13 class attacks).

**Why the others are wrong:**
- Birthday attacks target collision resistance of hash functions, not CBC padding validation
- Meet-in-the-middle targets multiple-encryption schemes like 2DES, not padding checks
- Related-key attacks exploit mathematical relationships between keys, not error message timing/content

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A logging system encrypts each log entry with AES-CTR mode, reusing the same key and the same initial counter value/nonce for every entry. What is the direct security consequence?

A) XORing two ciphertexts reveals the XOR of the two plaintexts, defeating confidentiality
B) The ciphertext becomes larger than the plaintext
C) The block cipher's key schedule is bypassed entirely
D) Padding oracle attacks become possible

<details>
<summary>Answer</summary>

**Correct: A**

CTR mode generates a keystream by encrypting the counter/nonce. Reusing the same nonce+key regenerates the identical keystream, so XORing two ciphertexts cancels the keystream and leaves the XOR of the plaintexts — the same catastrophic failure as one-time pad reuse.

**Why the others are wrong:**
- CTR is a stream-cipher-style mode; ciphertext length equals plaintext length regardless of nonce reuse
- The key schedule still runs normally to generate the keystream block
- CTR mode uses no padding, so padding oracle attacks do not apply

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** You need a block cipher mode of operation that supports random access to encrypted data (so you can decrypt block 500 without processing blocks 1-499) and allows parallel encryption/decryption. Which mode BEST fits?

A) CTR
B) CBC
C) CFB
D) OFB

<details>
<summary>Answer</summary>

**Correct: A**

CTR mode encrypts a counter value (nonce + block index) independently for each block, so any block's keystream can be computed directly without processing prior blocks — enabling both parallelism and random access.

**Why the others are wrong:**
- CBC requires the previous ciphertext block to decrypt/encrypt the current block, preventing random-access encryption
- CFB feeds ciphertext back into the cipher, creating a sequential dependency chain
- OFB pre-computes a keystream sequentially from the IV, so you must generate all prior keystream blocks first

</details>

---

**Q5.** A system must store user passwords for authentication. It needs to defend against both rainbow-table lookups and brute-force GPU cracking. Which combination of techniques should be applied?

A) Encrypt the password with AES-CBC using a static key
B) Hash the password once with SHA-256 and store the digest
C) Apply a unique per-user salt and a slow key-stretching function like bcrypt or PBKDF2
D) Apply a salt only, using a single fast hash iteration

<details>
<summary>Answer</summary>

**Correct: C**

Salting defeats precomputed rainbow tables by making each hash unique per user, while key stretching (multiple iterations in PBKDF2/bcrypt/scrypt/Argon2) deliberately slows down brute-force attempts even with GPU/ASIC acceleration.

**Why the others are wrong:**
- Encryption is reversible and the wrong primitive for password storage; a compromised key exposes all passwords in plaintext
- A single fast SHA-256 hash with no salt is trivially rainbow-tableable and fast to brute force
- Salting alone stops rainbow tables but does nothing to slow down per-guess brute force without stretching

</details>

---

**Q6.** Which requirement MUST be true of the Initialization Vector (IV) used in standard CBC mode encryption?

A) It must be kept secret from the recipient
B) It must be identical for every message encrypted with the same key
C) It must be derived mathematically from the encryption key
D) It must be unpredictable/random and not reused with the same key for a given context

<details>
<summary>Answer</summary>

**Correct: D**

The CBC IV does not need to be secret, but it must be unpredictable and unique per encryption under a given key; reusing it (or using a predictable one, as in BEAST) leaks information about plaintext relationships between messages.

**Why the others are wrong:**
- The IV is typically transmitted in the clear alongside the ciphertext — it needs unpredictability, not secrecy
- Reusing the same IV with the same key for multiple messages leaks whether the first blocks of plaintext are identical
- Deriving the IV from the key mathematically can reintroduce predictability, which the BEAST attack exploited

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** During AES key expansion, what is the primary purpose of the key scheduling algorithm?

A) It expands the original cipher key into a unique set of round keys used in each encryption round
B) It compresses the plaintext before encryption to improve performance
C) It generates the S-box substitution values dynamically per session
D) It selects which mode of operation (ECB, CBC, CTR) will be used

<details>
<summary>Answer</summary>

**Correct: A**

The key schedule takes the original secret key and derives a distinct round key for each round of the cipher (e.g., 11 round keys for AES-128), ensuring each round applies different key material even though only one master key exists.

**Why the others are wrong:**
- Plaintext compression is unrelated to key scheduling and is not part of AES
- AES S-boxes are fixed, pre-defined substitution tables based on finite field inversion — they are not regenerated per session
- Mode of operation is a separate architectural choice made independently of key expansion

</details>

---

**Q8.** How does Propagating Cipher Block Chaining (PCBC) differ from standard CBC mode?

A) PCBC eliminates the need for an IV entirely
B) PCBC XORs both the previous ciphertext block and the previous plaintext block into the current plaintext before encryption, so a single-bit error propagates through all subsequent blocks
C) PCBC only encrypts even-numbered blocks to speed up throughput
D) PCBC replaces the block cipher with a stream cipher internally

<details>
<summary>Answer</summary>

**Correct: B**

PCBC XORs each plaintext block with both the previous plaintext block and the previous ciphertext block before encrypting, unlike CBC which only XORs with the previous ciphertext. This means a transmission error in PCBC corrupts all following blocks (used historically in Kerberos v4), whereas CBC self-recovers after two blocks.

**Why the others are wrong:**
- PCBC still requires an IV just like CBC for the first block
- PCBC processes every block sequentially, not just even-numbered ones
- PCBC is still a block-cipher chaining mode, not a stream cipher construction

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

