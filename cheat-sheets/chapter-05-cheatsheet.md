# Number Theory Foundations — Cheat Sheet

## Euler's Totient Function
| Case | Formula |
|---|---|
| n = p (prime) | φ(n) = p - 1 |
| n = p×q (distinct primes) | φ(n) = (p-1)(q-1) |

**RSA worked example:** p=61, q=53 → n=3233, φ(n) = 60×52 = **3120**.
Exam trap: n and φ(n) are NOT the same value.

## RSA Key Generation Steps
1. Pick primes p, q → n = p×q
2. Compute φ(n) = (p-1)(q-1)
3. Choose e where gcd(e, φ(n)) = 1 (commonly **e = 65537**)
4. Compute d = e⁻¹ mod φ(n) via **Extended Euclidean Algorithm**
5. Public key = (n, e); Private key = (n, d)

## Extended Euclidean Algorithm
Solves: e·d ≡ 1 (mod φ(n))
Example: e=7, φ(n)=40 → d=23 (7×23 = 161 = 4×40+1)

## Modular Exponentiation
- Method: square-and-multiply
- Complexity: O(log e) multiplications vs O(e) naive
- Used for both RSA encrypt/decrypt and Diffie-Hellman key computation

## Discrete Logarithm Problem (DLP)
| Scheme | Hard Problem |
|---|---|
| RSA | Integer factorization |
| Diffie-Hellman | Discrete log mod p (Z_p*) |
| DSA | Discrete log mod p |
| ECDSA / ECDH | Discrete log over elliptic curve points |

Exam trap: RSA ≠ discrete log based. Don't mix up factorization vs DLP schemes.

## Birthday Problem
- Approximate items needed for 50% collision: **1.25 × √n**
- Classic case: 365 days → **~23 people** for >50% shared-birthday probability

## Birthday Attack vs Hash Size
| Hash Output | Birthday Bound (collision) |
|---|---|
| 128-bit (MD5) | ~2^64 |
| 160-bit (SHA-1) | ~2^80 |
| 256-bit (SHA-256) | ~2^128 |

Rule: birthday bound ≈ 2^(n/2) for an n-bit hash.

## Primality Testing
| Test | Type | Weakness/Note |
|---|---|---|
| Trial Division | Deterministic | Infeasible for large primes |
| Fermat Test | Probabilistic | Fails on Carmichael numbers (e.g., 561) |
| Miller-Rabin | Probabilistic | Industry standard, adjustable low error rate |
| AKS | Deterministic, polynomial-time | Correct but too slow for practical key gen |

## Key Numbers to Memorize
- Common RSA e: **65537**
- Birthday paradox 50% threshold (365 days): **23 people**
- Birthday attack strength = **half** the hash bit length
