## Chapter 12 Cheat Sheet — Exam Simulation & Time Management

### Exam Format Quick Facts
| Item | Value |
|---|---|
| Questions | 50 |
| Duration | 120 minutes |
| Passing score | 70% |
| Time per question | ~2.4 min average |

### Time Budget Plan
| Phase | Time | Action |
|---|---|---|
| First pass | 0–75 min | Answer every question you're confident on immediately. Flag anything uncertain — do not stall. |
| Second pass | 75–100 min | Return to flagged questions. Apply elimination strategy (below). |
| Final pass | 100–115 min | Re-check flagged answers only. Do not re-read questions you already answered confidently. |
| Buffer | 115–120 min | Submit-check: confirm every question has an answer selected — no blanks. |

### Elimination Strategy (Two Plausible Distractors)
1. Identify the scenario keyword (e.g., 'forward secrecy', 'no pre-shared key', 'Top Secret', 'CA-issued').
2. Eliminate any option that fails that keyword outright (e.g., static RSA when forward secrecy is required).
3. Between the remaining two plausible options, check for a **missing requirement** (e.g., confidentiality-only vs confidentiality+integrity).
4. Pick the option satisfying ALL stated requirements, not just the majority.

### Highest-Yield Gotchas by Domain
| Domain | Gotcha |
|---|---|
| Symmetric | ECB always leaks patterns; GCM = only mode with built-in auth |
| Asymmetric | Static RSA ≠ forward secrecy; DHE/ECDHE = forward secrecy |
| Hashing | SHA-256 and SHA3-256 both output 256 bits despite different internals |
| PKI | S/MIME = CA trust; PGP = web of trust |
| Attacks | Shared modulus + different exponents = Common Modulus Attack |
| Applications | Email confidentiality+signing = S/MIME, not TLS alone |

### Final 15-Minute Checklist
- [ ] Every question has a selected answer (no blanks — guessing beats zero credit)
- [ ] Re-verify flagged questions only, using keyword elimination
- [ ] Double-check any question involving classification levels (Secret vs Top Secret → AES-128 vs AES-256)
- [ ] Double-check any question involving key exchange forward secrecy
- [ ] Confirm you did not confuse hash output sizes (SHA-1=160, SHA-256/SHA3-256=256, SHA-512=512)
- [ ] Submit only after full review — do not exit early even if time remains

### Reminder
Always check the current official EC-Council 212-81 exam outline before scheduling — objective wording and emphasis can shift between blueprint revisions.
