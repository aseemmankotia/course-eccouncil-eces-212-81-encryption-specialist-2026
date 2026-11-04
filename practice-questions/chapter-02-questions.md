## Chapter 2: Block and Stream Ciphers: DES to AES — Practice Questions

**Q1.** A financial institution must maintain backward compatibility with existing 3DES infrastructure but wants the maximum security 3DES can provide. Which key configuration should they deploy?

A) 2-key 3DES (K1, K2, K1) providing ~80-bit effective strength
B) Single DES encryption with K1 only (56-bit strength)
C) 3DES with K1 = K2 = K3 (equivalent to single DES)
D) 3-key 3DES (K1, K2, K3) providing 112-bit effective strength

<details>
<summary>Answer</summary>

**Correct: D**

3-key 3DES (encrypt-decrypt-encrypt with three independent keys) is the strongest 3DES variant, giving 168 raw key bits but 112 bits of effective security due to meet-in-the-middle attacks.

**Why the others are wrong:**
- 2-key 3DES reduces effective strength to ~80 bits, well below 3-key's 112 bits
- Single DES is far weaker and not a form of 3DES compatibility
- Setting all three keys equal degrades 3DES to single DES strength (56 bits)

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A network engineer must encrypt a continuous, unpredictable-length audio stream in real time with minimal latency and no padding overhead. Which cipher type is architecturally BEST suited?

A) Block cipher operating in CBC mode
B) Block cipher operating in ECB mode
C) Stream cipher
D) Cryptographic hash function

<details>
<summary>Answer</summary>

**Correct: C**

Stream ciphers encrypt data bit-by-bit or byte-by-byte with no fixed block size, making them ideal for continuous, low-latency data such as voice or video streams.

**Why the others are wrong:**
- CBC requires padding to full blocks and introduces chaining latency unsuitable for real-time streams
- ECB also requires block padding and additionally leaks patterns, making it a worse choice
- Hash functions are one-way and provide no confidentiality/encryption at all

</details>

---

**Q3.** Which algorithm, originally submitted as Rijndael, was selected by NIST as the Advanced Encryption Standard to replace DES?

A) Rijndael
B) Twofish
C) Serpent
D) Blowfish

<details>
<summary>Answer</summary>

**Correct: A**

Rijndael, designed by Joan Daemen and Vincent Rijmen, won the AES competition in 2001 and was standardized as AES.

**Why the others are wrong:**
- Twofish was an AES finalist but was not selected
- Serpent was also an AES finalist, ranked highly for security but not chosen due to slower performance
- Blowfish predates the AES competition and was never a formal submission

</details>

---

**Q4.** An organization requires a NIST-approved, FIPS 140-2 compliant symmetric algorithm with a 256-bit key to protect top secret data. Which choice meets this requirement?

A) Blowfish-256
B) RC4-256
C) AES-256
D) TEA-256

<details>
<summary>Answer</summary>

**Correct: C**

AES-256 is the NIST-standardized, FIPS 140-2 validated algorithm approved for encrypting classified data up to Top Secret.

**Why the others are wrong:**
- Blowfish is not a NIST/FIPS-approved standard for classified data
- RC4 is a deprecated stream cipher with known keystream biases, never FIPS-approved for this use
- TEA is not a standardized or FIPS-approved algorithm and has known cryptographic weaknesses

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** How many rounds does AES-192 use?

A) 10
B) 12
C) 14
D) 16

<details>
<summary>Answer</summary>

**Correct: B**

AES round counts scale with key size: 128-bit key = 10 rounds, 192-bit key = 12 rounds, 256-bit key = 14 rounds.

**Why the others are wrong:**
- 10 rounds corresponds to AES-128, not AES-192
- 14 rounds corresponds to AES-256
- 16 rounds is not used by any standard AES key size

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** DES uses a 64-bit key field, but due to parity bits, its effective cryptographic key strength is:

A) 64 bits
B) 48 bits
C) 40 bits
D) 56 bits

<details>
<summary>Answer</summary>

**Correct: D**

8 of the 64 key bits are used for parity checking, leaving only 56 bits of actual key entropy, which is why DES is considered breakable via brute force today.

**Why the others are wrong:**
- 64 bits ignores the 8 parity bits that add no security
- 48 bits is not the effective key size (it's related to per-round subkey length, not the full key)
- 40 bits was historically the export-grade restriction on some ciphers, not DES's native strength

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the primary cryptographic weakness of RC4 that led to its deprecation in TLS?

A) Statistical biases in its keystream output allow plaintext recovery
B) Its small block size causes frequent collisions
C) It only supports 40-bit keys by design
D) It relies on a 56-bit DES-style Feistel structure

<details>
<summary>Answer</summary>

**Correct: A**

RC4's pseudo-random keystream has measurable statistical biases (especially in early output bytes), enabling attacks like those used against WEP and TLS, leading to its formal deprecation (RFC 7465).

**Why the others are wrong:**
- RC4 is a stream cipher and has no block size at all
- RC4 supports variable key lengths (typically 40-2048 bits); 40-bit was only a common weak configuration, not an inherent design limit
- RC4 is not Feistel-based; it uses a key scheduling algorithm (KSA) and pseudo-random generation algorithm (PRGA)

</details>

---

**Q8.** A security architect designing for a resource-constrained IoT sensor network needs a lightweight cipher using only simple XOR, addition, and shift operations for maximum speed on minimal hardware, accepting known related-key attack risks. Which cipher fits this description?

A) Twofish
B) Serpent
C) IDEA
D) TEA (Tiny Encryption Algorithm)

<details>
<summary>Answer</summary>

**Correct: D**

TEA was specifically designed for simplicity and speed using only XOR, ADD, and shift operations over 64 rounds (32 cycles), making it very lightweight, though it is known to be vulnerable to related-key and equivalent-key attacks.

**Why the others are wrong:**
- Twofish is a more complex Feistel-based AES finalist, not designed for minimal-operation lightweight use
- Serpent uses 32 rounds of substitution-permutation and is intentionally conservative/slower, not lightweight
- IDEA uses modular multiplication in addition to XOR/addition, making it heavier computationally than TEA

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

