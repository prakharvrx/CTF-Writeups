This challenge is a classic example of a **bit-flipping attack** against the **AES-CBC (Advanced Encryption Standard in Cipher Block Chaining mode)** block cipher. The core idea is to manipulate the Initialization Vector (IV) to alter the decrypted plaintext without knowing the encryption key.

## The Challenge

We are given an encrypted message from Donald. We know the following details:

- **Encryption Algorithm:** AES-CBC
- **Block Length:** 16 bytes (32 hexadecimal characters)    
- **Encrypted Message:** `{391e95a15847cfd95ecee8f7fe7efd66, 8473dcb86bc12c6b6087619c00b6657e}`
- **Components:** This message is a combination of the Initialization Vector (IV) and the Ciphertext (c) in the format `{IV, c}`.
    
    - **Original IV:** `391e95a15847cfd95ecee8f7fe7efd66`
    - **Ciphertext:** `8473dcb86bc12c6b6087619c00b6657e`
    
- **Original Plaintext:** `FIRE_NUKES_MELA!`
- **Target Plaintext:** `SEND_NUDES_MELA!`


Our goal is to find the new IV that, when used with the original ciphertext, will decrypt to our target plaintext. The final flag format is `flag{IV,c}`.

## The Vulnerability: AES-CBC Bit-Flipping

```
The CBC mode of operation has a specific decryption process for each block. To decrypt a ciphertext block (Ci​), it is first decrypted using the key, and the result is then XORed with the previous ciphertext block (Ci−1​) to get the plaintext (Pi​). The first block (C1​) is a special case, as it is XORed with the Initialization Vector (IV).

The decryption formula for the first block is: P1​=Ek​(C1​)⊕IV  

Since we know the original plaintext (P1​), the original ciphertext (C1​), and the original IV, we can use the properties of the XOR operation to derive the value of the decrypted ciphertext block, D.

D=Ek​(C1​)=P1​⊕IV  

Because the XOR operation is commutative and associative, we can also calculate the new IV we need to produce our desired plaintext, Pnew​.

Pnew​=D⊕IVnew​ Pnew​=(Poriginal​⊕IVoriginal​)⊕IVnew​  

By XORing both sides of the equation with Poriginal​ and IVoriginal​, we can isolate the unknown variable, IVnew​.

IVnew​=Pnew​⊕Poriginal​⊕IVoriginal​  

This is the exact logic we will implement in our exploit script.
```

## The Exploitation

We can write a simple Python script to perform the XOR operations on the byte arrays of the original IV, original plaintext, and our desired new plaintext.