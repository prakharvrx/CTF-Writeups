1. Download the image `oreo.jpg` from the cloud, I tried the strings but I couldn't find the correct flag, so I tried for some hidden data in the image.
![[one_oreo.png]]
2. Then I use the binwalk and I got the output:
```bash
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
9515          0x252B          RAR archive data, version 4.x, first volume type: MAIN_HEAD
```
3. Extract all, I used `binwalk -D oreo.jpg` and I got directory `_oreo.jpg.extracted` at that location and I checked its contents and it had a directory called `1` & a zip `2528.rar`. I choose to explore `1` first.
4. I try `strings b.jpg` before I got a file `b.jpg`
![[two_oreo.png]]
5. I got the output:
```bash
JFIF
"1$%)+...
383-7(-.+
%----------------------+----------------------+---7
!1AQqa
\5n`]
xsLy
.y fk
vSk:M
DzuMb
_NZ@
]ETyn
Xg3H
nBC_
]95r
C^^[p
Q`';
q`7'
\\o*
. 	&
04KZ
)Qc&
Q{k~
st&[
NW89
Lk$[
1Y79
a0\A
$;6g
%mG+$
DysM
2em7
6M>f
Ztn`$F
qUhTmjN
+67*
e6hi 
0d$j
-ko)'
CH;^u
&Du=
$t$Lv
1/i 
/1-6n
Gx#GA
M8n!
iT0?
kVI8
`.}v
gPl,c
bsDKw
O]=6V1
Rx|!
\l&>
!G=*
HSayi-9
#X3i
c>R2
 $+cmk1
u|h]a
tEp#
&Z	2`
ZMmG
a;}V
{2sRpo7%V
0=Q-C:
[e[!A
|5xk
+NgU
;HO+dD
D272}
`h	:
K`8m:-
Finally, flag{eat_more_oreos}
```

Flag : ``flag{eat_more_oreos}``

