## Chapter 4: Hash Functions, MAC, and HMAC — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | MD5 digest output size and status? | 128 bits. Practically broken via chosen-prefix collision attacks since 2004-2008. Exam tip: never select MD5 for security-critical integrity or password hashing. |
| 2 | SHA-1 digest output size and status? | 160 bits. Deprecated after the 2017 SHAttered collision attack (Google/CWI). Exam tip: collision resistance broken, but preimage resistance still theoretically intact. |
| 3 | SHA-2 family output sizes tested on 212-81? | SHA-224, SHA-256, SHA-384, SHA-512 — the number in the name equals the output bit length. Exam tip: SHA-256/512 are the most heavily tested variants. |
| 4 | SHA-3 underlying algorithm and construction type? | Based on Keccak, using a sponge construction (absorb then squeeze), unlike the Merkle–Damgård design used in MD5/SHA-1/SHA-2. Exam tip: sponge vs Merkle–Damgård is a classic comparison question. |
| 5 | RIPEMD-160 output size and origin? | 160 bits; European-designed alternative to SHA-1, notably used in Bitcoin address generation. Exam tip: same output size as SHA-1 but a different design lineage. |
| 6 | Whirlpool hash output size and design basis? | 512-bit output; internal compression function derived from the AES (Rijndael) cipher design. Exam tip: Whirlpool = AES-based, 512-bit digest. |
| 7 | HMAC formula per RFC 2104? | HMAC(K,m) = H((K⊕opad) \|\| H((K⊕ipad) \|\| m)). ipad = 0x36, opad = 0x5C, each repeated to the hash's block size. Exam tip: memorize the exact ipad/opad hex values. |
| 8 | Why prefer HMAC over a naive keyed hash H(key\|\|message)? | Naive concatenation is vulnerable to length-extension attacks on Merkle–Damgård hashes (MD5/SHA-1/SHA-2). HMAC's nested structure prevents this. Exam tip: 'length-extension attack' is a key exam trap term. |
| 9 | Purpose of a salt in password hashing? | A random, unique value combined with the password before hashing; defeats precomputed rainbow tables and ensures identical passwords produce different hashes. Exam tip: salts are stored alongside the hash, not kept secret. |
| 10 | bcrypt: underlying cipher and built-in salt? | Based on the Blowfish cipher (Eksblowfish key schedule); includes a built-in salt automatically. Exam tip: bcrypt = Blowfish + adjustable cost/work factor. |
| 11 | scrypt: primary design goal vs PBKDF2/bcrypt? | Memory-hard KDF built specifically to resist large-scale parallel cracking on GPUs/ASICs/FPGAs by requiring significant RAM per attempt. Exam tip: scrypt offers the strongest GPU/ASIC resistance of the three key-stretching functions. |
| 12 | PBKDF2-HMAC-SHA256 recommended minimum iterations (OWASP)? | 600,000 iterations per current OWASP Password Storage Cheat Sheet guidance. Exam tip: PBKDF2 relies solely on iteration count/CPU cost, not memory-hardness. |
