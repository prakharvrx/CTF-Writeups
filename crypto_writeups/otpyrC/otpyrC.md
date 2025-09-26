The main goal is to finding the flag is string reversal and simple decryption.

1. After I read the given message:
```bash
Okay, this one is pretty easy... but not necessarily.
d733432373937303734373666343730373937323733343b7644534
```
2. I just did the reversal online:
![[crypto/crypto_writeups/otpyrC/1.png]]
3. It was just hexadecimal text and I decrypted it.
![[crypto/crypto_writeups/otpyrC/2.png]]
I got `CTF{`43727970746f7470797243`}`. but did not work as flag
So decrypted the string again:
![[crypto/crypto_writeups/otpyrC/3.png]]

Flag: ``CryptotpyrC``
