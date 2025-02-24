In cryptography, a **mode of operation** refers to an algorithm that uses a block cipher to provide information security, such as confidentiality or authenticity. Here are some common modes of operation:

1. **Electronic Codebook (ECB)**: The simplest mode, where each block of plaintext is encrypted independently. [However, it is not recommended for use because identical plaintext blocks result in identical ciphertext blocks, making it vulnerable to pattern analysis](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)[1](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation).

![[Pasted image 20240912153507.png]]

2. **Cipher Block Chaining (CBC)**: Each plaintext block is XORed with the previous ciphertext block before being encrypted. [This mode ensures that identical plaintext blocks yield different ciphertext blocks, enhancing security](https://www.geeksforgeeks.org/block-cipher-modes-of-operation/)[2](https://www.geeksforgeeks.org/block-cipher-modes-of-operation/).
   
![[Pasted image 20240912153551.png]]
    
3. **Counter (CTR)**: Converts a block cipher into a stream cipher by encrypting successive values of a counter. [It allows for parallel encryption and decryption, making it highly efficient](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)[1](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation).

![[Pasted image 20240912153635.png]]

4. **Galois/Counter Mode (GCM)**: Combines the counter mode of encryption with Galois mode of authentication. [It provides both confidentiality and data integrity, making it a popular choice for secure communications](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)[1](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation).