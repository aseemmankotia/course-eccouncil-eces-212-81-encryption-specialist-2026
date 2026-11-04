## Chapter 1 Cheat Sheet — Crypto Foundations & Classical Ciphers

### Core Security Goals (CIA + Non-repudiation)
| Goal | Meaning | Mechanism |
|---|---|---|
| Confidentiality | Keep data secret | Encryption |
| Integrity | Data not altered | Hashing, MAC |
| Authentication | Verify identity | Passwords, certs, MAC |
| Non-repudiation | Sender can't deny sending | Digital signature (NOT MAC — MAC uses shared key) |

### Classical Ciphers
| Cipher | Type | Key | Notes |
|---|---|---|---|
| Caesar | Monoalphabetic shift | 1 shift value (1-25) | Broken by brute force/frequency analysis |
| Atbash | Fixed substitution | None | A<->Z reversal, self-inverse |
| Affine | Monoalphabetic math | (a,b), gcd(a,26)=1 | E(x)=(ax+b) mod 26; 12 valid a values → 312 keyspace |
| Vigenere | Polyalphabetic | Keyword | Broken via Kasiski examination (key length repetition) |
| Playfair | Digraph substitution | 5x5 grid keyword | I/J combined, 25 cells, encrypts letter pairs |
| Rail Fence | Transposition | # of rails | Zigzag write, row-by-row read; no substitution |
| ADFGVX | Substitution+transposition | 6x6 grid + columnar key | WWI German cipher; letters A D F G V X only |
| Homophonic | Substitution | Multiple symbols/letter | Flattens frequency distribution |
| Null cipher | Concealment | Position rule | Real message hidden among filler characters |

### Affine Cipher Valid 'a' Values (mod 26)
1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25 — must be coprime with 26 (12 values). Invalid a → cipher not invertible, decryption fails/ambiguous.

### Enigma Machine
- **Rotors:** scramble substitution, step with each keypress (odometer-style), notches trigger stepping of adjacent rotor.
- **Reflector (Umkehrwalze):** sends signal back through rotors; causes core flaw — **a letter never encrypts to itself**.
- **Plugboard (Steckerbrett):** swaps up to 10 letter pairs before/after rotor pass; increases keyspace, does not fix self-encryption flaw.
- Exam trap: assuming plugboard changes rotor stepping — it does not.

### Kerckhoffs's Principle
System must stay secure even if the algorithm is fully public — only the **key** must remain secret. Opposite of security-through-obscurity.

### Common Exam Traps
- Confusing MAC (shared key, no non-repudiation) with digital signature (private key, provides non-repudiation).
- Off-by-one letter indexing errors in Vigenere/Caesar math (A=0 vs A=1).
- Choosing an affine 'a' not coprime with 26.
- Assuming ADFGVX is 'just Playfair with more letters' — it adds columnar transposition.
- Believing Enigma's plugboard alone accounts for its security — rotor wiring + reflector + plugboard combine for total keyspace.
