## Chapter 8 Cheat Sheet — SSL/TLS Handshakes & Authentication Protocols
**Exam Domain:** Applications of Cryptography (24%)

### TLS 1.2 vs TLS 1.3
| Feature | TLS 1.2 | TLS 1.3 |
|---|---|---|
| Handshake RTT | 2-RTT | 1-RTT (0-RTT resumption option) |
| Static RSA key exchange | Allowed | Removed |
| Forward secrecy | Optional (depends on suite) | Mandatory (ECDHE/DHE only) |
| Compression | Allowed | Removed (CRIME/BREACH) |
| Renegotiation | Allowed | Removed |
| Cipher suite count | Dozens (many weak) | 5 AEAD-only suites |
| Weak ciphers (RC4, 3DES, MD5, SHA1) | Present | Removed |

### Cipher Suite Negotiation (TLS 1.3)
- ClientHello includes supported cipher suites + key_share extension (guessing likely group, e.g. X25519).
- ServerHello selects cipher suite + key_share → handshake keys derived immediately → 1-RTT complete.
- Cipher suite format: `TLS_<AEAD-cipher>_<hash>` — key exchange algorithm is negotiated separately.

### PAP vs CHAP
| | PAP | CHAP |
|---|---|---|
| Handshake | 2-way | 3-way (+ periodic re-challenge) |
| Credential sent | Plaintext password | Never sent — hash of challenge+secret |
| Replay protection | None | Yes (new challenge each cycle) |
| Hash algorithm | N/A | Typically MD5 |

### EAP Framework
- EAP = extensible **framework**, not a protocol itself; carries methods over PPP/802.1X.
- Common methods: **EAP-TLS** (mutual cert auth, strongest), **PEAP** (TLS tunnel + inner method), **EAP-TTLS**, **EAP-MD5** (weak, one-way), **LEAP** (Cisco, deprecated/weak).
- Exam tip: EAP-TLS requires certs on both client & server — most secure but highest deployment overhead.

### Kerberos Flow
1. **AS_REQ / AS_REP** — Client authenticates to Authentication Server (AS) using password-derived key → receives **TGT** + session key.
2. **TGS_REQ / TGS_REP** — Client presents TGT to Ticket Granting Server (TGS) → receives **service ticket**.
3. **AP_REQ** — Client presents service ticket directly to the target service (no password re-entry).
- KDC = AS + TGS combined. Default port: **88**.
- Default Windows TGT lifetime: **10 hours**, renewable **7 days** (policy-based).
- Replay defense: encrypted **timestamps**; default max clock skew **5 minutes**.

### Common Exam Traps
- Confusing TLS 1.3's 1-RTT with 0-RTT (0-RTT only on resumption, has replay risk).
- Assuming CHAP sends a hashed *password* — it hashes *challenge+secret*, password itself never transmitted.
- Thinking EAP is a single protocol rather than a carrier framework.
- Mixing up TGT (proves identity to KDC) vs service ticket (grants access to a specific resource).
