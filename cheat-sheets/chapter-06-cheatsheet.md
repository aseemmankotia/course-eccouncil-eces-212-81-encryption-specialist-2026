## Chapter 6 Cheat Sheet: RSA, DH, DSA, ElGamal, ECC

### RSA Key Generation
- Pick primes p, q → n = p×q, φ(n) = (p-1)(q-1)
- Choose e coprime to φ(n) — commonly **65537**
- Compute d = e⁻¹ mod φ(n)
- Public key: (n, e) | Private key: (n, d)
- Encrypt: c = m^e mod n | Decrypt: m = c^d mod n
- Sign: use d | Verify: use e
- Security basis: **integer factorization** of n

### RSA ↔ ECC Key Size Equivalence (NIST SP 800-57)
| Security Bits | RSA Key Size | ECC Key Size |
|---|---|---|
| 80 | 1024 | 160 |
| 112 | 2048 | 224 |
| 128 | 3072 | 256 |
| 192 | 7680 | 384 |
| 256 | 15360 | 521 |

**Exam note:** ECC gives equal security with far smaller keys → faster ops, less bandwidth.

### Diffie-Hellman
- Purpose: shared secret negotiation over insecure channel
- Math: g^ab mod p derived from exchanged g^a, g^b
- **No built-in authentication → MITM risk**
- Fix: pair with signed certs (DHE-RSA, DHE-DSS, ECDHE+cert)
- Security basis: discrete logarithm problem

### DSA (Digital Signature Algorithm)
- FIPS 186 standard — **signatures ONLY**, no encryption
- Uses per-signature random k — **must never be reused** (leaks private key)
- Signature = (r, s) pair; verification uses public key
- Key sizes: 1024/2048/3072-bit

### ElGamal
- Encryption AND separate signature variant exist
- Ciphertext = (c1, c2) → **always 2x plaintext size**
- Security basis: discrete log problem (like DH)
- CPA-secure only (not CCA2-secure) in basic form

### ECC (Elliptic Curve Cryptography)
- Domain parameters: **p, a, b, G, n, h**
- Security basis: Elliptic Curve Discrete Log Problem (ECDLP)
- Common curves: P-256 (secp256r1), P-384, P-521, Curve25519
- Used in ECDSA (signatures) and ECIES (encryption)

### Cramer-Shoup
- Public-key encryption, discrete-log based
- First scheme proven **IND-CCA2 secure without random oracle model**
- More computationally expensive than ElGamal — trade-off for stronger provable security

### RNG Types
| Type | Source | Example |
|---|---|---|
| TRNG | Physical entropy (thermal noise, decay) | Hardware RNG chip |
| PRNG | Deterministic algorithm + seed | Mersenne Twister |
| CSPRNG | Cryptographically secure algorithm + entropy seed | /dev/urandom, CTR_DRBG |

**Exam trap:** DH ≠ authenticated. DSA ≠ encryption capable. ElGamal ciphertext always doubles in size.
