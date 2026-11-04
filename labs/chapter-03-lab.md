# Chapter 3 Lab: Cipher Modes, Key Scheduling, and Key Management

**Estimated time:** 15 minutes

## Exercise

Encrypt a bitmap image with OpenSSL in AES-ECB and AES-CBC, view both outputs to observe the 'ECB penguin' pattern leakage, then repeat CTR mode encryption with a reused nonce to demonstrate keystream reuse

## Key takeaway

Mode selection determines whether patterns leak and whether nonce/IV reuse is catastrophic — ECB is always the wrong exam answer for real data.
