# Practice Test 1: ECES 212-81: Applied Cryptography Exam Prep

- **Questions:** 46
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A CTF challenge gives you the ciphertext 'KHOOR ZRUOG' and tells you it was encrypted with a simple substitution where every letter is shifted by the same fixed amount through the alphabet. Which classical cipher was used, and what is the plaintext?

A) Vigenere cipher; plaintext is 'WORLD HELLO'
B) Atbash cipher; plaintext is 'HELLO WORLD'
C) Playfair cipher; plaintext is 'HELLO WORLD'
D) Caesar cipher; plaintext is 'HELLO WORLD'

---

**Q2.** You need to teach a class the historical evolution from monoalphabetic to polyalphabetic substitution ciphers used to defeat frequency analysis. Which cipher should you select to demonstrate a keyword-based cipher where the same plaintext letter can map to different ciphertext letters depending on its position?

A) ROT13
B) Vigenere cipher
C) Rail Fence cipher
D) Affine cipher

---

**Q3.** You are configuring a classical Playfair cipher by hand and need to build the 5x5 key square before encrypting any digraphs. Which configuration step is required to correctly build this grid?

A) Fill the grid using ROT13 to generate letter positions automatically
B) Combine the letters I and J into a single cell since only 25 cells are available for 26 letters
C) Reverse the entire alphabet and place it into the grid in that order
D) Use a separate 6x6 grid to accommodate all 26 letters plus digits

---

**Q4.** Which cryptographic goal is specifically satisfied when a digital signature proves that a specific sender created a message and that sender cannot later deny having sent it?

A) Confidentiality
B) Non-repudiation
C) Integrity
D) Availability

---

**Q5.** During WWII, a German operator sets the Enigma machine's rotors and plugboard each morning according to a daily key sheet, then types a message that is scrambled letter by letter as the rotors step with each keypress. Which core Enigma component ensures that a letter is never encrypted to itself, a property later exploited by Allied cryptanalysts?

A) The plugboard (Steckerbrett)
B) The rotor stepping mechanism
C) The daily key sheet
D) The reflector (Umkehrwalze)

---

**Q6.** A cloud storage provider needs to encrypt data blocks on an SSD where individual blocks must be randomly accessed and decrypted independently, and the encryption process should be parallelizable across multiple CPU cores. Which block cipher mode of operation BEST meets these requirements?

A) ECB mode, because each block is encrypted independently allowing full parallelism
B) CBC mode, because chaining guarantees data integrity as well as confidentiality
C) CTR mode, because it turns the block cipher into a keyed keystream generator using an incrementing counter, enabling random access and full parallelism for both encryption and decryption
D) OFB mode, because the keystream can be precomputed once and reused for any block

---

**Q7.** A financial application already has a FIPS-validated AES-128 implementation in place and needs to add message authentication for transaction records without introducing a separate hash-function library. Which MAC construction should the developers use?

A) HMAC-SHA256, since it is the industry standard for message authentication
B) A plain MD5 checksum appended to the message
C) CMAC (Cipher-based MAC), since it derives the authentication tag directly from the existing AES block cipher implementation
D) CRC32 computed over the message payload

---

**Q8.** A security architect is implementing PBKDF2 for password hashing and must choose a minimum salt length that follows current best-practice guidance to defeat precomputed rainbow-table attacks. Which value should be selected?

A) 4 bytes (32 bits)
B) 0 bytes — salting is optional if the iteration count is high enough
C) 1 byte (8 bits)
D) 16 bytes (128 bits)

---

**Q9.** Which statement correctly differentiates a stream cipher from a block cipher?

A) Block ciphers cannot be used in any mode that emulates stream-cipher behavior
B) Stream ciphers always require padding to fill a fixed block size, while block ciphers never require padding
C) A stream cipher such as RC4 encrypts data one bit or byte at a time by XORing it with a generated keystream, while a block cipher such as AES encrypts fixed-size blocks of plaintext at once
D) Stream ciphers rely on substitution-permutation networks and S-boxes, while block ciphers rely solely on XOR operations with a keystream

---

**Q10.** A legacy banking system currently uses single DES, and a security audit flags the 56-bit effective key length as insufficient against brute-force attacks. The team wants to significantly increase effective key strength while reusing the existing DES hardware/software modules. Which approach should they implement?

A) Implement Triple DES (3DES) using the Encrypt-Decrypt-Encrypt (EDE) construction with two or three independent 56-bit keys
B) Pad the DES key to 128 bits before use to increase its strength
C) Switch DES to ECB mode, since ECB is inherently more resistant to brute-force key search
D) Double the number of DES rounds from 16 to 32 to strengthen the algorithm

---

**Q11.** An organization must replace SHA-1 in its code-signing pipeline after published collision attacks (such as SHAttered) demonstrated practical collisions. Which hash function should be selected to provide strong collision resistance for new signatures?

A) MD5, since it produces a shorter digest and is faster to compute
B) SHA-1 configured with a longer secret key
C) RIPEMD-128, since a shorter digest reduces storage overhead
D) SHA-256, since it is part of the SHA-2 family and has no known practical collision attacks

---

**Q12.** A company needs to encrypt a large real-time video stream on multi-core hardware. The design requires that encryption and decryption both be fully parallelizable and that any encrypted block be randomly accessible without decrypting preceding blocks. Which cipher mode of operation BEST satisfies these requirements?

A) CBC (Cipher Block Chaining)
B) CTR (Counter mode)
C) CFB (Cipher Feedback)
D) ECB (Electronic Codebook)

---

**Q13.** Which block cipher mode of operation is described as 'self-synchronizing,' meaning that if a ciphertext bit is corrupted or lost during transmission, correct decryption automatically resumes after a limited number of subsequent blocks?

A) OFB (Output Feedback)
B) CTR (Counter mode)
C) ECB (Electronic Codebook)
D) CFB (Cipher Feedback)

---

**Q14.** An implementation builds a message authentication code as: MAC = H((K XOR opad) || H((K XOR ipad) || message)). Which construction is this, and what value is opad typically set to for a hash function like SHA-256?

A) CMAC; opad = 0x5C repeated to the block size
B) HMAC; opad = 0x36 repeated to the block size
C) HMAC; opad = 0x5C repeated to the block size
D) CBC-MAC; opad = 0x5C repeated to the block size

---

**Q15.** Blowfish initializes its P-array and four 8-bit-input S-boxes using the hexadecimal digits of which mathematical constant before XORing in the actual key, and what is Blowfish's fixed block size?

A) The golden ratio; 64-bit blocks
B) Pi (π); 128-bit blocks
C) Euler's number (e); 128-bit blocks
D) Pi (π); 64-bit blocks

---

**Q16.** A developer stores user passwords using SHA-256 with a unique random salt per user, but applies only a single hash iteration. An attacker who steals the database can still crack most passwords quickly using GPU clusters, since SHA-256 is designed to compute very fast. Which change BEST addresses the brute-force speed problem while keeping the existing salt's protection against precomputed rainbow tables?

A) Replace the single SHA-256 hash with PBKDF2 using a high iteration count (600,000+) and the existing salt
B) Hash the password twice with SHA-256, i.e., SHA-256(SHA-256(password || salt))
C) Remove the salt and switch to MD5 for faster verification
D) Encrypt the stored hash using AES in ECB mode

---

**Q17.** A company is redesigning its TLS handshake process and requires that a compromise of the server's long-term private key in the future must NOT allow an attacker to decrypt previously captured session traffic. Which key exchange method should be used?

A) RSA key transport, where the client encrypts a pre-master secret with the server's public key
B) Diffie-Hellman Ephemeral (DHE) or ECDHE, generating new key pairs for each session
C) Static Diffie-Hellman using a fixed server key pair for all sessions
D) AES key wrapping of a session key using a pre-shared master key

---

**Q18.** During RSA key pair generation, an engineer must select the public exponent e. Which value is the standard choice used in practice to balance encryption performance with resistance to low-exponent attacks?

A) e = 3
B) e = 17
C) e = 65537
D) e = 65536 (2^16)

---

**Q19.** For an RSA modulus n = p * q where p = 7 and q = 11, what is Euler's totient value φ(n) used to compute the private exponent d?

A) 66
B) 60
C) 70
D) 77

---

**Q20.** A cryptography team is evaluating hash function output sizes and their resistance to collision attacks. For an n-bit hash function, approximately how many hash computations are required to find a collision with 50% probability using a birthday attack?

A) 2^n
B) 2^(n/2)
C) n^2
D) 2^(n-1)

---

**Q21.** A developer needs an asymmetric encryption scheme based on the discrete logarithm problem that incorporates a fresh random value into every encryption operation, producing a ciphertext (c1, c2) roughly twice the size of the plaintext and ensuring the same plaintext never produces the same ciphertext twice. Which algorithm matches this description?

A) RSA
B) ElGamal
C) DSA
D) Diffie-Hellman

---

**Q22.** A security architect wants to replace RSA-3072 with an elliptic curve algorithm that provides an equivalent security level while significantly reducing key size and computational overhead. Which ECC key size should be selected?

A) ECC-160
B) ECC-521
C) ECC-256
D) ECC-1024

---

**Q23.** A company is deploying battery-powered IoT sensors that must authenticate to a cloud gateway using asymmetric cryptography. The security team requires strength equivalent to 3072-bit RSA but needs the smallest possible key size and lowest computational overhead to preserve battery life. Which option BEST meets these requirements?

A) ECC using a 256-bit key
B) RSA with a 3072-bit key
C) DSA with a 3072-bit key
D) Diffie-Hellman with a 3072-bit key

---

**Q24.** Which asymmetric algorithm is standardized specifically for creating digital signatures (not for encrypting data), and relies on the difficulty of computing discrete logarithms in a finite field?

A) DSA
B) RSA
C) ECC
D) ElGamal

---

**Q25.** For an RSA key pair, the two chosen primes are p=13 and q=17. What is the value of Euler's totient φ(n) used to compute the private exponent d?

A) 192
B) 221
C) 208
D) 204

---

**Q26.** A cryptographer explains that the birthday problem is directly relevant to hash function security. What specific security limitation does it describe?

A) It limits collision resistance to roughly 2^(n/2) operations instead of 2^n, for an n-bit hash output.
B) It shows that key exchange protocols leak the shared secret after a predictable number of sessions.
C) It proves that digital signature verification fails once more than 2^n messages have been signed.
D) It demonstrates that prime factorization becomes easier as more primes of similar size are generated.

---

**Q27.** A company must ensure that a signed contract cannot later be denied by the signer, and any modification to the document must be detectable. Which mechanism BEST provides this?

A) HMAC computed with a shared secret key
B) Digital signature created with the signer's private key over the document hash
C) Symmetric encryption of the document with AES-256
D) SHA-256 hash of the document sent alongside it

---

**Q28.** In the Kerberos authentication protocol, what does a client present to the Ticket Granting Service (TGS) to obtain a service ticket?

A) Its long-term password hash directly
B) A ticket-granting ticket (TGT) issued by the Authentication Server (AS)
C) A self-signed X.509 certificate
D) A CHAP challenge response

---

**Q29.** Which X.509 v3 certificate extension must be set to 'CA:TRUE' for a certificate to legally issue and sign other certificates as a Certificate Authority?

A) Key Usage
B) Extended Key Usage
C) Subject Alternative Name
D) Basic Constraints

---

**Q30.** An enterprise Wi-Fi network currently uses WPA2-PSK and is vulnerable to offline dictionary attacks against captured 4-way handshakes. Which upgrade BEST mitigates this specific weakness?

A) Switch to WEP with a longer key
B) Increase the PSK rotation frequency to daily
C) Enable WPA3-Personal using SAE (Simultaneous Authentication of Equals)
D) Disable SSID broadcast

---

**Q31.** A site-to-site VPN gateway needs to encrypt entire original IP packets, including headers, for traffic between two branch office networks. Which IPsec mode should be configured?

A) Transport mode
B) AH in transport mode
C) Tunnel mode
D) ESP in authentication-only mode

---

**Q32.** What is the fundamental difference between steganography and encryption as applied to protecting a message?

A) Encryption hides the existence of data, while steganography scrambles readable content
B) Steganography and encryption are functionally identical processes
C) Steganography hides the existence of the message, while encryption hides the content of a visible message
D) Steganography is always weaker than encryption because it uses no algorithm

---

**Q33.** A company wants a single sign-on solution where a client authenticates once with a Key Distribution Center (KDC) and receives a Ticket Granting Ticket (TGT), then uses that ticket to request service tickets for other systems without re-entering credentials. Which authentication protocol BEST meets this requirement?

A) Kerberos
B) Password Authentication Protocol (PAP)
C) Challenge Handshake Authentication Protocol (CHAP)
D) Extensible Authentication Protocol with TLS (EAP-TLS)

---

**Q34.** An organization is upgrading its wireless network to defend against offline dictionary attacks on the pre-shared key exchange that were possible with WPA2's four-way handshake. Which WPA3 feature directly replaces that vulnerable handshake?

A) Simultaneous Authentication of Equals (SAE)
B) Temporal Key Integrity Protocol (TKIP)
C) Pre-Shared Key (PSK) with AES-CCMP
D) Wired Equivalent Privacy (WEP) with RC4

---

**Q35.** Two branch offices need a site-to-site VPN where traffic between their internal networks is fully encrypted, including the original IP headers, and new IP headers are added for routing between the gateway devices. Which IPsec mode should be configured?

A) Transport mode
B) Quick mode
C) Aggressive mode
D) Tunnel mode

---

**Q36.** A security administrator enables full-disk encryption on company laptops and wants the volume master key sealed to specific boot measurements so the key is released only if the boot process has not been tampered with. Which hardware component does BitLocker rely on to achieve this?

A) Trusted Platform Module (TPM)
B) Hardware Security Module (HSM)
C) Smart card reader
D) Encrypting File System (EFS) driver

---

**Q37.** An application needs to verify in near real time whether a specific X.509 certificate has been revoked, without downloading and parsing a potentially large revocation list. Which mechanism BEST meets this requirement?

A) Certificate Revocation List (CRL)
B) Certificate Transparency (CT) log
C) Certificate pinning
D) Online Certificate Status Protocol (OCSP)

---

**Q38.** An analyst intercepts ciphertext produced by a Vigenère cipher and suspects the key is short and repeating. Which technique should be used to determine the length of the repeating key by locating repeated sequences in the ciphertext and measuring the distances between them?

A) Kasiski examination
B) Birthday attack
C) Differential cryptanalysis
D) Rainbow table lookup

---

**Q39.** A penetration tester obtains a database of password hashes and attempts to crack them using a precomputed rainbow table, but the attack fails to recover any passwords despite the hashes being generated from weak, common passwords. Which password storage practice BEST explains this failure?

A) Passwords were stored in plaintext with strict access controls
B) Passwords were hashed with unsalted MD5
C) Passwords were hashed with a unique random salt per user
D) Passwords were encrypted using AES-256 in CBC mode

---

**Q40.** Which cryptanalysis technique examines pairs of plaintexts with a specific, chosen input difference (XOR difference) and statistically analyzes how that difference propagates through the rounds of a block cipher to recover key bits?

A) Differential cryptanalysis
B) Linear cryptanalysis
C) Frequency analysis
D) Kasiski examination

---

**Q41.** A cryptanalyst measures the exact execution time of an RSA implementation performing decryption on many different ciphertexts, seeking to infer private key bits from variations in processing time caused by modular exponentiation operations. This is an example of which type of attack?

A) Meet-in-the-middle attack
B) Timing attack (side-channel)
C) Chosen-ciphertext attack
D) Birthday attack

---

**Q42.** An analyst has ciphertext generated by a simple monoalphabetic substitution cipher applied to standard English plaintext. Which cryptanalysis approach is MOST effective for breaking this cipher?

A) Differential cryptanalysis
B) Linear cryptanalysis
C) Frequency analysis of letter occurrence
D) Kasiski examination

---

**Q43.** A financial institution wants to migrate its TLS key exchange mechanism to resist attacks from a future large-scale quantum computer capable of running Shor's algorithm. Which solution BEST meets this requirement?

A) Replace RSA key exchange with ML-KEM (Kyber), a lattice-based key encapsulation mechanism
B) Continue using RSA for key exchange but increase the key size to RSA-4096
C) Replace RSA with ECDH using a larger curve such as P-521
D) Use AES-256 in place of RSA for the key exchange step

---

**Q44.** An engineer needs to select the NIST-standardized post-quantum digital signature algorithm that is lattice-based and designated as the primary general-purpose signature scheme for signing firmware updates. Which algorithm should be selected?

A) ML-KEM (Kyber)
B) SPHINCS+
C) RSA-PSS
D) ML-DSA (Dilithium)

---

**Q45.** How does Grover's algorithm affect the security of symmetric encryption algorithms such as AES?

A) It completely breaks AES in polynomial time regardless of key size, similar to how Shor's algorithm breaks RSA
B) It has no impact on symmetric algorithms since Grover's algorithm only targets asymmetric cryptography
C) It converts symmetric ciphers into asymmetric ciphers, requiring a completely different key management model
D) It provides a quadratic speedup for brute-force key search, effectively halving the security bits of a symmetric key

---

**Q46.** A government agency wants to establish a key exchange channel where any eavesdropping attempt is physically detectable due to the laws of quantum mechanics. Which technology should be implemented?

A) Diffie-Hellman key exchange over TLS 1.3
B) Quantum Key Distribution (QKD) using a protocol such as BB84
C) ML-KEM key encapsulation mechanism
D) Elliptic Curve Diffie-Hellman (ECDH)

---

