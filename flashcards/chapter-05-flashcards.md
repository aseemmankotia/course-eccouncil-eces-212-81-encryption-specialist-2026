## Chapter 5: Number Theory Foundations for Asymmetric Crypto — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Formula for Euler's totient function φ(n) when n = p×q (distinct primes)? | φ(n) = (p-1)(q-1). Exam tip: used to compute RSA private exponent d = e⁻¹ mod φ(n). |
| 2 | RSA example: p=61, q=53. What is φ(n)? | φ(n) = 60 × 52 = 3120. Exam tip: don't confuse φ(n) with n = p×q = 3233. |
| 3 | What algorithm computes the modular multiplicative inverse needed for RSA's private key d? | Extended Euclidean Algorithm — solves e·d ≡ 1 (mod φ(n)). Exam tip: memorize the back-substitution steps, not just the gcd computation. |
| 4 | Which two asymmetric schemes base security on the Discrete Logarithm Problem, not factorization? | Diffie-Hellman and DSA (also ElGamal). Exam tip: RSA = factorization; DH/DSA = discrete log — a favorite exam distractor pairing. |
| 5 | Approximate formula for the birthday paradox (n possible values)? | ~1.25×√n items needed for 50% collision chance. Exam tip: for a 365-day year, ≈23 people. |
| 6 | Birthday attack complexity against an n-bit hash function? | ~2^(n/2) operations for 50% collision probability. Exam tip: SHA-256 (256-bit) → 2^128; MD5 (128-bit) → 2^64. |
| 7 | Fermat primality test weakness the exam tests? | Fails on Carmichael numbers (e.g., 561) — reports composite as 'probably prime'. Exam tip: Miller-Rabin fixes this weakness. |
| 8 | Why must RSA public exponent e be coprime to φ(n)? | gcd(e, φ(n)) = 1 is required so a modular inverse d exists satisfying e·d ≡ 1 (mod φ(n)). Exam tip: most common e = 65537. |
| 9 | Most common RSA public exponent value used in practice? | 65537 (2^16 + 1). Exam tip: chosen for fast encryption (few 1-bits) and resistance to small-exponent attacks like e=3. |
| 10 | Efficient algorithm for computing a^b mod n with large exponents? | Modular exponentiation via square-and-multiply. Exam tip: runs in O(log b) multiplications instead of O(b). |
| 11 | What group's discrete log problem underlies classic Diffie-Hellman? | The multiplicative group of integers mod p (Z_p*). Exam tip: ECDH uses discrete log over elliptic curve points instead — same hard problem, different group. |
| 12 | Attack enabled by broadcasting the same message with RSA e=3, unpadded, to 3+ recipients? | Hastad's Broadcast Attack — recovers plaintext via CRT without factoring n. Exam tip: mitigated by OAEP padding or using a larger, random-looking e. |
