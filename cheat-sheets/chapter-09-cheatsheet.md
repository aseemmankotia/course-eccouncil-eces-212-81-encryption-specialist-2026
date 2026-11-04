## Wi-Fi Security
| Standard | Cipher | Key Exchange | Known Weakness |
|---|---|---|---|
| WEP | RC4 | Static key + 24-bit IV | IV reuse → FMS/key recovery |
| WPA | RC4 (TKIP) | Per-packet key mixing | Weaker than AES, still exploitable |
| WPA2 | AES-CCMP | 4-way handshake (PSK/802.1X) | KRACK (nonce reuse via handshake replay) |
| WPA3 | AES-GCMP | SAE (Dragonfly) | Dragonblood side-channel/downgrade flaws |

WPA3-Personal = 128-bit SAE. WPA3-Enterprise = 192-bit (CNSA suite).

## IPsec
| Protocol | Number | Confidentiality | Integrity/Auth |
|---|---|---|---|
| AH | 51 | No | Yes |
| ESP | 50 | Yes | Optional |

**Modes:**
- Transport: encrypts payload only, original IP header visible → host-to-host.
- Tunnel: encrypts entire original packet, new IP header added → gateway-to-gateway VPNs.

**IKE ports:** UDP 500 (key exchange), UDP 4500 (NAT-T).

## Full-Disk / File Encryption
| Tool | Scope | Platform | Key Feature |
|---|---|---|---|
| BitLocker | Whole volume | Windows Pro/Ent | TPM-sealed AES-XTS, GPO/Intune managed |
| EFS | File/folder | Windows | User cert-based, transparent, no recovery agent = data loss risk |
| VeraCrypt | Volume/partition/hidden OS | Windows/macOS/Linux | Hidden volumes, cascaded ciphers (AES-Twofish-Serpent) |

Rule of thumb: whole-disk + TPM + enterprise mgmt → BitLocker. File-level only → EFS. Cross-platform or plausible deniability → VeraCrypt.

## Steganography
- **LSB (image):** alters least significant bit of pixel bytes — minimal visual change, common exam focus.
- **Audio stego:** hides data in least significant bits of audio samples (e.g., MP3Stego).
- **File hiding:** appends/embeds data after EOF marker or in unused header space.
- Tools: OpenStego, Steghide, S-Tools.

## Cryptography in Blockchain
- **Hashing:** SHA-256 secures block headers/transactions (Bitcoin).
- **Merkle tree:** enables lightweight (SPV) verification of a transaction via a Merkle proof — O(log n), not full download.
- **Consensus:** Proof-of-Work (computational hashing race) vs Proof-of-Stake (economic stake-weighted validation).

## Exam Traps
- AH sounds 'more secure' by name but provides NO encryption — ESP is the confidentiality protocol.
- KRACK ≠ break of AES; it's a handshake replay/nonce-reuse flaw.
- WPA3 uses SAE, not PSK, for the initial exchange — eliminates offline dictionary attacks.
- BitLocker ≠ EFS: volume vs file-level scope is the #1 differentiator tested.
