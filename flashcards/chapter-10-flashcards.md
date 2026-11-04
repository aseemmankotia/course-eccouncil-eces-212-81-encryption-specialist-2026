## Chapter 10: Cryptanalysis: Breaking Cryptosystems — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Most common letter in English plaintext (frequency analysis)? | E (~12.7%). Exam tip: memorize the top 5 — E, T, A, O, I — as the basis for breaking monoalphabetic substitution ciphers. |
| 2 | Kasiski examination — what value do you compute from distances between repeated ciphertext sequences? | The GCD (greatest common divisor) of the distances — it equals the likely Vigenère key length or a factor of it. |
| 3 | Who invented Kasiski examination, and when? | Friedrich Kasiski, 1863. Exam tip: it broke the long-standing myth that Vigenère ciphers were unbreakable. |
| 4 | Linear cryptanalysis vs. differential cryptanalysis — attack model? | Linear = known-plaintext attack using linear approximations of S-boxes. Differential = chosen-plaintext attack tracking XOR differences through rounds. |
| 5 | Who publicly developed differential cryptanalysis? | Eli Biham and Adi Shamir, late 1980s. Exam tip: NSA is believed to have known of it earlier when hardening DES S-boxes. |
| 6 | Who developed linear cryptanalysis? | Mitsuru Matsui, 1993 — first practical attack recovering keys from full DES. |
| 7 | Integral cryptanalysis is also known as? | The Square attack — tracks sums/balance over sets of plaintexts (active vs. fixed bytes) to break SPN ciphers like AES/Square. |
| 8 | Rainbow table vs. brute force — key trade-off? | Rainbow tables trade storage for computation time (precomputed hash chains) for fast lookups. Salting defeats them by forcing a unique table per salt value. |
| 9 | hashcat vs. John the Ripper — primary distinction? | hashcat = GPU-accelerated, optimized for raw speed on large hash sets. John the Ripper = CPU-based, flexible with format auto-detection and a strong rule/mangling engine. |
| 10 | hashcat command to crack MD5 hashes with a wordlist and rules? | `hashcat -m 0 -a 0 hashes.txt wordlist.txt -r rules/best64.rule` — Exam tip: -m sets hash mode (0=MD5), -a sets attack mode (0=dictionary). |
| 11 | Power analysis: SPA vs. DPA? | SPA (Simple Power Analysis) = visual inspection of a single power trace. DPA (Differential Power Analysis) = statistical analysis across many traces to extract key bits. Both attack the implementation, not the algorithm. |
| 12 | What do side-channel attacks target? | The physical implementation (timing, power draw, EM emissions, faults) — NOT the mathematical strength of the algorithm. Exam trap: a mathematically 'unbreakable' algorithm can still fall to side channels. |
