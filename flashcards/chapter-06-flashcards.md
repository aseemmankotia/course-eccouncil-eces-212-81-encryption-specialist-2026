## Chapter 6: RSA, Diffie-Hellman, DSA, ElGamal, and ECC — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | RSA-2048 security strength equivalent in ECC bits? | 224-bit ECC. Exam tip: RSA1024≈ECC160(80-bit), RSA2048≈ECC224(112-bit), RSA3072≈ECC256(128-bit), RSA7680≈ECC384(192-bit), RSA15360≈ECC521(256-bit). |
| 2 | What is the primary weakness of standard Diffie-Hellman key exchange? | No built-in authentication of the parties — vulnerable to man-in-the-middle attacks unless combined with certificates/signatures (DHE-RSA, DHE-DSS, ECDHE-cert). |
| 3 | ECC vs RSA: primary architectural advantage of ECC? | Equivalent security with much smaller key sizes (e.g., ECC-256 ≈ RSA-3072), reducing computation, bandwidth, and storage overhead. |
| 4 | ElGamal ciphertext size relative to plaintext? | Always 2x plaintext size — output consists of two components (c1, c2). This expansion is a defining structural property. |
| 5 | DSA use case restriction | DSA (FIPS 186) can ONLY be used for digital signatures — it has no encryption/decryption capability, unlike RSA or ElGamal. |
| 6 | RSA key generation formula for private exponent d? | d = e^-1 mod φ(n), where φ(n) = (p-1)(q-1) and n = p × q. Public key = (n, e); private key = (n, d). |
| 7 | Common RSA public exponent value and why? | 65537 (0x10001) — prime, has only 2 one-bits for fast exponentiation, avoids low-exponent attacks (e.g., issues with e=3). |
| 8 | Six ECC domain parameters tested on exam? | p (prime modulus), a and b (curve coefficients), G (base/generator point), n (order of G), h (cofactor). |
| 9 | Cramer-Shoup cryptosystem's key security property? | First practical public-key scheme proven IND-CCA2 secure (resistant to adaptive chosen-ciphertext attacks) WITHOUT relying on the random oracle model. |
| 10 | DSA signature security flaw if per-message k is reused? | Attacker can solve for k algebraically across two signatures and derive the signer's private key — catastrophic nonce-reuse vulnerability (also applies to ECDSA). |
| 11 | TRNG vs PRNG — key distinction | TRNG: entropy from physical sources (thermal noise, radioactive decay). PRNG: deterministic algorithm from a seed — same seed always produces same output sequence. |
| 12 | Which asymmetric algorithms rely on the discrete logarithm problem? | Diffie-Hellman, DSA, ElGamal, and ECC (via the elliptic curve discrete logarithm problem, ECDLP) — RSA instead relies on integer factorization. |
