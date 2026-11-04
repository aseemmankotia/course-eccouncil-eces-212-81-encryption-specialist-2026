# Chapter 7 Lab: Digital Signatures, X.509 Certificates, and PKI

**Estimated time:** 20 minutes

## Exercise

Generate a self-signed X.509 certificate with OpenSSL, inspect all fields using openssl x509 -text -noout, then build a simple two-tier CA and verify the resulting certificate chain

## Key takeaway

Signing always uses the signer's private key on a hash of the data, and trust in PKI flows downward from a self-signed root CA.
