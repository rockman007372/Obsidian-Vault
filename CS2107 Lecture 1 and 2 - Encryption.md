---
tags:
  - toProcess
course: CS2107
type: lecture
date: 2024-09-04 Wednesday
---
## Notes

#### Classical ciphers
- Substitution
- Permutation
- One time pad

Substitution cipher:
- Key = a substitution table S, 1-1 mapping 
- Key space: set of all possible keys
- Key space size: number of all possible keys
- Key size / length: number of bits to represent a key = log(total keys)
- Vulnerable to Frequency Analysis attack

Permutation cipher:
- Divide plain text into groups of size t
- Within each group, apply a permutation

One-time pad:
- n bit message, n bit key
- encryption: XOR each message bit with key bit

#### Modern Ciphers

Block cipher:
- fixed size input/output (e.g 128 bit input will be decrypted into 128 bit output)
- Kinda like a hash function, but used for both encryption and decryption
	- **Symmetric Key**: The same key is used for both encryption and decryption, which must be kept secret between the parties involved.
- Encrypting multiple blocks require **mode-of-operation**.

4 [[Mode of Operation]]: Used to chain blocks of encrypted data

1. Electronic Code Book (ECB)
	- deterministic block cipher
	- leaks info: each block is encrypted independently, which can reveal patterns and is generally insecure for large data sets.
	- Hence, we need Cipher Block Chaining (used with Initialization Vector)
2. Cipher Block Chaining (CBC)
	- Each plaintext block is XORed with the previous ciphertext block before being encrypted, introducing dependency between blocks
	- 2 same plaintext **blocks** now give different encrypted ciphertext **blocks**!
	- Have an initialization vector (another 128 bit block) - to make CBC output probabilistic 
	- How to decrypt:
		- Need ciphertext, key and IV
		1. **Divide the Ciphertext into Blocks**: Split the ciphertext into blocks of the same size as the block cipher (e.g., 128 bits for AES).
		2. **Decrypt Each Block**: Use the block cipher and the secret key to decrypt each block of ciphertext. This will give you intermediate values.
		3. **XOR with Previous Ciphertext Block**: For each block, XOR the decrypted intermediate value with the previous ciphertext block. For the first block, XOR with the IV.
	- However, is sequential (wastes time)
3. Counter mode (CTR)
	- Increment the IV by one for each block, then encrypt each of them
	- Use the new sequence to XOR  with their respective block
	- Turn a block cipher into a stream cipher, encrypting data in smaller units => **parallelization** 


#### Stream Cipher and IVs
- Counter-mode is a form of stream cipher
- From an IV and a key, form a **pseudorandom sequence** used for one-time paddding (XOR)
- IV and key can change, causing output to be probabilistic

#### Meet-in-the-middle Attack

Problem:
- Info: attacker has pair (m, c) of plaintext and cyphertext. 
	- aka: $(m, DES_{k1}(DES_{k2}(m)))$
- Goal: find k1 and k2

Solution:
- Create 2 sets of all encrypted m and all decrypted c => 2 * 2^k = 2^(k+1)
- Store them in hash table and probe until we find a matching middle man => O(2^k)
- Key size reduced from $2^{2k}$ to $2^{k + 1}$
- Can trade time for space: permutate the last s bits in each key k1 and k2, then apply Meet-in-the-middle
	- Space reduces from  $2^{k + 1}$ to  $2^{k - s + 1}$
	- Time increases to $2^{2s} * 2^{k-s+1} = 2^{k + s + 1}$ 

Remedy:
- 2 keys but triple encryption

#### Padding Oracle attack

Info:
- IV, ciphertext (iv, c)
- padding standard and the actual padding in ciphertext
- Access to Padding Oracle

Padding Oracle: 
- Query: any ciphertext
- Output: yes if the plaintext is in the correct padding format, else no
- Knows the key, used to decrypt ciphertext into plaintext and check padding format

Goal:
- Plaintext of (iv, c)



## Summary

## Questions/Cues

1. Why CBC needs IV?
	1. same plaintext will give the same cyphertext => reveal pattern => need to change IV

