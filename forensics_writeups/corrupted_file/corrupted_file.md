The main goal is to get the flag by manipulating the GIF headers

1. After download the `unopenable.gif`, it's not accessible. when I checked online its hex dump, it differed from standard GIF header
2. A standard GIF header looks like that in hex-dump:
![[hex-dump.png]]

3. According to that I can change the header of that GIF and download into the `new.gif`
4. After I see the GIF then it shows the base64 encrypted text : ``ZmxhZ3tnMWZfb3JfajFmfQ==``
5. I decode it and get the flag : ``flag{g1f_or_j1f}``
