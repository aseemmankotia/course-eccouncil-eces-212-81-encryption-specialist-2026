## Chapter 3: Cipher Modes, Key Scheduling, and Key Management — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | ECB mode security flaw? | Identical plaintext blocks always produce identical ciphertext blocks (no IV, no chaining). Exam tip: 'ECB penguin' image is the classic proof — visible patterns leak through encryption. |
| 2 | CBC mode IV requirement? | Must be unpredictable and unique per encryption under the same key; does NOT need to be secret. Predictable IVs enabled the BEAST attack. |
| 3 | CBC padding oracle attack — what does the attacker exploit? | Distinguishable error responses (padding valid/invalid) let the attacker decrypt ciphertext block-by-block without the key. Mitigation: use authenticated encryption (e.g., GCM) or constant-time error handling. |
| 4 | PCBC vs CBC — key difference? | PCBC XORs previous plaintext AND previous ciphertext into the next block, so errors propagate through ALL following blocks. CBC only XORs previous ciphertext, so it self-recovers after 2 blocks. PCBC was used in Kerberos v4. |
| 5 | CFB mode key characteristic? | Turns a block cipher into a self-synchronizing stream cipher by feeding ciphertext back as cipher input. Can recover from bit errors after a few blocks; no padding needed. |
| 6 | OFB mode — consequence of nonce/IV reuse? | Reusing the IV with the same key regenerates the identical keystream. XORing two ciphertexts cancels the keystream, exposing XOR of the plaintexts — same failure mode as OTP reuse. |
| 7 | CTR mode advantage over CBC/CFB/OFB? | Supports parallel encryption/decryption and random access to any block, since each block's keystream is derived independently from counter+nonce. Same nonce-reuse risk as OFB. |
| 8 | Salting vs Key Stretching — difference? | Salting adds unique random data per user to defeat precomputed rainbow tables. Key stretching (PBKDF2/bcrypt/scrypt/Argon2) adds computational cost (iterations/memory-hardness) to slow brute force. Use BOTH for password storage. |
| 9 | PBKDF2 iteration guidance (OWASP, current baseline)? | OWASP Password Storage Cheat Sheet recommends 600,000+ iterations for PBKDF2-HMAC-SHA256 as of the 2023 update, still cited as current guidance. Exam tip: know WHY stretching matters more than the exact number. |
| 10 | Purpose of S-boxes in block ciphers (e.g., DES, AES)? | Provide confusion — nonlinear substitution that obscures the relationship between key and ciphertext, resisting linear/differential cryptanalysis. DES S-boxes: 6-bit input → 4-bit output. |
| 11 | What does a key schedule algorithm produce? | Expands the master key into a distinct round key (subkey) for each encryption round, so every round uses different key material from one original key. |
| 12 | AES round keys generated per key size? | AES-128: 11 round keys (10 rounds). AES-192: 13 round keys (12 rounds). AES-256: 15 round keys (14 rounds). Exam tests these exact counts. |
