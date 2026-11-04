# Answer Key — Practice Test 2

**Q1. Correct: C**

Kasiski examination looks for repeated ciphertext sequences, measures the distance between them, and takes the GCD of those distances to estimate the Vigenere key length, which is exactly the scenario described.

---

**Q2. Correct: A**

ADFGVX extended the earlier ADFGX cipher by adding digits, requiring a 6x6 grid (36 characters), and it combines fractionation with a columnar transposition step, matching the described process exactly.

---

**Q3. Correct: C**

The reflector (Umkehrwalze) is wired so that no contact connects to itself, forcing the electrical signal to always return on a different path than it entered, which is the structural reason a letter could never encrypt to itself - a flaw later exploited by Allied cryptanalysts.

---

**Q4. Correct: D**

Non-repudiation is the specific goal that provides proof of origin and prevents the originator from denying they sent or signed the message, which is distinct from simply verifying identity (authentication).

---

**Q5. Correct: B**

Playfair rules require that identical letters falling in the same digraph be separated by inserting a filler letter (traditionally X, sometimes Q), turning 'LL' into pairs like 'LX' and 'LO', which is the standard classical handling technique.

---

**Q6. Correct: D**

In CTR mode, the keystream block for position i is E(nonce || counter=i), computed entirely independently of every other block. A client can jump straight to segment 1000 and generate the correct keystream with no data from any other segment, giving true random access.

---

**Q7. Correct: D**

DES has exactly 4 weak keys — those where the two 28-bit C and D halves are all zeros, all ones, or one half all zeros and the other all ones — causing every round to produce the same subkey, so E(k)=D(k).

---

**Q8. Correct: A**

The Rijndael S-box first computes the multiplicative inverse of each byte in GF(2^8) (with 0 mapped to itself), then applies a fixed affine transformation over GF(2). The inverse function gives strong nonlinearity, and the affine transform prevents the S-box from having a simple algebraic description, together giving high resistance to differential and linear attacks.

---

**Q9. Correct: C**

PBKDF2 (Password-Based Key Derivation Function 2) is explicitly designed for key stretching: it repeatedly applies an underlying PRF (typically HMAC) with a salt over many iterations, deliberately increasing computational cost to slow down offline brute-force and dictionary attacks.

---

**Q10. Correct: B**

OWASP's Password Storage Cheat Sheet recommends a minimum of 600,000 iterations for PBKDF2-HMAC-SHA256 to keep offline cracking sufficiently expensive given modern hardware.

---

**Q11. Correct: D**

The FMS attack exploits the fact that RC4's KSA generates certain 'weak' IV/key combinations where the first bytes of the keystream leak statistical information correlated with the key bytes. By capturing many frames using weak IVs and analyzing the first keystream byte, attackers could recover the static key.

---

**Q12. Correct: B**

CTR mode generates its keystream from an independent counter value plus nonce, so any block can be encrypted or decrypted independently and in any order (true random access), and a single-bit ciphertext error only flips the corresponding plaintext bit with no propagation.

---

**Q13. Correct: A**

AES's S-box is constructed by first taking the multiplicative inverse of a byte in the finite field GF(2^8) (with 0 mapped to itself), then applying a fixed affine (bit-matrix plus constant) transformation to add nonlinearity and resist algebraic attacks.

---

**Q14. Correct: D**

Blowfish initializes the P-array and S-boxes using the hexadecimal digits of pi (a nothing-up-my-sleeve number), then repeatedly XORs the key material into the P-array and re-encrypts a running all-zero block to derive the final subkey values.

---

**Q15. Correct: A**

HMAC is defined as H((K XOR opad) || H((K XOR ipad) || message)), where ipad is the byte 0x36 repeated to block size and opad is the byte 0x5C repeated to block size — these specific constants are defined in RFC 2104 and tested on the 212-81 exam.

---

**Q16. Correct: B**

Whirlpool's compression function is built on a substitution-permutation network closely modeled after the AES (Rijndael) cipher structure, and it produces a 512-bit (64-byte) hash digest — one of the largest standardized hash outputs tested on the exam.

---

**Q17. Correct: A**

φ(n) = (p-1)(q-1) = 12 × 16 = 192. This is the Euler's totient value required to derive a valid public/private exponent pair.

---

**Q18. Correct: B**

112 = 2^4 × 7. e=3 is odd and not a multiple of 7, so gcd(3,112)=1, making it a valid exponent that has a multiplicative inverse mod φ(n).

---

**Q19. Correct: B**

Diffie-Hellman security relies on the Discrete Logarithm Problem (DLP): given g, p, and g^a mod p, it is computationally infeasible to recover a for large safe primes p.

---

**Q20. Correct: B**

The birthday bound states that for an n-bit hash, roughly sqrt(2^n) = 2^(n/2) samples are needed for a 50% collision probability. For n=128, that is 2^64 computations.

---

**Q21. Correct: A**

NIST equivalence tables map 256-bit ECC keys to approximately 3072-bit RSA/DH keys, both offering roughly 128 bits of symmetric-equivalent security.

---

**Q22. Correct: D**

Cramer-Shoup extends ElGamal by adding extra group elements and a universal hash function to produce a verification tag, making the scheme provably secure against adaptive chosen-ciphertext attacks (IND-CCA2), unlike plain ElGamal which is only IND-CPA secure.

---

**Q23. Correct: C**

φ(n) = (p-1)(q-1) = 60*52 = 3120. Solving 17d ≡ 1 (mod 3120) via the extended Euclidean algorithm gives d = 2753, verified by 17*2753 = 46801 = 15*3120 + 1.

---

**Q24. Correct: D**

Cramer-Shoup was explicitly designed as an extension of ElGamal that adds a universal hash function and extra group elements to achieve IND-CCA2 security in the standard model, unlike plain ElGamal.

---

**Q25. Correct: C**

The birthday bound states that a 50% collision probability occurs after roughly sqrt(2^n) hashes, and sqrt(2^128) = 2^64.

---

**Q26. Correct: A**

NIST maps 256-bit ECC keys to approximately the 128-bit security level, which corresponds to a 3072-bit RSA key per SP 800-57's key equivalence table.

---

**Q27. Correct: C**

ESP (Encapsulating Security Payload) provides confidentiality and optional integrity for the payload, and because it does not authenticate the outer IP header, it works correctly with NAT (often combined with NAT-T using UDP encapsulation). AH authenticates the entire packet including the IP header, which breaks when NAT rewrites addresses.

---

**Q28. Correct: A**

The client presents the TGT plus a freshly generated authenticator (encrypted with the TGT session key) in the TGS-REQ, proving it possesses the session key without resending credentials, and the TGS then issues a service ticket.

---

**Q29. Correct: C**

SAE (based on the Dragonfly handshake) derives the Pairwise Master Key through an interactive exchange tied to the AP, so an attacker cannot capture a single exchange and brute-force it offline; each guess requires interacting with the live AP, which is rate-limitable.

---

**Q30. Correct: A**

The Basic Constraints extension explicitly marks a certificate as a CA certificate (CA=TRUE) and can restrict the certification path length via pathLenConstraint, which is what permits a certificate to sign subordinate CA certificates.

---

**Q31. Correct: D**

TLS 1.3 removed static RSA key exchange entirely and requires (EC)DHE for its standard handshake, ensuring that a compromised long-term private key cannot be used to decrypt previously captured sessions, i.e., forward secrecy.

---

**Q32. Correct: A**

VeraCrypt's hidden volume feature hides an encrypted volume inside the free space of an outer volume such that its existence cannot be proven, giving the user plausible deniability — a data-hiding concept closely related to steganography, where the goal is concealing the existence of data, not just its content.

---

**Q33. Correct: A**

ESP (protocol 50) is the only IPsec header that provides payload confidentiality via encryption; it also optionally provides integrity and authentication, making it the correct choice for a confidentiality requirement.

---

**Q34. Correct: B**

After the AS authenticates the user and issues a TGT (encrypted with the TGS's secret key), the client presents that TGT to the TGS along with an authenticator to request a service ticket for a specific resource — this is the core AS-REQ/AS-REP then TGS-REQ/TGS-REP flow.

---

**Q35. Correct: A**

WPA3-Personal replaces the WPA2 four-way handshake with SAE (Dragonfly key exchange), a password-authenticated key exchange that provides forward secrecy and resists offline dictionary attacks and the nonce-reuse/reinstallation flaws exploited by KRACK, because each session derives fresh unique session keys without the vulnerable handshake message replay pattern.

---

**Q36. Correct: C**

OCSP allows a client (or a proxy) to query a responder for the real-time revocation status of a single certificate, returning a small signed response quickly, avoiding the overhead of downloading and parsing an entire CRL file, and is designed for exactly this low-latency, high-volume scenario (often paired with OCSP stapling).

---

**Q37. Correct: D**

BitLocker relies on the TPM to store Platform Configuration Register (PCR) measurements taken during boot (firmware, boot loader, boot manager, etc.); the volume master key is sealed against expected PCR values, so if the boot chain is altered (e.g., tampered boot loader), the measurements change and the TPM refuses to release the key, forcing recovery-key entry — this ties both key sealing and tamper detection to the same TPM mechanism.

---

**Q38. Correct: C**

Kasiski examination estimates key length by finding the greatest common divisor of distances between repeated ciphertext segments, since such repeats occur when the same plaintext segment aligns with the same keystream offset. GCD(12,18,24) = 6, indicating a 6-character key.

---

**Q39. Correct: D**

Differential cryptanalysis is a chosen-plaintext attack that tracks how specific input XOR differences propagate through a cipher's rounds, exploiting the non-uniform distribution of output differences in S-boxes to deduce key bits.

---

**Q40. Correct: B**

A unique per-user salt forces an attacker to build a separate precomputed table for every possible salt value, making rainbow tables computationally infeasible; this is the standard defense against precomputation attacks.

---

**Q41. Correct: B**

Variations in execution time caused by data-dependent branching in modular exponentiation leak information about individual key bits; statistically correlating these timing differences is a classic timing side-channel attack, first demonstrated by Kocher against RSA implementations.

---

**Q42. Correct: B**

Integral cryptanalysis, also known as the Square attack, exploits sets (lambda-sets) of plaintexts where certain byte positions are held constant and others take all possible values, then examines whether the XOR sum of the ciphertexts is balanced (zero) to distinguish reduced-round versions of ciphers such as Square or AES.

---

**Q43. Correct: B**

Grover's algorithm gives a quadratic (not exponential) speedup for unstructured search, effectively reducing an n-bit symmetric key's brute-force strength to n/2 bits. AES-256 under Grover behaves like a ~128-bit key, which is still considered secure, so AES-256 does not need to be replaced -- only AES-128 becomes a concern.

---

**Q44. Correct: C**

ML-KEM (based on CRYSTALS-Kyber) is the NIST-standardized lattice-based Key Encapsulation Mechanism, purpose-built for establishing a shared secret over an insecure channel, analogous to the role Diffie-Hellman/RSA key exchange played classically.

---

**Q45. Correct: D**

Due to the no-cloning theorem, any interception and measurement by Eve disturbs the quantum states, introducing detectable errors. Alice and Bob estimate the quantum bit error rate (QBER) from the compared subset; a QBER above the expected channel-noise threshold reveals eavesdropping.

---

**Q46. Correct: C**

Shor's algorithm solves integer factorization and discrete logarithms in polynomial time, exponentially faster than the best classical algorithms, which is why it breaks RSA, Diffie-Hellman, and ECC entirely. Grover's algorithm only provides a quadratic speedup for unstructured search, which reduces the effective security of symmetric keys and hash preimage resistance by half the bit-length but does not break them outright.

---

