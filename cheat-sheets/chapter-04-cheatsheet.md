# Chapter 4 Cheat Sheet: Hash Functions, MAC & HMAC

## Hash Function Output Sizes & Status
| Algorithm | Output Size | Construction | Status |
|---|---|---|---|
| MD5 | 128-bit | Merkle–Damgård | Broken (collisions since 2004) |
| SHA-1 | 160-bit | Merkle–Damgård | Deprecated (SHAttered collision, 2017) |
| SHA-224/256/384/512 | matches name | Merkle–Damgård | Secure, industry standard |
| SHA-3 (Keccak) | 224/256/384/512-bit | Sponge (absorb/squeeze) | Secure, NIST standard (2015) |
| RIPEMD-160 | 160-bit | Merkle–Damgård variant | Legacy, used in Bitcoin addresses |
| Whirlpool | 512-bit | AES-derived (Rijndael-based) | Secure, less common |
| BLAKE2b / BLAKE2s | 512-bit / 256-bit | ChaCha-derived | Fast, secure, modern |

**Exam Note:** Birthday bound for collision resistance ≈ 2^(n/2) for an n-bit hash. Preimage resistance ≈ 2^n.

## MAC vs HMAC
| Feature | Generic MAC (naive H(key‖msg)) | HMAC |
|---|---|---|
| Length-extension vulnerable | Yes (on MD/SHA-1/SHA-2) | No |
| Construction | Simple concatenation | Nested double hash w/ ipad (0x36) & opad (0x5C) |
| RFC | — | RFC 2104 |
| Formula | H(K‖m) | H((K⊕opad)‖H((K⊕ipad)‖m)) |

**Common Mistake:** Assuming any keyed hash is automatically as secure as HMAC — naive constructions are NOT.

## Password Hashing & Key Stretching
| Function | Core Design | Memory-Hard? | Built-in Salt? | Notes |
|---|---|---|---|---|
| PBKDF2 | Iterated HMAC | No | No (salt param separate) | OWASP min. ~600,000 iterations (SHA-256) |
| bcrypt | Blowfish (Eksblowfish) | Partial | Yes | Cost factor controls work |
| scrypt | Custom, large memory blocks | Yes (strongest) | No (salt param separate) | Best resistance to GPU/ASIC attacks |

**Exam Note:** Salting defeats rainbow tables; key stretching (PBKDF2/bcrypt/scrypt) slows brute force via iteration count and/or memory cost — these are two distinct, complementary defenses, not the same thing.

## Quick Gotchas
- MD5/SHA-1 = collision-broken, never for signatures/integrity.
- HMAC ≠ encryption — it provides integrity + authenticity only, not confidentiality.
- Salt is stored in cleartext with the hash; it is not secret, just unique.
- scrypt > bcrypt > PBKDF2 in memory-hardness/GPU resistance, in that order.
