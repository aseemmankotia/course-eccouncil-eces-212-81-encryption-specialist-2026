# Answer Key — Practice Test 1

**Q1. Correct: D**

A fixed shift of every letter by the same amount (here shift of 3) is the defining feature of the Caesar cipher. Shifting K->H, H->E, O->L, O->L, R->O gives 'HELLO', and Z->W, R->O, U->R, O->L, D->D gives 'WORLD', so the plaintext is 'HELLO WORLD'.

---

**Q2. Correct: B**

The Vigenere cipher uses a repeating keyword to select a different Caesar shift for each letter position, making it polyalphabetic and specifically designed to defeat simple frequency analysis that breaks monoalphabetic ciphers.

---

**Q3. Correct: B**

Playfair uses a 5x5 = 25 cell grid, but the English alphabet has 26 letters, so the classical convention is to merge I and J into one cell (sometimes Q is dropped instead), then fill remaining cells with unused alphabet letters in order after placing the keyword.

---

**Q4. Correct: B**

Non-repudiation is the goal that ensures a party cannot deny having performed an action, such as sending a signed message; digital signatures are the classic mechanism used to achieve this.

---

**Q5. Correct: D**

The reflector routes the electrical signal back through the rotors after passing through them once, and its wiring design mathematically guarantees a letter can never be encrypted to itself, a structural flaw that Allied codebreakers at Bletchley Park exploited to eliminate impossible key settings.

---

**Q6. Correct: C**

CTR mode encrypts a counter value (combined with a nonce) to produce keystream blocks independently of plaintext or ciphertext chaining, so any block can be encrypted or decrypted by computing E(k, nonce||counter) directly, giving true random access and parallelism with no padding needed.

---

**Q7. Correct: C**

CMAC builds a secure MAC entirely from a block cipher (like AES) using CBC-style chaining with derived subkeys, so it reuses the already-validated AES-128 code path without requiring any hash function library.

---

**Q8. Correct: D**

NIST SP 800-132 and general cryptographic best practice recommend a minimum salt length of 128 bits (16 bytes) of randomness, which makes precomputed rainbow tables and multi-target attacks computationally infeasible.

---

**Q9. Correct: C**

This is the fundamental architectural distinction tested on the exam: stream ciphers (e.g., RC4) generate a continuous keystream XORed with plaintext bit-by-bit or byte-by-byte, while block ciphers (e.g., AES, DES, Blowfish) operate on fixed-size blocks (e.g., 128 bits for AES) using rounds of substitution and permutation.

---

**Q10. Correct: A**

3DES reuses the standard DES algorithm three times with either two or three independent keys in an EDE sequence, raising effective security to roughly 112 bits (two-key) or up to 168 bits nominal (three-key), directly addressing the brute-force weakness while remaining backward-compatible with DES hardware.

---

**Q11. Correct: D**

SHA-256 belongs to the SHA-2 family, produces a 256-bit digest, and as of 2026 has no known practical collision or preimage attacks, making it a standard replacement for SHA-1 in code-signing and certificate applications.

---

**Q12. Correct: B**

CTR mode encrypts a counter value (combined with a nonce) independently for each block and XORs it with plaintext/ciphertext, so any block can be encrypted or decrypted independently and in parallel, and any block can be accessed randomly by computing the counter value directly.

---

**Q13. Correct: D**

CFB feeds the actual ciphertext back into the cipher as input for generating the next keystream block. Because the feedback is based on ciphertext (not an internal state independent of it), the mode automatically resynchronizes a few blocks after a bit is lost or corrupted.

---

**Q14. Correct: C**

This nested double-hash structure with an inner pad (ipad) and outer pad (opad) is the exact HMAC construction defined in RFC 2104. The standard values are ipad = 0x36 and opad = 0x5C, each byte repeated to fill the hash function's internal block size (64 bytes for SHA-256).

---

**Q15. Correct: D**

Blowfish's key schedule initializes its 18-entry P-array and four 256-entry S-boxes with the hexadecimal digits of pi, then repeatedly XORs the key material and re-encrypts to derive the final subkeys. Blowfish operates on a fixed 64-bit block size, with a variable key length from 32 to 448 bits.

---

**Q16. Correct: A**

PBKDF2 (a key-stretching/key-derivation function) repeatedly applies a pseudorandom function with a configurable, high iteration count, deliberately increasing the computational cost of each guess. Combined with the existing per-user salt, this defeats both rainbow tables and GPU brute-force speed, and the work factor can be tuned upward as hardware improves.

---

**Q17. Correct: B**

Ephemeral Diffie-Hellman (DHE/ECDHE) generates a fresh key pair per session, so recovering the server's static private key later provides no way to derive past session keys — this is the definition of perfect forward secrecy (PFS).

---

**Q18. Correct: C**

65537 (2^16 + 1) is the de facto standard RSA public exponent — it is prime, has a small Hamming weight for fast modular exponentiation, and is large enough to resist known low-exponent attacks like Hastad's broadcast attack.

---

**Q19. Correct: B**

For n = p*q with distinct primes, φ(n) = (p-1)(q-1) = (7-1)(11-1) = 6 * 10 = 60.

---

**Q20. Correct: B**

The birthday paradox shows that collisions in an n-bit output space are found with roughly 2^(n/2) attempts rather than 2^n, which is why hash digests need double the bit-length of the desired collision-resistance security level (e.g., SHA-256 gives ~128-bit collision resistance).

---

**Q21. Correct: B**

ElGamal encryption relies on the discrete logarithm problem, uses a random ephemeral value k for each encryption to produce a ciphertext pair (c1, c2), giving probabilistic (semantically secure) encryption with ciphertext expansion of roughly 2x.

---

**Q22. Correct: C**

According to NIST key-size equivalence guidance, RSA-3072 corresponds to a 128-bit security level, which matches ECC-256 — providing comparable security with far smaller keys and faster operations.

---

**Q23. Correct: A**

NIST key-strength equivalence tables show a 256-bit ECC key provides security roughly equivalent to a 3072-bit RSA key, while requiring far less computation and a much smaller key size — ideal for constrained devices.

---

**Q24. Correct: A**

DSA (Digital Signature Algorithm), standardized in FIPS 186, is designed exclusively for digital signatures and its security is based on the discrete logarithm problem in a finite field — it has no defined encryption mode.

---

**Q25. Correct: A**

φ(n) = (p-1)(q-1) = (13-1)(17-1) = 12 × 16 = 192.

---

**Q26. Correct: A**

The birthday paradox shows that finding a collision in an n-bit hash function requires only about 2^(n/2) attempts on average (e.g., ~2^64 for a 128-bit hash), far fewer than the 2^n needed for a brute-force preimage attack, meaning collision resistance is effectively halved in bit-strength.

---

**Q27. Correct: B**

A digital signature uses the signer's unique private key over a hash of the document, providing both integrity (hash) and non-repudiation (only the signer holds the private key).

---

**Q28. Correct: B**

After initial authentication with the AS, the client receives a TGT, which it then presents to the TGS to request service tickets for specific resources.

---

**Q29. Correct: D**

The Basic Constraints extension explicitly flags whether a certificate is a CA (CA:TRUE/FALSE) and can define a path length constraint.

---

**Q30. Correct: C**

SAE replaces the vulnerable 4-way handshake with a Diffie-Hellman-based exchange that resists offline dictionary and brute-force attacks and provides forward secrecy.

---

**Q31. Correct: C**

Tunnel mode encapsulates and encrypts the entire original IP packet within a new IP header, the standard configuration for gateway-to-gateway site-to-site VPNs.

---

**Q32. Correct: C**

Steganography conceals the presence of a hidden message within a carrier, whereas encryption transforms a visible message into unreadable ciphertext without hiding that a message exists.

---

**Q33. Correct: A**

Kerberos uses a KDC that issues a TGT after initial authentication; that TGT is then presented to request service tickets for other resources without re-authenticating, providing true SSO backed by symmetric-key tickets and mutual authentication.

---

**Q34. Correct: A**

SAE, also called the Dragonfly handshake, replaces the WPA2 four-way handshake in WPA3-Personal, providing forward secrecy and resistance to offline dictionary and brute-force attacks against the captured handshake.

---

**Q35. Correct: D**

Tunnel mode encrypts the entire original IP packet, including the header, and encapsulates it inside a new IP packet with a new header — the standard configuration for gateway-to-gateway (site-to-site) VPNs.

---

**Q36. Correct: A**

BitLocker seals the Volume Master Key to TPM Platform Configuration Register (PCR) measurements, releasing the key only when the measured boot components (firmware, bootloader, etc.) match the expected trusted values, protecting against tampering and offline attacks.

---

**Q37. Correct: D**

OCSP lets a client query a responder for the real-time revocation status of a single certificate by serial number, avoiding the overhead of downloading and parsing an entire CRL.

---

**Q38. Correct: A**

Kasiski examination finds repeated substrings in the ciphertext, measures the distances between their occurrences, and finds the GCD of those distances — the GCD (or a factor of it) reveals the probable key length for a polyalphabetic cipher like Vigenère.

---

**Q39. Correct: C**

A unique salt per user forces the attacker to build a separate rainbow table (or brute-force chain) for each salt value, which defeats the entire purpose of a precomputed table and makes the attack computationally infeasible at scale — this is the exam's key gotcha regarding salting.

---

**Q40. Correct: A**

Differential cryptanalysis, introduced by Biham and Shamir, uses chosen plaintext pairs with a fixed input XOR difference and tracks the probability of resulting output differences through the cipher's S-boxes and rounds to deduce key material.

---

**Q41. Correct: B**

A timing attack is a side-channel attack that exploits measurable variations in the time an algorithm takes to execute, which can leak information about secret key bits — a classic real-world attack against naive RSA implementations without constant-time exponentiation.

---

**Q42. Correct: C**

Because each plaintext letter always maps to the same ciphertext letter in a monoalphabetic substitution, the statistical frequency distribution of English letters (e.g., 'E' being most common) is preserved in the ciphertext, making frequency analysis highly effective at recovering the substitution mapping.

---

**Q43. Correct: A**

ML-KEM (standardized as FIPS 203, based on Kyber) is built on the Module Learning With Errors lattice problem, which has no known efficient quantum algorithm attack, making it resistant to Shor's algorithm.

---

**Q44. Correct: D**

ML-DSA (standardized as FIPS 204, based on CRYSTALS-Dilithium) is the NIST-selected primary lattice-based digital signature algorithm intended for general-purpose use in post-quantum migrations.

---

**Q45. Correct: D**

Grover's algorithm gives a quadratic speedup (roughly the square root of the search space) for unstructured search, which applies to brute-forcing symmetric keys. This effectively halves the security strength, so AES-128 offers only about 64 bits of quantum-adjusted security, motivating the use of AES-256.

---

**Q46. Correct: B**

QKD protocols such as BB84 encode key bits on the quantum states of photons; the no-cloning theorem and the disturbance caused by measurement mean any eavesdropping attempt introduces detectable errors, allowing the communicating parties to identify interception.

---

