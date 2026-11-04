## Chapter 2 Cheat Sheet: Block & Stream Ciphers (DES to AES)

### Symmetric Algorithm Quick Reference

| Algorithm | Block Size | Key Size | Rounds | Structure | Status |
|---|---|---|---|---|---|
| DES | 64-bit | 64-bit (56 effective) | 16 | Feistel | Broken (brute force) |
| 3DES (2-key) | 64-bit | 112-bit raw (~80 effective) | 48 (3x16) | Feistel EDE | Deprecated |
| 3DES (3-key) | 64-bit | 168-bit raw (112 effective) | 48 (3x16) | Feistel EDE | Legacy use only |
| AES-128 | 128-bit | 128-bit | 10 | SPN | Current standard |
| AES-192 | 128-bit | 192-bit | 12 | SPN | Current standard |
| AES-256 | 128-bit | 256-bit | 14 | SPN | Current standard |
| Blowfish | 64-bit | 32-448 bit | 16 | Feistel | Legacy, still usable |
| Twofish | 128-bit | up to 256-bit | 16 | Feistel | AES finalist (lost) |
| Serpent | 128-bit | up to 256-bit | 32 | SPN | AES finalist (lost, most conservative) |
| IDEA | 64-bit | 128-bit | 8.5 | Lai-Massey | Used in early PGP |
| RC4 | Stream | 40-2048 bit | N/A | Stream (KSA+PRGA) | Deprecated (biased keystream) |
| TEA | 64-bit | 128-bit | 64 (32 cycles) | Feistel-like | Weak (related-key attacks) |

### Memory Tricks
- **AES rounds = key size / 16 + 6**: 128/16+6=... (use table above, don't rely on formula in exam — just memorize 10/12/14)
- **3DES effective strength**: 2-key drops one key → attacker meet-in-middle cuts strength roughly in half (~80 bits); 3-key keeps full 112-bit effective strength.
- **DES 56 not 64**: "8 bits go to parity, not security."

### Block vs Stream — Decision Rule
- Need padding tolerance, data at rest, files → **Block cipher**
- Need continuous, real-time, low-latency, no padding → **Stream cipher**

### Common Exam Traps
1. Confusing DES's 64-bit *key field* with its 56-bit *effective* strength — exam always asks for effective strength.
2. Assuming 2-key and 3-key 3DES give equal security — they do NOT (80 vs 112 bits).
3. Forgetting AES block size is ALWAYS 128 bits regardless of key size — only the key size and round count change.
4. Picking RC4 for "fast lightweight encryption" without noting its deprecated status due to keystream bias.
5. Confusing Rijndael (submission name) with AES (the standardized name) — they are the same algorithm.

### S-boxes and Key Scheduling
- **S-boxes**: provide *confusion* (nonlinearity). DES: 8 S-boxes, 6-bit in → 4-bit out.
- **Key scheduling**: generates all round subkeys from the master key. Weak schedules (DES weak keys, TEA related-key flaw) are common exam gotchas.
