I have a image and I have to find the hidden flag inside the flag

![[bobby image.png]]

so simple I can use the strings command to analyze but it shows nothing so after I can use the hex editor and i found something,

![[hex editor.png]]

the image have some hidden messages like : ``congrats you found me! you win an iPad!``

if you see the first hex you will see it's a jpeg file,
![[jpeg signature.png]]

so using the stego tool to find the hidden message inside the image and i got this ``zpv_tigqylhbafmeoesllpms`` so I can then use the one time pad so after I got the final flag that is ``you_thinkyougotskillshuh``

