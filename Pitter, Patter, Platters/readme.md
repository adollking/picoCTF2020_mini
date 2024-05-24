# Pitter, Patter, Platters


## Description
'Suspicious' is written all over this disk image. Download suspicious.dd.sda1


## solution

lets using fls to get list file

```console
fls suspicious.dd.sda1

d/d 11: lost+found
d/d 2009:       boot
d/d 4017:       tce
r/r 12: suspicious-file.txt
V/V 8033:       $OrphanFiles

```
using icat to print file 

```console
icat suspicious.dd.sda1 12

Nothing to see here! But you may want to look here -->

```
get line using strings 

```console

┌──(root㉿DES)-[Pitter, Patter, Platters]
└─# strings -a -t x suspicious.dd.sda1 | grep "Nothing to see here!"
 200400 Nothing to see here! But you may want to look here -->
```
using xxd to tail string 

``` console
 xxd -s 0x200400 -l 120 suspicious.dd.sda1
00200400: 4e6f 7468 696e 6720 746f 2073 6565 2068  Nothing to see h
00200410: 6572 6521 2042 7574 2079 6f75 206d 6179  ere! But you may
00200420: 2077 616e 7420 746f 206c 6f6f 6b20 6865   want to look he
00200430: 7265 202d 2d3e 0a7d 0031 0032 0039 0030  re -->.}.1.2.9.0
00200440: 0038 0038 0061 0062 005f 0033 003c 005f  .8.8.a.b._.3.<._
00200450: 007c 004c 006d 005f 0031 0031 0031 0074  .|.L.m._.1.1.1.t
00200460: 0035 005f 0033 0062 007b 0046 0054 0043  .5._.3.b.{.F.T.C
00200470: 006f 0063 0069 0070                      .o.c.i.p
```
echo and rev

```console
┌──(root㉿DES)-[Pitter, Patter, Platters]
└─# echo "}129088ab_3<_|Lm_111t5_3b{FTCocip" | rev
picoCTF{b3_5t111_mL|_<3_ba880921}
```
