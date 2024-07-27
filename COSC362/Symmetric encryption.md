### Advanced Encryption Standard (AES)
- Designed in an open competition due to controversy over DES (?)
- Substitution-permutation network (fancy maths)
- Block length of 128bit
- Key size can be size to 128, 192, or 256 bits
- All operations performed on 8-bit blocks

- Round 0: Add round key
- Round 1 to N-1: substitute bytes, shift rows, mix columns, add round key
- Round N: substitute bytes, shift tows, add round key

#### Modes of operation (?)

#### Confidentiality only
- Electronic code block (ECB)
	- The same data block gets encrypted the same way
		- This reveals patterns of data when a data block repeats
	- Ideal for a short amount of data
- Cipher block chaining (CBC) 
- Output feed back (OFB)
- Cipher feed back (CFB)
- Counter (CTR)

### Cryptanalysis
> The process of attempting to discover the plaintext or key of encrypted data

Brute-force attacks:
- Try every possible key against the ciphertext until the plaintext is outputted.
- On average, half of all possible keys must be tried
Cryptanalytic attacks:
- Rely on the nature of the algorithm plus perhaps some knowledge of the general characteristics of the plaintext or even some sample plaintext-ciphertext pairs.

An encryption scheme is computationally secure if it meets one of the following:
- The cost of breaking the cipher exceeds the value of the encrypted information
- The time required to break the cipher exceeds the useful lifetime of the information

#### Ciphertext only attack
- Only know algorithm and ciphertext
- Have a general idea of what is contained, e.g. language, filetype, fixed header

#### Known plaintext
- Know the algorithm, ciphertext, and one or more plaintext-ciphertext pairs
- May also know certain patterns in the plaintext
- Attacker cannot select the plaintext-ciphertext pairs

#### Chosen plaintext
- Know the algorithm, ciphertext, and chosen plaintext-ciphertext pairs
- Can interact with the source system
- Attacker controls the plaintext, and system generates the corresponding ciphertext
- Goal is to discover the secret/pattern used to encrypt
- Attack is typically used against public key algorithms

