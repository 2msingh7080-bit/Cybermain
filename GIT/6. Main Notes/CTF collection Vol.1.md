2025-06-20 22:14

Status:

Tags: #CTF 

# CTF collection Vol.1

## Task 2What does the base said?

 - Can you decode the following?
	 - VEhNe2p1NTdfZDNjMGQzXzdoM19iNDUzfQ==
- how to do 
	- so go to cyberchef and past in base64
 - output : ``THM{ju57_d3c0d3_7h3_b453]``
----
## Task 3Meta meta
- Download the file and extract the meta data using strings 
	- `` strings Find_me_1577975566801.jpg `` 
 - output `` THM{3x1f_0r_3x17}``
----
## Task 4 Mon, are we going to be okay?
Something is hiding. That's all you need to know.  
Answer the questions below
It is sad. Feed me the flag.
----
1. extract uing steghide  
   - ``steghide extract -sf Extinction_1577976250757.jpg``
	- ``cat Final_message.txt ``
	- output `` THM{500n3r_0r_l473r_17_15_0ur_7urn}``
----
## Task 5Erm......Magick
Huh, where is the flag? ==THM{wh173_fl46}==

----
## Task 6QRrrrr
- simple download QRcode and then scan it in online QRcode scanner
- output ``THM{qr_m4k3_l1f3_345y}``
----
## Task 7Reverse it or read it?
- download and run strings hello_1577977122465.hello   
- output `` THM{345y_f1nd_345y_60}``
----
## Task 8Another decoding stuff
Can you decode it?
3agrSy1CewF9v8ukcSkPSYm3oKUoByUpKG4L
- paste it on cyber chef (base58)
- output ``THM{17_h45_l3553r_l3773r5}``
----
## Task 9Left or right
Left, right, left, right... Rot 13 is too mainstream. Solve this
MAF{atbe_max_vtxltk}

- paste it on cyber chef under  ROT13 and set amount to 7
- output  `` THM{hail_the_caesar}`` 
----
## Task 10Make a comment
- inspect the page and you will get it 
- output `` THM{4lw4y5_ch3ck_7h3_c0m3mn7}``
----
## Task 11Can you fix it?
- download the file 
- open hexda editor  
- fix the header for png using hexda editor (**89 50 4e 47**)
	- `` hexeditor spoil_1577979329740.png ``
- ouput `` THM{y35_w3_c4n}``
----
## Task 12Read it 

- open reddit [here](https://www.reddit.com/r/tryhackme/comments/eizxaq/new_room_coming_soon/)
- output `` THM{50c14l_4cc0un7_15_p4r7_0f_051n7}``
----
## Task 13Spin my head 
What is this?

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++.------------.+++++.>+++++++++++++++++++++++.<<++++++++++++++++++.>>-------------------.---------.++++++++++++++.++++++++++++.<++++++++++++++++++.+++++++++.<+++.+.>----.>++++.

- decode using cipher decode [here](https://www.dcode.fr/brainfuck-language)
- output ``THM{0h_my_h34d}``
----
## Task 14An exclusive!
Exclusive strings for everyone!

S1: 44585d6b2368737c65252166234f20626d  
S2: 1010101010101010101010101010101010
- run this code as python 
```bash
s1 = "44585d6b2368737c65252166234f20626d"
S2 = "1010101010101010101010101010101010"
s2 = S2  # Fix the variable name to match case
a = hex(int(s1, 16) ^ int(s2, 16))[2:]
print(bytes.fromhex(a).decode("utf-8"))
```
- run ``python T14.py``
- output  `` THM{3xclu51v3_0r}`` 
----
## Task 15Binary walk
- download the file
- run this command 
	- ``binwalk hell_1578018688127.jpg``
	- ``unzip hell_1578018688127.jpg``
	- ``cat hello_there.txt ``
- output ``  THM{y0u_w4lk_m3_0u7}``
----
## Task 16Darkness 
- download the image 
- scan in  aperslove  [here](https://www.aperisolve.com/)
- output `` THM{7h3r3_15_h0p3_1n_7h3_d4rkn355}``
----
## Task 17A sounding QR
How good is your listening skill?

P/S: The flag formatted as THM{Listened Flag}, the flag should be in All CAPS
- output ``THM{SOUNDINGQR}
----
## Task 18Dig up the past
Sometimes we need a 'machine' to dig the past

Targetted website: https://www.embeddedhacker.com/[](http://www.embeddedhacker.com)  
Targetted time: 2 January 2020
- use wayback machine 
- ouput  `` THM{ch3ck_th3_h4ckb4ck}`` 
----
## Task 19Uncrackable!
Can you solve the following? By the way, I lost the key. Sorry >.<  

MYKAHODTQ{RVG_YVGGK_FAL_WXF}

Flag format: TRYHACKME{FLAG IN ALL CAP}

- use cipher [here](https://www.dcode.fr/vigenere-cipher)
- output `` TRYHACKME{YOU_FOUND_THE_KEY}``
---
## Task 20Small bases

Decode the following text.
581695969015253365094191591547859387620042736036246486373595515576333693

- convert from dec to hex -> then put it to cyber chef 
- output  ``THM{17_ju57_4n_0rd1n4ry_b4535}``
-----
## Task 21Read the packet
I just hacked my neighbor's WiFi and try to capture some packet. He must be up to no good. Help me find it.

- open wire shark with the downloaded file  -> select http 
- output `` THM{d0_n07_574lk_m3}``
----

### References
