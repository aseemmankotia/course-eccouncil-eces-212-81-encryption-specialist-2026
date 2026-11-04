## Chapter 10: Cryptanalysis: Breaking Cryptosystems — Practice Questions

**Q1.** An analyst finds repeated ciphertext trigrams in a suspected Vigenère cipher at distances of 18, 24, and 30 characters apart. Using Kasiski examination, what is the most likely key length?

A) 6
B) 3
C) 8
D) 12

<details>
<summary>Answer</summary>

**Correct: A**

The GCD of 18, 24, and 30 is 6. Kasiski examination assumes the key length divides the distance between repeated sequences, so the GCD of all observed distances is the strongest candidate for key length.

**Why the others are wrong:**
- 3 is a factor of the GCD but not the GCD itself — it would only be correct if no larger common divisor existed.
- 8 does not evenly divide 18, so it cannot be the key length given these distances.
- 12 does not evenly divide 18 (18/12 is not a whole number), so it is mathematically inconsistent with the data.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A large amount of ciphertext from a monoalphabetic substitution cipher is available, with no known plaintext. Which technique is best suited to break it?

A) Kasiski examination
B) Frequency analysis
C) Differential cryptanalysis
D) Rainbow table lookup

<details>
<summary>Answer</summary>

**Correct: B**

Frequency analysis exploits the fact that letter frequencies in the plaintext language (e.g., E, T, A, O, I in English) are preserved as a fixed 1-to-1 mapping in monoalphabetic ciphers, making it the classic and most effective attack.

**Why the others are wrong:**
- Kasiski examination targets polyalphabetic ciphers (like Vigenère) to recover key length — it is irrelevant against a single fixed substitution alphabet.
- Differential cryptanalysis is a modern block-cipher attack requiring chosen plaintexts and round-based structures, not applicable to classical substitution ciphers.
- Rainbow tables are for reversing password hashes, not for breaking substitution ciphers.

</details>

---

**Q3.** A security team discovers that an attacker cracked a stolen password hash in minutes using a precomputed table instead of brute force. Which defense most directly prevents this attack from working in the future?

A) Increase the number of hash iterations only
B) Switch to a faster hashing algorithm
C) Add a unique salt per password before hashing
D) Encode the password with ROT13 before storage

<details>
<summary>Answer</summary>

**Correct: C**

A unique per-password salt forces an attacker to build a separate rainbow table for every possible salt value, making precomputed tables computationally infeasible — this is the direct, textbook countermeasure.

**Why the others are wrong:**
- Increasing iterations (like PBKDF2 rounds) slows brute force but does nothing to stop a rainbow table if salts are still absent or reused.
- A faster hash algorithm actually makes both brute force and rainbow table attacks easier, not harder.
- ROT13 is a trivial substitution with no cryptographic security value and is instantly reversible.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A researcher measures the CPU time a smart card takes to complete many RSA decryption operations, statistically correlating timing variations to infer bits of the private key. This is best classified as which type of attack?

A) Differential cryptanalysis
B) Linear cryptanalysis
C) Kasiski examination
D) Timing side-channel attack

<details>
<summary>Answer</summary>

**Correct: D**

This attack exploits the physical timing behavior of the implementation, not the mathematical structure of RSA itself — the defining characteristic of a side-channel attack.

**Why the others are wrong:**
- Differential cryptanalysis analyzes how input plaintext differences propagate through a block cipher's rounds — it does not involve physical timing measurements.
- Linear cryptanalysis uses linear approximations of S-box behavior with known plaintext-ciphertext pairs, not timing data.
- Kasiski examination is a classical technique for finding Vigenère key length from repeated ciphertext patterns, unrelated to RSA or timing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A pentester needs to crack a large batch of NTLM password hashes as fast as possible using GPU acceleration. Which tool is the best fit?

A) hashcat
B) Wireshark
C) A custom Kasiski script
D) OpenSSL

<details>
<summary>Answer</summary>

**Correct: A**

hashcat is purpose-built for GPU-accelerated password/hash recovery and natively supports NTLM (mode 1000), making it dramatically faster than CPU-based approaches for large hash sets.

**Why the others are wrong:**
- Wireshark is a packet capture and network analysis tool with no password-cracking capability.
- Kasiski examination is a classical cipher-breaking technique for Vigenère ciphers, unrelated to hash cracking.
- OpenSSL is a cryptographic library/toolkit for implementing crypto operations, not a dedicated password-cracking engine.

</details>

---

**Q6.** What distinguishes differential cryptanalysis from linear cryptanalysis?

A) Differential analyzes linear approximations of cipher operations; linear studies fixed plaintext differences.
B) Differential cryptanalysis requires no plaintext at all; linear cryptanalysis requires full key recovery before analysis begins.
C) Differential and linear cryptanalysis are the same technique published under two different names.
D) Differential cryptanalysis tracks how input plaintext differences propagate to ciphertext differences (chosen-plaintext); linear cryptanalysis builds linear approximations relating plaintext, ciphertext, and key bits (known-plaintext).

<details>
<summary>Answer</summary>

**Correct: D**

This correctly captures both the underlying method (difference propagation vs. linear approximation) and the attack model (chosen-plaintext vs. known-plaintext), which is exactly how the exam distinguishes the two.

**Why the others are wrong:**
- This swaps the definitions — it describes linear cryptanalysis's method as differential's and vice versa.
- Both techniques require plaintext-ciphertext pairs collected before analysis; key recovery is the goal, not a prerequisite.
- They are distinct techniques developed by different researchers (Biham/Shamir vs. Matsui) using fundamentally different mathematical approaches.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Integral cryptanalysis (the Square attack) is most effective against which cipher structure?

A) Feistel networks with randomized S-boxes
B) One-time pads
C) Substitution-Permutation Networks (SPN) like AES/Square
D) Stream ciphers based on LFSRs

<details>
<summary>Answer</summary>

**Correct: C**

Integral cryptanalysis was designed against and is most effective on SPN-based block ciphers, tracking sets of plaintexts where certain bytes are held constant (fixed) and others vary across all possible values (active), exploiting the algebraic structure of AES-like ciphers.

**Why the others are wrong:**
- Feistel networks have a different structural weakness profile and are more commonly targeted by differential/linear cryptanalysis.
- One-time pads are information-theoretically secure when used correctly and are not vulnerable to any cryptanalytic technique.
- LFSR-based stream ciphers are typically attacked via correlation attacks or algebraic attacks, not integral cryptanalysis.

</details>

---

**Q8.** An analyst has a 500,000-entry wordlist and wants to test it, with common mangling rules (appending numbers, capitalization changes), against 10,000 leaked password hashes. Which approach is best?

A) Brute-force attack testing every possible character combination
B) Dictionary attack with rule-based mangling using John the Ripper
C) Kasiski examination on the hash values
D) Rainbow table lookup only, with no wordlist

<details>
<summary>Answer</summary>

**Correct: B**

John the Ripper's rule engine applies mangling transformations (case changes, appended digits, leetspeak) to wordlist entries, making it the standard efficient approach when a targeted wordlist and common human password patterns are available.

**Why the others are wrong:**
- Brute force testing all combinations is exponentially slower and unnecessary when a targeted wordlist already covers likely candidates.
- Kasiski examination applies to classical polyalphabetic ciphers, not modern cryptographic hash functions.
- Rainbow tables require unsalted hashes and precomputed chains matching the exact hash algorithm/charset — they don't leverage a custom wordlist with mangling rules.

</details>

---

