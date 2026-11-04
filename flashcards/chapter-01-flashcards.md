## Chapter 1: Cryptography Foundations and Classical Ciphers — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Affine cipher encryption formula? | E(x) = (ax + b) mod 26. Requires gcd(a,26)=1. Exam tip: only 12 valid values of a (1,3,5,7,9,11,15,17,19,21,23,25). |
| 2 | Total affine cipher keyspace (mod 26)? | 12 valid 'a' values × 26 possible 'b' values = 312 total keys. |
| 3 | Caesar cipher key space size? | 25 possible shifts (excluding shift of 0). Exam tip: trivially broken via brute force or frequency analysis. |
| 4 | Atbash cipher key? | No key — fixed reverse-alphabet substitution (A<->Z, B<->Y...). Exam tip: it is its own inverse (applying it twice returns the original text). |
| 5 | Vigenere vs Caesar — key difference? | Vigenere: polyalphabetic, keyword drives a different shift per letter, resists simple frequency analysis. Caesar: monoalphabetic, one fixed shift. Exam tip: Vigenere is broken via Kasiski examination (finding repeated key length). |
| 6 | Playfair cipher grid size and missing letter? | 5x5 grid = 25 cells. J is combined with I (or omitted). Exam tip: encrypts digraphs (letter pairs), not single letters. |
| 7 | ADFGVX cipher origin and structure? | German WWI field cipher. 6x6 grid (36 chars: A-Z + 0-9) labeled A D F G V X; combines substitution + columnar transposition. Exam tip: a fractionation cipher. |
| 8 | Enigma's core structural flaw exploited at Bletchley Park? | No letter can ever encrypt to itself, due to the reflector design. This enabled known-plaintext 'crib' attacks. |
| 9 | Enigma plugboard (Steckerbrett) purpose? | Swaps pairs of letters before/after rotor scrambling (up to 10 pairs), adding an extra substitution layer. Exam tip: increases keyspace but does NOT remove the 'no self-encryption' flaw. |
| 10 | Kerckhoffs's principle in one sentence? | A cryptosystem must remain secure even if everything about it except the key is public knowledge. Exam tip: opposite of 'security through obscurity.' |
| 11 | Four core security goals tested in this chapter? | Confidentiality (keep data secret), Integrity (data unaltered), Authentication (verify identity), Non-repudiation (sender can't deny sending — requires a digital signature, not just a MAC). |
| 12 | Rail Fence cipher type? | Transposition cipher — plaintext written in a zigzag across 'rails,' then read row by row. Exam tip: no substitution occurs, so letter frequency analysis still reveals the original alphabet distribution. |
