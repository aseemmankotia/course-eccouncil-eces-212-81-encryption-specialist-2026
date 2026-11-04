## Chapter 9: Wi-Fi Security, VPNs, Disk Encryption, and Steganography — Practice Questions

**Q1.** A company needs to build a site-to-site VPN between two branch office gateways over the public internet. The requirement is that the ENTIRE original IP packet, including headers, must be hidden from anyone sniffing the transit link. Which configuration BEST meets this requirement?

A) IPsec transport mode using AH
B) IPsec transport mode using ESP
C) An SSL VPN operating in transport mode
D) IPsec tunnel mode using ESP

<details>
<summary>Answer</summary>

**Correct: D**

Tunnel mode encapsulates the entire original packet (including the original IP header) inside a new IP packet, and ESP provides confidentiality via encryption plus optional integrity — exactly what gateway-to-gateway VPNs use.

**Why the others are wrong:**
- AH never encrypts payload — it only provides integrity/authentication, so headers and data remain visible.
- Transport mode only encrypts the payload; the original IP header stays exposed, defeating the requirement.
- SSL VPNs don't use IPsec transport/tunnel modes at all, and 'transport mode' isn't an SSL VPN concept.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** During a wireless assessment, an attacker repeatedly retransmits message 3 of the 4-way handshake, forcing the client to reinstall an already-used pairwise transient key and reset its nonce/replay counter to zero. Which attack is being performed?

A) FMS attack against WEP
B) Dragonblood against WPA3
C) Evil Twin access point attack
D) KRACK against WPA2

<details>
<summary>Answer</summary>

**Correct: D**

KRACK (Key Reinstallation Attack) exploits the WPA2 4-way handshake by replaying message 3, forcing nonce/key reuse in CCMP/AES, enabling packet decryption or replay.

**Why the others are wrong:**
- FMS targets WEP's weak RC4 key scheduling via IV collisions, not the handshake process.
- Dragonblood targets side-channel/downgrade flaws in WPA3's SAE (Dragonfly) exchange, not the 4-way handshake reinstallation.
- Evil Twin is a rogue AP impersonation attack, unrelated to handshake nonce reuse.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An enterprise needs whole-disk encryption on Windows laptops with TPM 2.0 chips, managed centrally via Group Policy/Intune, with minimal user interaction. Which solution BEST fits?

A) EFS
B) VeraCrypt
C) BitLocker
D) PGP Whole Disk Encryption

<details>
<summary>Answer</summary>

**Correct: C**

BitLocker is natively integrated with Windows, uses AES-XTS with TPM-sealed keys, and supports centralized management through Group Policy and Intune.

**Why the others are wrong:**
- EFS only encrypts individual files/folders, not the entire volume.
- VeraCrypt is third-party and lacks native GPO/Intune integration for enterprise-wide management.
- PGP WDE isn't natively Windows-integrated and doesn't leverage TPM sealing the way BitLocker does.

</details>

---

**Q4.** A whistleblower needs disk encryption on a laptop that must work across Windows, macOS, and Linux, and must support a hidden volume for plausible deniability if the machine is seized. Which tool BEST meets this need?

A) VeraCrypt
B) BitLocker
C) EFS
D) LUKS

<details>
<summary>Answer</summary>

**Correct: A**

VeraCrypt is cross-platform and explicitly supports hidden volumes and hidden operating systems for plausible deniability.

**Why the others are wrong:**
- BitLocker is Windows-only and has no hidden volume feature.
- EFS is Windows-only, file-level, and has no plausible deniability mechanism.
- LUKS is Linux-only and does not provide the same cross-platform hidden volume capability as VeraCrypt.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** Which pair of UDP ports does IKE use for initial key exchange and for NAT traversal, respectively?

A) 500 and 4500
B) 443 and 8443
C) 500 and 1701
D) 4500 only, no separate port needed

<details>
<summary>Answer</summary>

**Correct: A**

IKE uses UDP 500 for the initial exchange; when NAT is detected, negotiation switches to UDP 4500 (NAT-Traversal) to encapsulate ESP inside UDP.

**Why the others are wrong:**
- 443/8443 are HTTPS-related ports, not IKE.
- 1701 is L2TP's port, not IKE NAT-T.
- 4500 alone is incomplete — 500 is used first before a NAT is detected.

</details>

---

**Q6.** Which statement BEST describes the functional difference between IPsec AH and ESP?

A) AH encrypts data, ESP only authenticates it
B) AH and ESP provide identical services and are interchangeable
C) AH has been fully deprecated and removed from the IPsec standard
D) AH provides integrity and authentication only with no encryption; ESP provides confidentiality plus optional integrity

<details>
<summary>Answer</summary>

**Correct: D**

AH (protocol 51) authenticates the packet and header but never encrypts payload. ESP (protocol 50) encrypts the payload and can optionally provide integrity/authentication too.

**Why the others are wrong:**
- This reverses the actual roles — AH never encrypts.
- They are not interchangeable; only ESP offers confidentiality, which is why ESP is used far more often.
- AH is still defined in RFC 4302 and remains valid, though rarely deployed since it lacks encryption.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A forensic analyst finds an image file with the same dimensions, format, and file size as the original, but the cryptographic hash differs and pixel byte values are altered in patterns limited to the lowest-order bits. What technique was most likely used?

A) LSB steganography
B) Full-disk encryption
C) ESP encapsulation
D) Password salting

<details>
<summary>Answer</summary>

**Correct: A**

Least Significant Bit steganography hides data by altering only the lowest-order bit of each pixel byte, causing imperceptible visual change but a detectable hash/statistical shift.

**Why the others are wrong:**
- Full-disk encryption operates on entire volumes, not individual image pixel bytes.
- ESP is an IPsec transport protocol, unrelated to image file manipulation.
- Salting is a password-hashing technique, irrelevant to image steganography.

</details>

---

**Q8.** In a blockchain, which structure allows a lightweight client to verify that a single transaction was included in a block WITHOUT downloading every transaction in that block?

A) A symmetric session key shared by all nodes
B) A complete hash chain of the entire blockchain history
C) A certificate chain issued by a central certificate authority
D) A Merkle proof derived from the block's Merkle tree

<details>
<summary>Answer</summary>

**Correct: D**

A Merkle tree hashes transactions pairwise up to a single root; a Merkle proof (path of sibling hashes) lets a client verify inclusion in O(log n) hashes without downloading the full block.

**Why the others are wrong:**
- Blockchains have no shared symmetric session key architecture for this purpose.
- Downloading the entire chain defeats the purpose of a lightweight (SPV) client.
- Public blockchains are decentralized and do not rely on a central CA for transaction verification.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

