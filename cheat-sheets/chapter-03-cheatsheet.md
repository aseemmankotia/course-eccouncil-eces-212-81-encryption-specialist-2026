## Cipher Modes Cheat Sheet

| Mode | IV/Nonce? | Parallel Enc | Parallel Dec | Random Access | Error Propagation | Padding? | Key Vulnerability |
|---|---|---|---|---|---|---|---|
| ECB | No | Yes | Yes | Yes | None (block-local) | Yes | Pattern leakage — 'ECB penguin' |
| CBC | Yes (unpredictable) | No | Yes | No | Self-heals after 2 blocks | Yes | Padding oracle if errors distinguishable |
| PCBC | Yes | No | No | No | Propagates through ALL following blocks | Yes | Used in Kerberos v4; fragile to bit errors |
| CFB | Yes | No | Yes | No | Self-synchronizing, recovers after few blocks | No | IV reuse leaks keystream |
| OFB | Yes (nonce) | No (keystream precompute sequential) | Yes | No | Bit-error stays local, but nonce reuse catastrophic | No | Nonce reuse = keystream reuse |
| CTR | Yes (nonce+counter) | Yes | Yes | Yes | Bit-error stays local | No | Nonce+counter reuse = keystream reuse |

### Exam Gotchas
- **ECB**: never use for anything beyond single-block/random data (e.g., key wrapping of already-random keys).
- **CBC**: IV must be unpredictable, NOT secret. Distinguishable padding errors → padding oracle (POODLE-class).
- **CTR/OFB**: reusing nonce/counter with same key = catastrophic keystream reuse, breaks confidentiality like OTP reuse.

### Key Stretching vs Salting
| Technique | Defends Against | Mechanism | Examples |
|---|---|---|---|
| Salting | Rainbow tables | Unique random value per hash | Random 16+ byte salt per user |
| Stretching | Brute force / GPU cracking | Deliberate iteration/memory cost | PBKDF2, bcrypt, scrypt, Argon2 |

OWASP (2023 guidance, still current baseline): PBKDF2-HMAC-SHA256 ≥ 600,000 iterations.

### Key Scheduling & S-boxes
- **Key schedule**: expands master key → unique round key per round.
- **AES round keys**: AES-128 → 11, AES-192 → 13, AES-256 → 15.
- **S-boxes**: provide *confusion* (nonlinear substitution); resist linear/differential cryptanalysis. DES S-box: 6-bit in → 4-bit out.

### Quick Memory Trick
ECB = **E**very **B**lock **C**opies pattern.
CBC = **C**hained **B**locks, **C**orrupt-recovering.
CTR/OFB = **C**ounter/**O**utput **F**eedback — never reuse the nonce, ever.
