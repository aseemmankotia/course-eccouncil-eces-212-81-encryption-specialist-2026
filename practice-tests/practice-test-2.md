# Practice Test 2: ECES 212-81: Applied Cryptography Exam Prep

- **Questions:** 46
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A cryptanalyst examining ciphertext from a polyalphabetic substitution cipher finds identical three-letter sequences reappearing at intervals of 6, 9, and 12 characters throughout the message. Which classical cryptanalysis technique should be applied next, and what does it reveal?

A) Frequency analysis - reveals the plaintext language distribution
B) Index of coincidence on a monoalphabetic shift - reveals the shift value
C) Kasiski examination - determines the probable key length by finding the GCD of the repeat distances
D) Rail fence depth analysis - reveals the number of transposition rails

---

**Q2.** A WWI field commander needs to encrypt messages using a fractionating cipher that first converts plaintext into letter pairs drawn from a 6x6 grid containing the 26 letters plus 10 digits (using only A, D, F, G, V, X as coordinate labels), and then applies a columnar transposition to the resulting fractionated text. Which cipher is being described?

A) ADFGVX cipher - uses a 6x6 grid including digits, followed by columnar transposition
B) ADFGX cipher - uses a 5x5 grid without digits
C) Playfair cipher - encrypts digraphs using a 5x5 grid without transposition
D) Vigenere cipher - uses a repeating keyword for polyalphabetic substitution

---

**Q3.** An Enigma I machine is set up with three rotors, a reflector, and a plugboard with 10 cable pairs connected. Which component is responsible for guaranteeing that the Enigma cipher can never encrypt a letter to itself?

A) The plugboard - swaps letter pairs before the signal enters the rotors
B) The rotor stepping mechanism - advances one or more rotors after each keypress
C) The reflector - sends the current back through the rotors using fixed, non-identity wiring
D) The ring settings - offset the internal wiring position relative to the rotor contacts

---

**Q4.** A user digitally signs and sends a contract. The recipient can later prove that the specific sender created and transmitted that exact contract, and the sender cannot credibly deny having done so. Which cryptographic goal is being provided beyond basic authentication?

A) Confidentiality - ensures only authorized parties can read the contract
B) Integrity - ensures the contract was not altered in transit
C) Availability - ensures the contract remains accessible over time
D) Non-repudiation - ensures the sender cannot deny having signed and sent the message

---

**Q5.** When encrypting the plaintext 'BALLOON' with a classic Playfair cipher, the digraph pairing process encounters the repeated letter pair 'LL' occurring consecutively. What is the standard classical technique used to handle this situation?

A) Skip the second repeated letter and treat the pair as a single character
B) Insert a filler letter, such as X, between the repeated letters to break up the digraph
C) Apply Atbash substitution to the repeated letters prior to encryption
D) Merge the repeated letters into a single homophonic symbol

---

**Q6.** A streaming video service encrypts video segments so that any client can seek to an arbitrary point in the stream and decrypt only the segment it needs, without decrypting or even receiving any preceding segments. Which block cipher mode of operation BEST supports this requirement?

A) OFB (Output Feedback) mode, since it generates a continuous keystream
B) CBC (Cipher Block Chaining) mode, since ciphertext blocks are chained together
C) CFB (Cipher Feedback) mode, since it feeds ciphertext back into the cipher
D) CTR (Counter) mode, since each keystream block is computed independently from a counter value

---

**Q7.** DES has a small set of keys for which the key schedule generates the identical 48-bit round subkey for all 16 rounds, meaning encryption with such a key is its own inverse. How many of these 'weak keys' exist among DES's key space?

A) 64
B) 12
C) 256
D) 4

---

**Q8.** The AES (Rijndael) S-box provides strong resistance to differential and linear cryptanalysis primarily because it is constructed by combining which two mathematical operations over GF(2^8)?

A) Multiplicative inverse in GF(2^8) followed by an affine transformation
B) Left circular bit rotation followed by a substitution lookup borrowed from DES
C) Modular exponentiation followed by a Feistel-style swap of nibbles
D) XOR with a fixed round key followed by a simple byte permutation

---

**Q9.** A developer must derive a strong 256-bit encryption key from a user-supplied passphrase, and the derivation process must be deliberately slow and tunable to resist brute-force and dictionary attacks. Which construction is designed for this purpose?

A) RC4 keystream generator seeded with the passphrase
B) A single application of SHA-256 to the passphrase
C) PBKDF2 with a salt and a high iteration count
D) HMAC-SHA1 computed once over the passphrase

---

**Q10.** Per current OWASP password storage guidance, when PBKDF2-HMAC-SHA256 is used for password hashing, what is the minimum recommended iteration count?

A) 1,000
B) 600,000
C) 65,536
D) 10,000

---

**Q11.** WEP encrypts wireless frames using RC4 with a 24-bit initialization vector (IV) prepended to a static key. Researchers demonstrated the Fluhrer-Mantin-Shamir (FMS) attack, allowing full key recovery after capturing enough frames. Which weakness in RC4 made this attack possible?

A) RC4's S-box is generated using a reversible DES Feistel structure
B) RC4 requires a fixed 64-bit key, making exhaustive search feasible within a minute
C) RC4 uses a 128-bit block size vulnerable to birthday-bound collisions
D) RC4's Key Scheduling Algorithm produces keystream bytes that are statistically correlated with the key for certain 'weak' IV values

---

**Q12.** A satellite communication system experiences frequent single-bit transmission errors and must support decrypting out-of-order packets in parallel (no sequential dependency between blocks). Which block cipher mode BEST satisfies both requirements?

A) OFB (Output Feedback)
B) CTR (Counter Mode)
C) CFB (Cipher Feedback)
D) CBC (Cipher Block Chaining)

---

**Q13.** The AES (Rijndael) S-box substitution values are generated by applying which two-step mathematical process to each input byte?

A) Multiplicative inverse in GF(2^8) followed by an affine transformation
B) A fixed permutation lookup table copied from DES's S-boxes
C) XOR of the byte with the round key only, with no further transformation
D) Two sequential applications of the Feistel round function

---

**Q14.** During Blowfish's key-expansion (key schedule) process, the 18 subkeys of the P-array and the four 256-entry S-boxes are initialized with a fixed value before being XORed with the cipher key. What is that initial value derived from?

A) The ASCII bytes of the string 'BLOWFISH'
B) An MD5 hash of the supplied key
C) An all-zero 4096-bit table
D) The hexadecimal digits of pi

---

**Q15.** In the HMAC construction, what hexadecimal byte values are used to build the inner padding (ipad) and outer padding (opad) constants applied to the key before hashing?

A) ipad = 0x36, opad = 0x5C
B) ipad = 0x5C, opad = 0x36
C) ipad = 0xFF, opad = 0x00
D) ipad = 0x0F, opad = 0xF0

---

**Q16.** The Whirlpool hash function's internal compression function is structurally based on which cipher design, and what is its resulting digest length?

A) A DES-based design producing a 128-bit digest
B) An AES-based design producing a 512-bit digest
C) An RC6-based design producing a 256-bit digest
D) A Blowfish-based design producing a 160-bit digest

---

**Q17.** During RSA key generation you select primes p=13 and q=17. What is φ(n), the value used to compute the private exponent d?

A) 192
B) 221
C) 208
D) 156

---

**Q18.** You are generating an RSA key pair where φ(n) = 112. Which of the following values is a valid choice for the public exponent e (must satisfy 1 < e < φ(n) and gcd(e, φ(n)) = 1)?

A) 8
B) 3
C) 14
D) 4

---

**Q19.** The security of the Diffie-Hellman key exchange protocol against passive eavesdroppers is based on the presumed intractability of which mathematical problem?

A) The subset sum problem
B) The discrete logarithm problem
C) The shortest vector problem in a lattice
D) Integer factorization of large composite numbers

---

**Q20.** An attacker mounts a birthday attack against a hash function with a 128-bit output size. Approximately how many random hash computations are needed before there is roughly a 50% chance of finding a collision?

A) 2^32
B) 2^64
C) 2^256
D) 2^128

---

**Q21.** Per NIST key-strength equivalence guidance referenced in encryption specialist material, which ECC key size provides security roughly equivalent to a 3072-bit RSA key?

A) 256-bit ECC
B) 160-bit ECC
C) 384-bit ECC
D) 224-bit ECC

---

**Q22.** How does the Cramer-Shoup cryptosystem improve upon the classic ElGamal encryption scheme?

A) It replaces modular exponentiation with elliptic curve point multiplication for smaller keys
B) It removes the need for a random ephemeral key per encryption
C) It provides perfect forward secrecy by rotating the private key after each session
D) It adds a hash-based verification component to achieve IND-CCA2 security against adaptive chosen-ciphertext attacks

---

**Q23.** During RSA key generation, a candidate selects primes p=61 and q=53, computes n=3233, and chooses public exponent e=17. What is the corresponding private exponent d, satisfying e*d ≡ 1 (mod φ(n))?

A) 2789
B) 3009
C) 2753
D) 2621

---

**Q24.** A cryptographer needs an asymmetric encryption scheme that is provably secure against adaptive chosen-ciphertext attacks (IND-CCA2) in the standard model, extending the basic discrete-logarithm-based ElGamal construction with an additional hash-based integrity check. Which algorithm should be selected?

A) ElGamal
B) RSA-OAEP
C) DSA
D) Cramer-Shoup

---

**Q25.** A system uses a hash function producing a 128-bit digest. Applying the birthday bound, approximately how many random inputs must be hashed before there is a 50% probability that two of them collide?

A) 2^128
B) 2^32
C) 2^64
D) 2^256

---

**Q26.** According to NIST SP 800-57 key-strength equivalence guidance, a 256-bit ECC key provides a security level roughly comparable to which RSA modulus size?

A) 3072
B) 2048
C) 4096
D) 1024

---

**Q27.** A company connects two branch offices over an IPsec VPN. The tunnel must traverse a NAT device between the sites, and the traffic must be both encrypted and authenticated. Which IPsec protocol should be selected, and why?

A) AH, because it authenticates the entire IP packet including the header, guaranteeing NAT compatibility
B) AH in transport mode, because it encrypts the payload while leaving the header untouched
C) ESP, because it encrypts and can authenticate the payload without authenticating the outer IP header, making it NAT-traversal friendly
D) ESP with NULL encryption, because encryption is unnecessary when NAT is present

---

**Q28.** In a Kerberos authentication exchange, after the client receives a Ticket Granting Ticket (TGT) from the Authentication Server, what does the client send to the Ticket Granting Service (TGS) to obtain a service ticket?

A) The TGT along with an authenticator encrypted using the session key shared with the KDC
B) The user's plaintext password for re-verification
C) A newly generated AS-REQ message identical to the first request
D) The target service's X.509 certificate for mutual authentication

---

**Q29.** WPA3's Simultaneous Authentication of Equals (SAE) is considered resistant to offline dictionary attacks that plague WPA2-PSK's 4-way handshake. What is the primary reason for this resistance?

A) SAE requires passphrases to be at least 63 characters long
B) SAE encrypts the SSID broadcast so attackers cannot identify the network
C) SAE performs an interactive Diffie-Hellman-style key exchange with the access point, so each password guess requires a live exchange, preventing captured-handshake offline cracking
D) SAE eliminates the need for a shared passphrase entirely by using certificates

---

**Q30.** An organization's root CA certificate must be able to issue certificates to subordinate (intermediate) CAs, which in turn issue end-entity certificates. Which X.509 v3 extension and setting enables this delegation of CA authority?

A) Basic Constraints extension with CA=TRUE and an appropriate pathLenConstraint
B) Extended Key Usage set to serverAuth
C) Subject Alternative Name listing the subordinate CA's DNS name
D) Key Usage extension set to keyEncipherment only

---

**Q31.** TLS 1.3 removed several legacy key exchange options present in TLS 1.2. Which key exchange mechanism does TLS 1.3 mandate for its standard full handshake to guarantee forward secrecy?

A) Static RSA key transport
B) Kerberos-based ticket exchange
C) PSK-only mode with no key exchange, using a permanently cached session key
D) (EC)DHE — ephemeral Diffie-Hellman or elliptic-curve Diffie-Hellman

---

**Q32.** A forensic analyst examines a VeraCrypt-encrypted container. The container contains a hidden volume nested inside an outer decoy volume, and there is no cryptographic or structural evidence indicating the hidden volume exists without the correct hidden-volume password. This capability is best classified as an example of:

A) Plausible deniability achieved through a steganographic hidden-volume technique
B) One-way hashing to preserve data integrity
C) Digital watermarking for copyright enforcement
D) Asymmetric key wrapping using a public/private key pair

---

**Q33.** A network engineer is designing an IPsec VPN tunnel for a healthcare company that must guarantee patient records remain confidential in transit, in addition to integrity and origin authentication. Which IPsec protocol component MUST be included in the Security Association to meet the confidentiality requirement?

A) Encapsulating Security Payload (ESP), since it provides payload encryption plus optional authentication
B) Authentication Header (AH) alone, since it provides encryption of the entire packet
C) Internet Key Exchange (IKE) Phase 1 alone, since key negotiation itself encrypts the data
D) AH combined with a manual pre-shared key, since PSK adds encryption to AH

---

**Q34.** During Kerberos authentication, a user's workstation successfully authenticates to the KDC and needs to access a file server. Which exact ticket does the client present to the Ticket Granting Service (TGS) to request a service ticket for the file server?

A) The service ticket (ST) issued previously for the same file server
B) The Ticket Granting Ticket (TGT) obtained from the Authentication Service (AS)
C) The user's plaintext password hash, re-sent for TGS verification
D) The KDC's own long-term secret key, shared during initial enrollment

---

**Q35.** A wireless security auditor demonstrates the KRACK (Key Reinstallation Attack) against a legacy access point by forcing nonce reuse during the WPA2 four-way handshake, allowing partial keystream recovery. Which WPA3 mechanism specifically eliminates this class of handshake vulnerability?

A) Replacing the four-way PSK handshake with Simultaneous Authentication of Equals (SAE)
B) Increasing the PSK length requirement to 63 characters minimum
C) Switching the encryption cipher from AES-CCMP to AES-GCMP only
D) Mandating WPS PIN-based pairing instead of PSK entry

---

**Q36.** An organization's PKI team needs certificate status checks to return within milliseconds for a high-volume TLS-terminating load balancer, without downloading and caching a large periodically-updated revocation list. Which revocation-checking mechanism BEST fits this requirement?

A) Certificate Revocation List (CRL) fetched fresh on every single TLS handshake
B) Certificate Transparency (CT) log inclusion proof validation
C) Online Certificate Status Protocol (OCSP), queried per-certificate in near real time
D) Key Usage extension inspection embedded directly in the certificate

---

**Q37.** A laptop protected with BitLocker is stolen while powered off. The attacker removes the drive and attempts to read it from another machine, and separately attempts to tamper with the boot loader to bypass authentication on the original machine. Which underlying hardware mechanism is responsible for BOTH sealing the volume encryption key to a trusted boot state AND detecting the boot loader tampering attempt?

A) A hardware security module (HSM) issued by the domain's certificate authority
B) The drive's onboard AES-NI encryption accelerator chip
C) A software-based Secure Boot flag stored in the Windows registry
D) The Trusted Platform Module (TPM), which seals the key to measured PCR values

---

**Q38.** A Vigenère ciphertext analysis reveals three repeated three-letter sequences occurring at ciphertext offsets of 12, 18, and 24 characters apart. Using Kasiski examination, what is the most probable key length?

A) 4
B) 8
C) 6
D) 12

---

**Q39.** An attacker selects pairs of plaintexts that differ by a fixed XOR value and encrypts both through a block cipher, then studies how that input difference propagates to produce non-uniform output differences, ultimately recovering key bits from the most probable differential characteristic. Which cryptanalysis technique is being performed?

A) Linear cryptanalysis
B) Integral cryptanalysis
C) Meet-in-the-middle attack
D) Differential cryptanalysis

---

**Q40.** A security team stores password hashes without any per-user randomization and discovers that precomputed rainbow tables can recover most passwords in seconds. Which single change to the hashing process BEST defeats rainbow table attacks?

A) Increase the hash output length
B) Apply a unique salt to each password before hashing
C) Switch from SHA-1 to SHA-256 with no other changes
D) Encrypt the hash output with AES

---

**Q41.** A hardware security module implements RSA decryption using square-and-multiply modular exponentiation whose execution time varies depending on whether each private key bit is 0 or 1. An attacker who measures decryption latency across many operations to recover the private key is exploiting which category of attack?

A) Chosen-ciphertext attack
B) Timing side-channel attack
C) Differential cryptanalysis
D) Birthday attack

---

**Q42.** Which cryptanalytic technique encrypts a structured set of plaintexts in which one byte position takes all 256 possible values while all other bytes remain fixed, then analyzes the XOR sum of the resulting ciphertexts to detect balanced or non-balanced properties after a reduced number of rounds?

A) Linear cryptanalysis
B) Integral cryptanalysis
C) Kasiski examination
D) Differential cryptanalysis

---

**Q43.** A financial institution encrypts data at rest with AES-256 and is preparing a quantum-readiness roadmap. Their security architect is concerned specifically about Grover's algorithm running on a future large-scale quantum computer. Which action BEST reflects the actual impact of Grover's algorithm on this symmetric cipher?

A) Immediately downgrade to AES-128 since Grover halves the effective key strength anyway, so the smaller key saves performance
B) No key-size change is required for AES-256, since Grover's quadratic speedup reduces its effective security to roughly 128 bits, which remains an adequate margin
C) Migrate all AES-256 usage to RSA-4096, since RSA is inherently more quantum-resistant than symmetric ciphers
D) Replace AES-256 with ECC-256, since elliptic curve algorithms are unaffected by Grover's algorithm

---

**Q44.** A protocol designer needs to select a NIST-standardized algorithm specifically to establish a shared secret key between two parties over an insecure channel, with resistance to attacks from a cryptographically relevant quantum computer. Which algorithm should be selected?

A) ML-DSA (Dilithium)
B) SPHINCS+
C) ML-KEM (Kyber)
D) FALCON

---

**Q45.** During a BB84 quantum key distribution session, Alice and Bob compare a random subset of their sifted key bits (bits where they used matching measurement bases) to check for eavesdropping. Which observation would indicate that an eavesdropper (Eve) has intercepted and measured the photons?

A) A high number of basis mismatches between Alice's sending basis and Bob's measuring basis
B) Bob detects photons using entangled pairs instead of single photons
C) The polarization angle of received photons differs from 0 or 90 degrees
D) A quantum bit error rate significantly higher than the expected baseline noise level in the compared subset

---

**Q46.** An exam question asks you to correctly distinguish the cryptographic impact of Shor's algorithm from that of Grover's algorithm. Which statement correctly characterizes the two?

A) Shor's algorithm gives a quadratic speedup against symmetric ciphers; Grover's algorithm gives an exponential speedup that fully breaks RSA and ECC
B) Both algorithms provide the same exponential speedup, but Shor targets hash functions while Grover targets public-key algorithms
C) Shor's algorithm gives an exponential speedup that breaks RSA, Diffie-Hellman, and ECC by efficiently solving integer factorization and discrete logarithm problems; Grover's algorithm gives only a quadratic speedup useful against symmetric ciphers and hash functions
D) Shor's algorithm only threatens hash-based signature schemes like SPHINCS+, while Grover's algorithm threatens lattice-based schemes like Kyber

---

