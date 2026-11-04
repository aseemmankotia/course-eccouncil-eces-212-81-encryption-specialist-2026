## Chapter 4: Hash Functions, MAC, and HMAC — Practice Questions

**Q1.** A security engineer discovers that a legacy application stores user password hashes using unsalted MD5. Which attack is MOST likely to succeed easily against this stored data?

A) Man-in-the-middle attack on the login form
B) Padding oracle attack on the database
C) Birthday attack against the TLS handshake
D) Rainbow table lookup against the stored hashes

<details>
<summary>Answer</summary>

**Correct: D**

Unsalted hashes are identical for identical passwords, making precomputed rainbow tables highly effective and fast to look up.

**Why the others are wrong:**
- MITM targets the transmission channel, not data already at rest in a database
- Padding oracle attacks target CBC-mode block ciphers, not hash storage
- A birthday attack targets hash collisions, not password recovery, and has no relation to TLS handshakes

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** During a code review, an auditor finds that two different input files produce the identical MD5 digest. Which cryptographic property has been violated?

A) Collision resistance
B) Preimage resistance
C) Second preimage resistance
D) Avalanche effect

<details>
<summary>Answer</summary>

**Correct: A**

Collision resistance means it should be infeasible to find ANY two distinct inputs that hash to the same output; finding two arbitrary colliding files breaks exactly this property.

**Why the others are wrong:**
- Preimage resistance concerns recovering an input from a given hash output, not two matching inputs
- Second preimage resistance requires a specific target input to be matched, not two arbitrary files colliding
- Avalanche effect describes output change magnitude from small input changes; it is a design goal, not the property being broken here

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A developer must guarantee both message integrity and authenticity between two parties sharing a secret key, while specifically avoiding length-extension attack vulnerabilities. Which construction should be used?

A) Plain SHA-256 hash of the message
B) HMAC-SHA256
C) MD5(key || message)
D) CRC32 checksum of the message

<details>
<summary>Answer</summary>

**Correct: B**

HMAC's nested double-hash construction with ipad/opad specifically defeats length-extension attacks that affect Merkle–Damgård hashes.

**Why the others are wrong:**
- A plain hash provides no keying, so it offers no authenticity and can be tampered with freely
- Concatenating key and message (H(key||message)) is the naive MAC construction vulnerable to length-extension attacks
- CRC32 is a non-cryptographic checksum, easily forged and offers no security guarantee

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An organization needs a password hashing scheme intentionally designed to be memory-hard, resisting large-scale parallel cracking using GPUs and ASICs. Which of the following BEST meets this requirement?

A) scrypt
B) PBKDF2
C) bcrypt
D) Salted SHA-256

<details>
<summary>Answer</summary>

**Correct: A**

scrypt was explicitly designed as a memory-hard KDF, requiring large amounts of RAM per computation to neutralize the parallelization advantage of GPUs and ASICs.

**Why the others are wrong:**
- PBKDF2 is CPU/iteration-hard only; it has no memory-hardness and remains parallelizable on GPUs
- bcrypt improves on PBKDF2 with a Blowfish-based schedule but is not designed with the same aggressive memory-hardness as scrypt
- Salted SHA-256 is fast by design and easily brute-forced at scale, offering no key stretching at all

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which hash function produces a 512-bit digest using an internal structure derived from the AES cipher design?

A) Whirlpool
B) BLAKE2b
C) SHA-512
D) RIPEMD-160

<details>
<summary>Answer</summary>

**Correct: A**

Whirlpool produces a 512-bit output and its internal compression function is built on a design closely related to AES (Rijndael).

**Why the others are wrong:**
- BLAKE2b can output 512 bits but uses a ChaCha-derived design, not AES
- SHA-512 outputs 512 bits but uses a Merkle–Damgård construction, unrelated to AES
- RIPEMD-160 only produces a 160-bit digest, not 512 bits

</details>

---

**Q6.** As of current OWASP guidance, what is the recommended minimum iteration count when using PBKDF2-HMAC-SHA256 for password storage?

A) 100
B) 600,000
C) 1,000
D) 4

<details>
<summary>Answer</summary>

**Correct: B**

OWASP's Password Storage Cheat Sheet recommends at least 600,000 iterations for PBKDF2-HMAC-SHA256 to sufficiently slow down brute-force attempts.

**Why the others are wrong:**
- 100 iterations provides essentially no meaningful protection against modern hardware
- 1,000 iterations was an old recommendation from over a decade ago and is now considered far too weak
- 4 iterations offers no cryptographic value whatsoever

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In the HMAC construction as defined in RFC 2104, what are the two fixed padding constants XORed with the key before hashing?

A) 0x00 and 0xFF
B) 0x0F and 0xF0
C) 0x36 (ipad) and 0x5C (opad)
D) 0xAA and 0x55

<details>
<summary>Answer</summary>

**Correct: C**

RFC 2104 defines ipad as the byte 0x36 and opad as the byte 0x5C, each repeated to the block size of the hash function.

**Why the others are wrong:**
- 0x00/0xFF are not the defined HMAC constants
- 0x0F/0xF0 are not the defined HMAC constants
- 0xAA/0x55 are not the defined HMAC constants

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the PRIMARY difference between a generic keyed MAC and HMAC?

A) A MAC uses asymmetric keys while HMAC uses symmetric keys
B) A MAC always produces a longer output than HMAC
C) HMAC does not require a secret key at all
D) HMAC is a specific keyed-hash construction designed to mitigate weaknesses present in naive keyed-hashing MAC constructions

<details>
<summary>Answer</summary>

**Correct: D**

HMAC is a standardized, provably secure keyed-hash construction created specifically to address the length-extension and other weaknesses of naive keyed-hash MAC designs.

**Why the others are wrong:**
- Both MAC and HMAC use symmetric secret keys, not asymmetric ones
- Output length depends on the underlying hash function chosen, not on whether it is a generic MAC or HMAC
- HMAC absolutely requires a secret key, just like any MAC

</details>

---

