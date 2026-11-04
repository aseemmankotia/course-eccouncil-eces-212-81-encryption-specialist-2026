## Chapter 8: SSL/TLS Handshakes and Authentication Protocols — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | TLS 1.3 full handshake round trips (RTT)? | 1-RTT (down from 2-RTT in TLS 1.2). 0-RTT resumption is possible with a PSK but has weaker replay protection. Exam tip: TLS 1.3 = 1-RTT. |
| 2 | Kerberos KDC default port? | Port 88 (TCP/UDP). Exam tip: KDC (AS + TGS) listens on 88. |
| 3 | Windows default Kerberos TGT lifetime? | 10 hours max ticket lifetime, renewable up to 7 days (default domain policy, configurable). Exam tip: this is a policy setting, not a protocol-fixed value. |
| 4 | PAP vs CHAP credential transmission | PAP: plaintext password sent once (2-way handshake). CHAP: password never sent — challenge-response hash exchanged, repeated periodically. Exam tip: CHAP = no plaintext, replay-resistant. |
| 5 | TLS 1.2 vs TLS 1.3 static RSA key exchange | TLS 1.2 permits static RSA key exchange (no forward secrecy). TLS 1.3 removed static RSA entirely — only ephemeral (EC)DHE allowed, forward secrecy mandatory. Exam tip: TLS 1.3 = forward secrecy always. |
| 6 | Kerberos authentication flow order | 1) Client→AS: AS_REQ. 2) AS→Client: TGT + session key (AS_REP). 3) Client→TGS: TGT + request (TGS_REQ). 4) TGS→Client: service ticket (TGS_REP). 5) Client→Service: AP_REQ. Exam tip: TGT obtained once; service tickets obtained per resource. |
| 7 | CHAP three-way handshake steps | 1) Authenticator sends Challenge. 2) Peer sends hash(challenge+secret) as Response. 3) Authenticator sends Success/Failure. Repeats periodically. Exam tip: hash commonly MD5 (CHAP/MD5, RFC 1994). |
| 8 | TLS 1.3 approved cipher suites | 5 official AEAD cipher suites: TLS_AES_128_GCM_SHA256, TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256, TLS_AES_128_CCM_SHA256, TLS_AES_128_CCM_8_SHA256. Exam tip: cipher suite = AEAD cipher + hash only; key exchange negotiated separately via extensions. |
| 9 | OpenSSL command to test negotiated TLS version | openssl s_client -connect host:443 -tls1_3 (or -tls1_2). Exam tip: expect a question asking which version was negotiated from a given command/output. |
| 10 | EAP vs PAP/CHAP | EAP is a framework, not a fixed protocol — it carries multiple auth methods (EAP-TLS, EAP-TTLS, PEAP, EAP-MD5). PAP/CHAP are standalone fixed PPP authentication protocols. Exam tip: EAP = extensible container. |
| 11 | Why did TLS 1.3 remove compression and renegotiation? | Compression removed to eliminate CRIME/BREACH-style attacks; renegotiation removed to prevent downgrade and DoS attacks. Exam tip: know TLS 1.3's removed-feature list — compression, renegotiation, static RSA, RC4/3DES/MD5/SHA1 ciphers. |
| 12 | Kerberos ticket contents and replay defense | Tickets contain client identity, validity timestamps, and a session key, encrypted with the KDC/service's secret key. Exam tip: default max clock skew (Windows) is 5 minutes — exceeding it causes authentication failure. |
