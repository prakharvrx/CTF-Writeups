1. Download the image `Gandalf.jpg`, I trying the strings command and I got the output:
![[gandlaf.png]]
```bash
JFIF
+Q1RGbGVhcm57eG9yX2lzX3lvdXJfZnJpZW5kfQo=
+xD6kfO2UrE5SnLQ6WgESK4kvD/Y/rDJPXNU45k/p
+h2riEIj13iAp29VUPmB+TadtZppdw3AuO7JRiDyU
...
```
3. I decrypted the first one which is `Q1RGbGVhcm57eG9yX2lzX3lvdXJfZnJpZW5kfQo=` and get the false flag which is ``CTFlearn{xor_is_your_friend}``
4. Then I decrypted the remaining 2 and I get the hexadecimal text because of the RFC
5. Then I XOR them online and get the flag : `CTFlearn{Gandalf.BilboBaggins}`

RFC text is a formal document describing IP or standards