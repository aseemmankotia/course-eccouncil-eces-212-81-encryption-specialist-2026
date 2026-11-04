# Cryptanalysis Cheat Sheet

## Classical Attacks
| Technique | Target | Requirement | Key Idea |
|---|---|---|---|
| Frequency analysis | Monoalphabetic substitution | Large ciphertext, no plaintext needed | Letter frequency preserved 1:1 (E≈12.7%, T,A,O,I next) |
| Kasiski examination | Polyalphabetic (Vigenère) | Repeated ciphertext sequences | GCD of distances between repeats ≈ key length |
| Index of Coincidence | Polyalphabetic | Statistical | Confirms/refines Kasiski's key-length estimate |

## Modern Block Cipher Attacks
| Technique | Attack Model | Author(s) | Targets |
|---|---|---|---|
| Linear cryptanalysis | Known-plaintext | Mitsuru Matsui (1993) | Linear approximations of S-boxes; broke full DES |
| Differential cryptanalysis | Chosen-plaintext | Biham & Shamir (late 1980s) | Tracks XOR difference propagation through rounds |
| Integral (Square) cryptanalysis | Chosen-plaintext, sets | — | SPN ciphers (AES/Square); active vs. fixed byte sets |

## Side-Channel Attacks (attack the implementation, not the math)
| Type | Mechanism |
|---|---|
| Timing attack | Correlate operation duration to key-dependent branching/ops |
| SPA (Simple Power Analysis) | Visual inspection of a single power trace |
| DPA (Differential Power Analysis) | Statistical analysis across many power traces |
| Electromagnetic (EM) analysis | Capture EM emissions during crypto operations |
| Fault injection | Induce errors (voltage/clock glitching) to leak key data |

**Exam note:** Side-channel attacks bypass strong math entirely — a provably secure cipher can still fall if the implementation leaks physical signals.

## Password Cracking: Rainbow Tables vs. Brute Force
| Method | Trade-off | Defeated by |
|---|---|---|
| Brute force | High compute, low storage | Longer/complex passwords, high iteration counts |
| Rainbow table | Low compute (lookup), high precomputed storage | **Salting** — unique salt per hash forces a new table per salt |

**Rule:** Salting doesn't slow down cracking a single hash much — it prevents *reusing* one precomputed table across many accounts.

## Tools
| Tool | Compute | Strength |
|---|---|---|
| hashcat | GPU | Raw speed, huge hash-mode support (`-m`), attack modes (`-a`) |
| John the Ripper | CPU | Format auto-detection, flexible rule/mangling engine |

**Command pattern:** `hashcat -m <hash_type> -a <attack_mode> hashes.txt wordlist.txt -r rules.rule`

## Common Exam Traps
- Confusing linear (known-plaintext) with differential (chosen-plaintext) attack models.
- Assuming increasing hash speed helps security — it always helps the attacker more.
- Assuming salting alone prevents brute force — it only defeats **precomputation reuse** (rainbow tables), not per-hash brute force.
- Forgetting Kasiski's GCD step can yield a *factor* of the true key length, not just the length itself — verify with Index of Coincidence.
