## Chapter 7: Digital Signatures, X.509 Certificates, and PKI — Practice Questions

**Q1.** A user wants to digitally sign a 50MB file before sending it over email. Which BEST describes the correct order of operations?

A) Encrypt the file with the recipient's public key, then hash the ciphertext with the sender's private key
B) Encrypt the file with the sender's private key, then hash the ciphertext with the recipient's public key
C) Hash the file with a cryptographic hash function, then encrypt the hash with the sender's private key
D) Hash the file, then encrypt the hash with the recipient's public key

<details>
<summary>Answer</summary>

**Correct: C**

Signing = hash the data first, then encrypt (sign) the hash with the SENDER'S private key. The verifier decrypts with the sender's public key to confirm authenticity and integrity.

**Why the others are wrong:**
- Hashing ciphertext instead of plaintext, and using the wrong keys, breaks the ability to prove the signature is tied to the original message.
- Encrypting the whole large file with the private key for 'signing' is not standard practice and is inefficient; hashing the ciphertext afterward makes no sense.
- Encrypting with the recipient's public key provides confidentiality, not authentication — anyone could technically produce it since the recipient's public key isn't secret, so it proves nothing about the sender's identity.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A bank's PKI team needs near real-time certificate revocation checking with minimal impact on TLS handshake latency for millions of connections per day. Which approach BEST meets this requirement?

A) Publish and distribute CRLs every 24 hours
B) Query the CA's OCSP responder directly on every client connection
C) Configure OCSP stapling on the web server
D) Require clients to download the full CRL on every connection

<details>
<summary>Answer</summary>

**Correct: C**

OCSP stapling lets the server pre-fetch a signed, timestamped OCSP response from the CA and attach ('staple') it to the TLS handshake, eliminating the client's separate round trip to the CA while keeping status current.

**Why the others are wrong:**
- 24-hour CRL updates are not real-time; a revoked cert could remain trusted for up to a day.
- Direct client-to-OCSP-responder queries add a round trip per connection at scale and leak client browsing patterns to the CA — worse for latency and privacy.
- Downloading the full CRL on every connection adds significant bandwidth and latency overhead.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An analyst examines an X.509 certificate and needs to determine which Certificate Authority vouched for the certificate's public key. Which field should the analyst check?

A) Subject
B) Validity Period
C) Public Key
D) Issuer

<details>
<summary>Answer</summary>

**Correct: D**

The Issuer field identifies the CA that signed the certificate, i.e., the entity vouching for the binding of identity to public key.

**Why the others are wrong:**
- Subject identifies the entity the certificate was issued TO, not the issuing CA.
- Validity Period only shows the not-before/not-after dates, not identity information.
- Public Key belongs to the Subject, not the issuing CA.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A field technician's laptop must verify certificate revocation status for devices on an air-gapped network with no internet access. Which method BEST supports this requirement?

A) OCSP responder query
B) Locally cached CRL, periodically updated via sneakernet
C) OCSP stapling
D) Online Certificate Status Protocol over VPN

<details>
<summary>Answer</summary>

**Correct: B**

A CRL is a downloadable file that can be manually transferred (sneakernet) and checked entirely offline, making it suitable for air-gapped environments.

**Why the others are wrong:**
- Standard OCSP requires a live network query to the CA's responder, which is impossible on an air-gapped network.
- OCSP stapling still depends on the server periodically fetching a fresh signed response online; it is not designed for fully disconnected verification.
- OCSP over VPN still requires network connectivity, which contradicts the air-gapped constraint.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which hash algorithm should be selected when generating a digital signature under current security best practices in 2026?

A) MD5
B) SHA-256
C) SHA-1
D) CRC32

<details>
<summary>Answer</summary>

**Correct: B**

SHA-256 (SHA-2 family) is the current recommended hash for signatures, offering strong collision resistance.

**Why the others are wrong:**
- MD5 is cryptographically broken with demonstrated collision attacks and must never be used for signatures.
- SHA-1 has been deprecated for certificate and signature use since 2017 due to practical collision attacks.
- CRC32 is a simple error-detection checksum with no cryptographic security properties, not a cryptographic hash.

</details>

---

**Q6.** Which X.509 certificate field contains the CA's digital signature that binds the subject's identity to the public key?

A) Serial Number
B) Signature Algorithm / Signature Value
C) Subject Alternative Name
D) Key Usage

<details>
<summary>Answer</summary>

**Correct: B**

The Signature field is computed by the CA over the rest of the certificate (tbsCertificate) using the CA's private key — this is what proves the CA vouched for the identity-to-key binding.

**Why the others are wrong:**
- Serial Number only uniquely identifies the certificate within the issuing CA; it is not a signature.
- Subject Alternative Name lists additional identities/domains covered by the cert, unrelated to the CA's signature.
- Key Usage defines the permitted operations for the SUBJECT's key (e.g., digitalSignature, keyEncipherment) — it is often confused with the CA's own signature over the certificate but is a different field.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A certificate's 'Not After' field shows a date that has already passed. During TLS handshake validation, how should a client treat this certificate?

A) Reject it as expired regardless of CRL/OCSP status
B) Accept it if the Issuer is trusted
C) Accept it only if OCSP reports 'good'
D) Prompt the CA to reissue automatically

<details>
<summary>Answer</summary>

**Correct: A**

Expiration is checked independently of revocation. An expired certificate must be rejected even if it was never revoked.

**Why the others are wrong:**
- A trusted Issuer does not override the independent expiration check.
- A 'good' OCSP response only confirms non-revocation; it does not extend or override the certificate's expiration date.
- There is no automatic client-triggered reissuance process during handshake validation.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement BEST distinguishes a Root CA from an Intermediate CA in a PKI hierarchy?

A) Root CA certificates are always short-lived; intermediate CA certificates are long-lived
B) The Root CA is self-signed and forms the trust anchor; the Intermediate CA is signed by the Root (or another intermediate) and issues end-entity certificates
C) Intermediate CAs can issue Root CA certificates but not end-entity certificates
D) Root CAs and Intermediate CAs are functionally identical, differing only in naming

<details>
<summary>Answer</summary>

**Correct: B**

The Root CA is self-signed and serves as the trust anchor, typically kept offline for security. Intermediate CAs chain up to the root and handle day-to-day certificate issuance, limiting exposure of the root's private key.

**Why the others are wrong:**
- This is reversed — Root CA certificates typically have very long validity periods (often decades) and are kept offline; intermediates rotate more frequently.
- This reverses the actual relationship — intermediates cannot issue root certificates.
- They differ meaningfully: the root is the ultimate trust anchor with restricted usage, while intermediates perform routine issuance to reduce root key risk.

</details>

---

