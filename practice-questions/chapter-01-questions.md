## Chapter 1: Cryptography Foundations and Classical Ciphers — Practice Questions

**Q1.** A company needs to ensure that a sender cannot later deny having digitally signed and sent a contract. Which mechanism BEST provides this guarantee?

A) Symmetric encryption with a shared secret key
B) A Message Authentication Code (MAC) using a shared key
C) A SHA-256 hash of the message
D) A digital signature created with the sender's private key

<details>
<summary>Answer</summary>

**Correct: D**

Digital signatures use the signer's unique private key, which only the signer possesses. Anyone can verify it with the public key, binding identity to the message and providing non-repudiation.

**Why the others are wrong:**
- Symmetric keys are shared, so either party could have produced the ciphertext — no proof of unique origin.
- A MAC uses a shared secret key, so either the sender or receiver could have generated it — no non-repudiation.
- A hash alone only proves integrity (data wasn't altered), not who sent it.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Using the Vigenere cipher with plaintext 'ATTACK' and repeating keyword 'LEMON', what is the ciphertext letter for the first plaintext letter 'A'?

A) A
B) M
C) L
D) K

<details>
<summary>Answer</summary>

**Correct: C**

A=0, key letter L=11. (0+11) mod 26 = 11 = 'L'.

**Why the others are wrong:**
- Copies the plaintext unchanged, ignoring the key shift entirely.
- Results from adding the wrong key letter or miscounting the alphabet position.
- Off-by-one indexing error when converting letters to numbers (0-25 vs 1-26).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An analyst chooses a=4 for an affine cipher with modulus 26. What is the result?

A) The cipher becomes non-invertible because gcd(4,26)=2, so decryption is impossible
B) Encryption works normally but slightly slower
C) b must be set equal to a for the cipher to function
D) It behaves exactly like a Caesar cipher with only minor weakening

<details>
<summary>Answer</summary>

**Correct: A**

gcd(4,26)=2, not 1, so the mapping x -> 4x+b mod 26 is not a bijection — multiple plaintext letters collide to the same ciphertext letter, making unique decryption impossible.

**Why the others are wrong:**
- Modular arithmetic has no performance/overflow concept relevant to this exam.
- a and b are independent key components; there's no such requirement.
- It does not merely 'weaken' the cipher — invalid a values fully break decryption.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** Which cipher encrypts plaintext in digraphs (letter pairs) using a 5x5 key square rather than encrypting single letters?

A) Vigenere
B) Caesar
C) Playfair
D) Atbash

<details>
<summary>Answer</summary>

**Correct: C**

Playfair uses a 5x5 grid built from a keyword and encrypts two letters (a digraph) at a time using grid position rules.

**Why the others are wrong:**
- Vigenere is polyalphabetic but still encrypts one letter at a time using a repeating keyword shift.
- Caesar applies a single fixed shift to one letter at a time.
- Atbash is a fixed single-letter reversal (A<->Z) with no grid and no key.

</details>

---

**Q5.** Which WWI-era German cipher used only the six letters A, D, F, G, V, X and combined a grid-based substitution with columnar transposition?

A) Playfair
B) ADFGVX
C) Rail Fence
D) Homophonic cipher

<details>
<summary>Answer</summary>

**Correct: B**

ADFGVX used a 6x6 grid (36 characters, letters+digits) labeled with those six letters, then applied columnar transposition to the fractionated output — a German field cipher from WWI.

**Why the others are wrong:**
- Playfair uses a 5x5 grid with no restriction to six letters and no transposition step.
- Rail Fence is pure transposition with no substitution grid or letter-set restriction.
- Homophonic ciphers map multiple symbols to one plaintext letter to flatten frequency; unrelated to the ADFGVX letter set.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** On a WWII Enigma machine, if the plugboard (Steckerbrett) swaps A and F, what is guaranteed about the overall machine's behavior?

A) A will still never encrypt to itself, since the rotor/reflector design prevents any letter mapping to itself
B) A can now encrypt to itself for that keypress
C) The plugboard now controls rotor stepping order
D) The plugboard replaces the function of the reflector

<details>
<summary>Answer</summary>

**Correct: A**

The plugboard adds an extra substitution layer before and after the rotors, but the reflector design still guarantees a letter can never encrypt to itself — this flaw was exploited at Bletchley Park.

**Why the others are wrong:**
- Contradicts Enigma's core structural flaw, which the exam explicitly tests.
- Rotor stepping is driven by notches on the rotors themselves, not the plugboard.
- The reflector (Umkehrwalze) is a separate component that routes the signal back through the rotors; the plugboard doesn't replace it.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** For an affine cipher with modulus 26, which value of 'a' produces a valid, invertible key?

A) 2
B) 9
C) 13
D) 26

<details>
<summary>Answer</summary>

**Correct: B**

gcd(9,26)=1, so 9 is coprime with 26 and produces a valid bijective mapping.

**Why the others are wrong:**
- gcd(2,26)=2, not coprime — invalid.
- gcd(13,26)=13, not coprime — invalid.
- gcd(26,26)=26, equivalent to a=0 — invalid.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** According to Kerckhoffs's principle, the security of a cryptosystem should rely on:

A) Keeping the algorithm itself secret from adversaries
B) A combination of a secret algorithm and a secret key
C) Keeping only the key secret, while the algorithm may be public knowledge
D) The physical security of the hardware implementing the cipher

<details>
<summary>Answer</summary>

**Correct: C**

Kerckhoffs's principle states a system should remain secure even if everything about it except the key is publicly known.

**Why the others are wrong:**
- This describes security through obscurity, the opposite of the principle.
- The principle explicitly rejects the need for a secret algorithm.
- Physical hardware security is unrelated to the principle's definition of cryptosystem security.

</details>

---

