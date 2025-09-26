I have a `.pcap` file 

so that file I can run into the wireshark

wireshark is the network protocol analyzer tool for capturing packet data

So simply I can use the filter and write it `http` and find the useful packets

![[capture the flag.png]]

and something i get suspicious ``247 2.270670 10.50.203.75 185.21.216.190 HTTP 504 GET /?msg=ZmxhZ3tBRmxhZ0luUENBUH0= HTTP/1.1`` 

In message , msg= I see something in base64 and I can decode this and got the flag ``flag{AFlagInPCAP}``

