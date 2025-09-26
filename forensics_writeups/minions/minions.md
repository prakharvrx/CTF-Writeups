The main goal is to find the flag is to use binwalk and basic crypto recon

1. Download the image `Hey_You.png`
![[minions1.png]]

2. When we do a `strings Hey_You.png`. We get the following output:
```bash
...
Rar!
$You_Still_Here/Nothing_Here_16/..txt
Ac]I
https://mega.nz/file/wZw2nAhS#i3Q0r-R8psiB8zwUrqHTr661d8FiAS1Ott8badDnZkoH
You_Still_Here/Nothing_Here_1
You_Still_Here/Nothing_Here_10
You_Still_Here/Nothing_Here_11
You_Still_Here/Nothing_Here_12
You_Still_Here/Nothing_Here_13
You_Still_Here/Nothing_Here_14
You_Still_Here/Nothing_Here_15
You_Still_Here/Nothing_Here_16
You_Still_Here/Nothing_Here_17
You_Still_Here/Nothing_Here_18
You_Still_Here/Nothing_Here_19
You_Still_Here/Nothing_Here_2
You_Still_Here/Nothing_Here_3
You_Still_Here/Nothing_Here_4
You_Still_Here/Nothing_Here_5
You_Still_Here/Nothing_Here_6
You_Still_Here/Nothing_Here_7
You_Still_Here/Nothing_Here_8
You_Still_Here/Nothing_Here_9
You_Still_Here
```
3. We get another image from there `Only_Few_Steps.jpg`
![[minons2.png]]

If we do `strings Only_Few_Steps.jpg`. We get following output:
```bash
YouWon(Almost).jpg
```

4. This says that we have to use ``binwalk --extract --dd=".*." Only_Few_Steps.jpg``, to get that other image. After extracting we got the following image:
![[minions3.png]]

5. When we do `strings YouWon(Almost).jpg`, we get the following output:
```bash
CTF{VmtaU1IxUXhUbFZSYXpsV1RWUnNRMVpYZEZkYWJFWTJVVmhrVlZGVU1Eaz0=}
```
After decoding with base64 strings:

Flag: ``CTF{M1NI0NS_ARE_C00L}``
