## Chapter 12: Full 212-81 Exam Simulation and Time-Management Strategy — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | 212-81 exam format: number of questions, duration, and passing score? | 50 questions, 120 minutes, 70% passing score. Exam tip: budget ~2.4 min/question, leaving a buffer for flagged reviews. |
| 2 | AES key size mandated for Top Secret vs Secret classification (CNSA/Suite B)? | AES-128 = Secret, AES-256 = Top Secret. Exam tip: 'Top Secret' scenario keyword = pick the AES-256 answer. |
| 3 | SHA-256 vs SHA3-256 output size? | Both produce 256-bit digests. Exam tip: don't assume SHA-3 outputs differ in size — only the internal structure (sponge vs Merkle-Damgård) differs. |
| 4 | CBC vs CTR vs GCM — which mode provides built-in authentication? | Only GCM is AEAD (encryption + authentication tag). CBC/CTR need a separate MAC via Encrypt-then-MAC. Exam tip: 'integrity + confidentiality in one mode' = GCM. |
| 5 | RSA static key transport vs DHE/ECDHE — which gives forward secrecy? | DHE/ECDHE (ephemeral keys per session). Static RSA key transport does not. Exam tip: 'forward secrecy' keyword eliminates static RSA answers. |
| 6 | Which crypto primitive verifies sender identity + integrity with no pre-shared secret? | Digital signature (sign with private key, verify with public key). Exam tip: eliminate HMAC answers whenever the question states 'no pre-shared key.' |
| 7 | Minimum acceptable RSA modulus size on the current exam for reasonable security? | 2048-bit minimum; 3072/4096-bit for higher assurance. Exam tip: 1024-bit RSA is the deprecated/insecure distractor to eliminate. |
| 8 | OpenSSL command to generate a 2048-bit RSA private key? | openssl genrsa -out private.pem 2048 . Exam tip: know genrsa vs genpkey vs req flags — the exam may show CLI snippets. |
| 9 | OpenSSL command to create a self-signed X.509 cert valid 365 days? | openssl req -x509 -new -key private.pem -days 365 -out cert.pem . Exam tip: the -x509 flag produces a self-signed cert instead of a CSR. |
| 10 | Common Modulus Attack — what scenario triggers it? | Same RSA modulus N reused with different public exponents e for the same plaintext. Exam tip: 'shared N' keyword in the question = Common Modulus Attack answer. |
| 11 | Birthday attack rule of thumb for an n-bit hash? | ~2^(n/2) attempts needed for a 50% collision chance. Exam tip: for a 128-bit hash, collision resistance is effectively 2^64 — far weaker than its 2^128 preimage resistance. |
| 12 | S/MIME vs PGP — trust model difference? | S/MIME = hierarchical CA-issued certificate trust. PGP = decentralized web of trust (peer endorsements). Exam tip: 'CA-issued cert' keyword = S/MIME; 'peer trust network' keyword = PGP. |
