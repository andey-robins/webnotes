Cryptography
=====
Notes from Chapter 5: Cryptography.

Terms
-----
- Cryptography = creationg
- Cryptanalysis = breaking
- Cryptology = Cryptogrphay + cryptanalysis
- Encryption = plaintext + key -> cyphertext
    - a reversable process by definition
- Decryption = ciphertext + key -> plaintext
- Block Ciphers = cleartext -> encryption -> ciphertext -> decryption -> plaintext
    - can use either shared keys or public keys
    - public keys are also known as asymmetric keys
    - shared keys (symmetric) must always be kept secret
- Hashes = one way functions
    - plaintext -> hash -> hash
    - can't "dehash" or go back

Examples
-----
Some ciphers, their limitations, and their use cases.

### Mono-Alphabetic Susbstitution Ciphers
- caesar ciphers
- a permutation of the letters of the alphabet

### Stream Ciphers
- vigenere
- this effectively creates a changing shift based on how far into the cipher it is
- if the key is as long as the plaintext, then this is an example of a perfect cipher

### Block Ciphers
- playfair
- a transformation of inputs that can be repeated
- 5x5 grid, drop a single letter (i/j is usually picked)
    - put characters into the grid
    - split plaintext into letter pairs
    - split of pairs with an x
    - make even with an x
    - then choosing based on the letters in the grid comes next

### Hash Functions
- convert a large amount of information into a smaller structure