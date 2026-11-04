## Chapter 8: SSL/TLS Handshakes and Authentication Protocols — Practice Questions

**Q1.** A company's RADIUS server must authenticate remote dial-up users without ever transmitting the password in plaintext, and must protect against replay attacks by issuing a new challenge value periodically throughout the session. Which protocol should be used?

A) PAP
B) EAP-TLS
C) CHAP
D) Kerberos

<details>
<summary>Answer</summary>

**Correct: C**

CHAP (RFC 1994) never sends the password itself — it sends a hash of the challenge and shared secret — and re-issues challenges periodically during the session, defeating replay.

**Why the others are wrong:**
- PAP sends the username and password in cleartext during a simple 2-way handshake, with no replay protection.
- EAP-TLS is certificate-based mutual authentication typically used for 802.1X wireless/wired networks, not classic dial-up RADIUS challenge-response.
- Kerberos is a ticket-based SSO system using a KDC, not a PPP challenge-response protocol for dial-up links.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A financial services company migrates from TLS 1.2 to TLS 1.3 to reduce handshake latency while ensuring that a compromised private key in the future cannot decrypt previously recorded sessions. Which combination of TLS 1.3 properties provides this?

A) 1-RTT handshake with mandatory ephemeral (EC)DHE key exchange
B) 1-RTT handshake with static RSA key exchange
C) 0-RTT resumption using static RSA
D) 2-RTT handshake with renegotiation enabled

<details>
<summary>Answer</summary>

**Correct: A**

TLS 1.3 completes a full handshake in 1-RTT and mandates ephemeral Diffie-Hellman (ECDHE/DHE) for every session, guaranteeing forward secrecy.

**Why the others are wrong:**
- Static RSA key exchange was removed entirely from TLS 1.3 — it never provides forward secrecy.
- 0-RTT exists in TLS 1.3 for session resumption but static RSA is not a TLS 1.3 key exchange option; 0-RTT also has known replay weaknesses, unrelated to forward secrecy claim.
- TLS 1.2 required 2-RTT and supported renegotiation, which TLS 1.3 removed for security reasons.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A user logs into a Windows domain. After successful authentication, the user requests access to a file server. Which credential does the client present to the Ticket Granting Service (TGS) to obtain a service ticket, without re-entering their password?

A) Plaintext password
B) Ticket Granting Ticket (TGT)
C) NTLM hash
D) PAP session key

<details>
<summary>Answer</summary>

**Correct: B**

After the AS_REQ/AS_REP exchange, the client holds a TGT issued by the KDC's Authentication Server. It presents this TGT (via TGS_REQ) to obtain a service ticket for each resource, without re-entering credentials.

**Why the others are wrong:**
- The password is never transmitted in Kerberos — only a timestamp encrypted with a key derived from the password is sent during initial authentication.
- NTLM hashes belong to the older NTLM authentication protocol, not Kerberos ticket exchange.
- PAP is an unrelated PPP authentication protocol and has no session key concept in Kerberos.

</details>

---

**Q4.** Which EAP method is best suited for a wireless enterprise network requiring mutual authentication via digital certificates on both the client and the server?

A) EAP-MD5
B) EAP-TLS
C) LEAP
D) PAP

<details>
<summary>Answer</summary>

**Correct: B**

EAP-TLS uses X.509 certificates on both client and server, providing strong mutual authentication and is the recommended EAP method for enterprise WPA2/WPA3-Enterprise deployments.

**Why the others are wrong:**
- EAP-MD5 only authenticates the client (one-way) using a weak MD5 challenge and offers no mutual authentication.
- LEAP (Cisco proprietary) has known cryptographic weaknesses and does not use certificate-based mutual auth by default.
- PAP is a PPP protocol, not an EAP method, and transmits credentials in cleartext.

</details>

---

**Q5.** An organization wants single sign-on (SSO) authentication using symmetric-key cryptography and time-stamped tickets to prevent replay, relying on a centralized trusted third party. Which should they deploy?

A) CHAP
B) PAP
C) TLS 1.3
D) Kerberos

<details>
<summary>Answer</summary>

**Correct: D**

Kerberos uses a centralized KDC (trusted third party), symmetric-key cryptography, and timestamped tickets to prevent replay while enabling SSO across multiple services.

**Why the others are wrong:**
- CHAP is a point-to-point challenge-response protocol with no centralized ticketing or SSO capability.
- PAP has no ticketing, no third party, and sends credentials in plaintext.
- TLS 1.3 secures transport channels but is not an SSO ticketing/authentication framework.

</details>

---

**Q6.** During TLS 1.3 cipher suite negotiation, which of the following key exchange components was removed compared to TLS 1.2?

A) AEAD ciphers
B) ECDHE
C) SHA-256 hashing
D) Static RSA key exchange

<details>
<summary>Answer</summary>

**Correct: D**

TLS 1.3 eliminated static RSA key exchange entirely because it provides no forward secrecy; only ephemeral (EC)DHE key exchanges are permitted.

**Why the others are wrong:**
- AEAD ciphers (e.g., AES-GCM, ChaCha20-Poly1305) are required in TLS 1.3, not removed.
- ECDHE is retained and mandated in TLS 1.3 as the primary key exchange mechanism.
- SHA-256 is still used within TLS 1.3 cipher suite naming and HKDF key derivation.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** How many round trips (RTT) does a full handshake require in TLS 1.3 compared to TLS 1.2, under normal (non-0-RTT) conditions?

A) TLS 1.3 requires 2 RTT; TLS 1.2 requires 1 RTT
B) Both require 2 RTT
C) TLS 1.3 requires 1 RTT; TLS 1.2 requires 2 RTT
D) TLS 1.3 requires 0 RTT always; TLS 1.2 requires 1 RTT

<details>
<summary>Answer</summary>

**Correct: C**

TLS 1.3 reduced the full handshake to a single round trip by combining key share and cipher negotiation into the initial ClientHello/ServerHello exchange, versus TLS 1.2's two round trips.

**Why the others are wrong:**
- This reverses the actual relationship — TLS 1.2 is the slower, 2-RTT protocol.
- TLS 1.2 is not equal to TLS 1.3 in round trips; this is the core latency improvement of TLS 1.3.
- 0-RTT is only available on session resumption with a valid PSK, not on every TLS 1.3 handshake.

</details>

---

**Q8.** What is the fundamental difference between PAP and CHAP authentication?

A) PAP uses a challenge-response mechanism; CHAP transmits credentials in plaintext
B) PAP is used only in wireless networks; CHAP is used only in VPNs
C) PAP and CHAP are both extensions of EAP
D) PAP transmits credentials in plaintext; CHAP uses a challenge-response hash mechanism

<details>
<summary>Answer</summary>

**Correct: D**

PAP performs a simple 2-way handshake sending username/password in cleartext. CHAP uses a 3-way challenge-response handshake where the password is never sent, only a hash of the challenge and shared secret.

**Why the others are wrong:**
- This reverses the definitions of PAP and CHAP.
- Neither protocol is restricted to a specific medium — both are PPP-layer authentication protocols usable across various link types.
- PAP and CHAP predate EAP and are standalone PPP authentication protocols, not EAP methods.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

