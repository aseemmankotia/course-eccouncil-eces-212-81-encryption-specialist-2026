# Chapter 4 Lab: Hash Functions, MAC, and HMAC

**Estimated time:** 20 minutes

## Exercise

Generate MD5, SHA-1, and SHA-256 digests of the same file with OpenSSL to compare output lengths, then compute an HMAC-SHA256 and a PBKDF2-derived key in Python using hashlib

## Key takeaway

Hash output size is not the same as effective security strength — always apply the birthday bound, and never use MD5 or SHA-1 for security-critical integrity.
