# Chapter 7 Cheat Sheet: Digital Signatures, X.509, PKI

## Digital Signature — Order of Operations (heavily tested)
1. **Hash** the message (SHA-256 or stronger)
2. **Encrypt the hash** with the **sender's PRIVATE key** → this is the signature
3. Verifier **decrypts signature** with sender's **PUBLIC key** and compares to a fresh hash of the received message

**Never:** encrypt the whole message with the private key to "sign" it — sign the hash, not the data.

| Goal | Use Sender's... | Use Recipient's... |
|---|---|---|
| Confidentiality | — | Public key (encrypt) |
| Authentication/Signing | Private key (encrypt/sign) | — |
| Verify signature | Public key (decrypt/verify) | — |

## X.509 Certificate Key Fields

| Field | What It Proves |
|---|---|
| Subject | Entity the cert was issued **to** |
| Issuer | CA that **vouched** for / signed the cert |
| Validity Period (Not Before/Not After) | Time window cert is valid |
| Public Key | Subject's public key |
| Signature Algorithm/Value | CA's signature over the cert body — binds identity to key |
| Serial Number | Unique ID within the issuing CA |
| Key Usage | Allowed operations for the subject's key (not the CA's signature) |

## CRL vs OCSP

| | CRL | OCSP | OCSP Stapling |
|---|---|---|---|
| Method | Full list of revoked certs | Real-time single-cert query | Server pre-fetches signed OCSP response |
| Freshness | Periodic (can be stale) | Near real-time | Near real-time |
| Latency impact | Download overhead | Extra round trip to CA | No extra client round trip |
| Privacy | Good (no per-check CA contact) | CA sees client's queries | Good (CA doesn't see client) |
| Works offline/air-gapped | Yes (transferable file) | No | No |

**Exam rule:** Expiration and revocation are checked **independently** — an expired cert is rejected even if OCSP says "good."

## PKI Hierarchy / Chain of Trust

```
Root CA (self-signed, trust anchor, offline)
  └── Intermediate CA (signed by Root, does issuing)
        └── End-entity certificate (server/user)
```

- **Root CA**: self-signed, long validity, kept offline to protect its private key
- **Intermediate CA**: signed by root, handles routine issuance, limits root key exposure
- **Trust anchor**: root's public key/cert pre-installed in OS/browser trust store; chain validation terminates here

## Certificate Validation Levels

| Type | Verifies |
|---|---|
| DV | Domain control only |
| OV | Domain + legal business existence |
| EV | Domain + legal + physical + operational existence (highest assurance) |

## Key Numbers
- SHA-256 output: 256 bits
- Min RSA key size (current): 2048 bits
- Max public TLS cert validity: 398 days
- SHA-1: deprecated for signatures since 2017
- MD5/CRC32: never use for signing (broken/non-cryptographic)
