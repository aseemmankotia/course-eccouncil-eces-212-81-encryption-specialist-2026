## Chapter 2: Block and Stream Ciphers: DES to AES — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | DES: block size, key size, effective key strength, rounds? | 64-bit block, 64-bit key field (56-bit effective + 8 parity bits), 16 rounds, Feistel structure. Exam tip: DES is brute-forceable in hours on modern hardware. |
| 2 | 3DES: 2-key vs 3-key effective strength? | 2-key (K1,K2,K1) = ~80-bit effective strength. 3-key (K1,K2,K3) = 112-bit effective strength. Both use EDE (Encrypt-Decrypt-Encrypt) mode. Exam tests these exact numbers. |
| 3 | AES key sizes and matching round counts? | 128-bit key = 10 rounds. 192-bit key = 12 rounds. 256-bit key = 14 rounds. Block size is always 128 bits regardless of key size. |
| 4 | What algorithm won the NIST AES competition and what was its original name? | Rijndael (by Daemen and Rijmen) won in 2001 and was standardized as AES. Exam tip: 'Rijndael' and 'AES' are used interchangeably on exams. |
| 5 | Blowfish key size, block size, rounds? | Variable key size 32-448 bits, 64-bit block, 16 rounds, Feistel structure. Designed by Bruce Schneier as a fast, free DES alternative. |
| 6 | Twofish vs Serpent — both were AES finalists, why wasn't either chosen? | Twofish (128-bit block, up to 256-bit key) and Serpent (128-bit block, up to 256-bit key, 32 rounds) both lost to Rijndael. Serpent was considered more secure but slower; Twofish was fast but more complex to implement in hardware. |
| 7 | IDEA: key size, block size, historical use? | 128-bit key, 64-bit block, 8.5 rounds. Historically used in early versions of PGP for symmetric encryption. |
| 8 | RC4: cipher type and primary weakness? | Byte-oriented stream cipher, variable key length (40-2048 bits). Weakness: statistical biases in early keystream bytes allow plaintext recovery. Deprecated in TLS (RFC 7465). |
| 9 | TEA (Tiny Encryption Algorithm): structure and known weakness? | 64-bit block, 128-bit key, 64 rounds (32 cycles) using only XOR, ADD, and shift operations. Known weakness: vulnerable to related-key attacks and has equivalent keys. |
| 10 | Block cipher vs stream cipher — best use case for each? | Block cipher: fixed-size data at rest, files, database records (needs padding). Stream cipher: continuous real-time data like voice/video streams, low-latency requirements, no padding needed. |
| 11 | What is the purpose of an S-box in a block cipher? | S-boxes (substitution boxes) provide confusion by nonlinearly mapping input bits to output bits, preventing linear cryptanalysis. DES uses 8 S-boxes, each mapping 6-bit input to 4-bit output. |
| 12 | What is key scheduling and why does a weak schedule matter? | Key scheduling is the algorithm that derives all round subkeys from the master key. A weak key schedule (e.g., in DES's weak keys, or TEA's related-key issue) can let attackers exploit relationships between keys to break the cipher faster than brute force. |
