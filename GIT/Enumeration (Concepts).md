2025-07-25 17:17

Status:

Tags:

# Enumeration (Concepts)

### What is Enumeration
Enumeration is the process of extracting usernames, machine names, network resources, shares, and services from a system or network. In the enumeration phase, an attacker creates active connections with the system and sends directed queries to gain more information about the target. The attacker uses the information collected using enumeration to identify vulnerabilities in the system security, which help them exploit the target system.
- In particular, enumeration allows the attacker to collect the following information: 
	- Network resources 
	- Network shares 
	- Routing tables 
	- Audit and service settings 
	- SNMP and fully qualified domain name (FQDN) details 
	- Machine names 
	- Users and groups 
	- Applications and banners

#### Techniques for Enumeration 
-  Extract usernames using email IDs
	- Every email address contains two parts, a username and a domain name, in the format “username@domainname
- Extract information using default passwords
	- Many online resources provide a list of default passwords assigned by manufacturers to their products. 
- Brute force Active Directory
	- Microsoft Active Directory is susceptible to username enumeration at the time of user-supplied input verification. 
- Extract information using DNS Zone Transfer
	- A network administrator can use DNS zone transfer to replicate DNS data across several DNS servers or back up DNS files. For this purpose, the administrator needs to execute a specific zone-transfer request to the name server.
- Extract user groups from Window
	- To extract user groups from Windows, the attacker should have a registered ID as a user in the Active Directory. 
-  Extract usernames using SNMP
	- Attackers can easily guess read-only or read-write community strings by using the SNMP application programming interface (API) to extract usern
- Extract network resources and topology using SNMP
	- Attackers can methodically query the SNMP tree to gather detailed information about network resources and topology
#### Services and Ports to Enumerate
- Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) manage data communications between terminals in a network.
- Services and TCP/UDP ports that can be enumerated include the following. ▪
	- TCP/UDP 53: DNS Zone Transfer
	- TCP/UDP 135: Microsoft RPC Endpoint Mapper
	- UDP 137: NetBIOS Name Service (NBNS)
	-  TCP 139: NetBIOS Session Service (SMB over NetBIOS)
	- TCP/UDP 445: SMB over TCP (Direct Host)
	-  UDP 161: Simple Network Management Protocol (SNMP)
	- TCP/UDP 389: Lightweight Directory Access Protocol (LDAP)
	-  TCP 2049: Network File System (NFS)
	- TCP 25: Simple Mail Transfer Protocol (SMTP)
	- TCP/UDP 162: SNMP Trap
	- UDP 500: Internet Security Association and Key Management Protocol (ISAKMP)/Internet Key Exchange (IK
	- TCP 22: Secure Shell (SSH) / Secure File Transfer Protocol (SFTP) 
	- TCP/UDP 3268: Global Catalog Service 
	- TCP/UDP 5060, 5061: Session Initiation Protocol (SIP)
	- TCP 20/21: File Transfer Protocol
	- TCP 23: Telnet
	- UDP 69: Trivial File Transfer Protocol (TFTP)
	-  TCP 179: Border Gateway Protocol (BGP)

### NetBIOS Enumeration
obtain the NetBIOS name table of a remote computer- 
	 command 
		 `` nbtstat –a <IP address of the remote machine>``-**NetBIOS** stands for **Network Basic Input/Output System**. It is not exactly a network protocol itself but an API (Application Programming Interface) that provides communication services at the session layer (Layer 5 of the OSI model). NetBIOS allows **applications on different computers to communicate with each other within a local area network (LAN)**.

| windows        | Protocols               |
| -------------- | ----------------------- |
| Protocol Ports | TCP 137, 138 (UDP), 139 |
-  A NetBIOS name is a unique 16 ASCII character string used to identify the network devices over TCP/IP; fifteen characters are used for the device name, and the sixteenth character is reserved for the service or name record type

- Attackers use NetBIOS enumeration to obtain the following: 
	- The list of computers that belong to a domain 
	- The list of shares on the individual hosts in a network 
	- Policies and passwords

![[Pasted image 20250725200817.png]]

	
#### Nbtstat Utility 
Nbtstat is a Windows utility that helps in troubleshooting NETBIOS name resolution problems.

-  The syntax of the nbtstat command is as follows:
	- ``nbtstat [-a <remotename>] [-A <IPaddress>] [-c] [-n] [-r] [-R] [-RR] [-s] [-S] [<interval>][-?]``
- The table shown below lists various Nbtstat parameters and their respective functions.
![[Pasted image 20250725201015.png]]
![[Pasted image 20250725201141.png]]


- obtain the NetBIOS name table of a remote computer
	- command 
		- `` nbtstat –a <IP address of the remote machine>``
-  to obtain the contents of the NetBIOS name cache, the table of NetBIOS names, and their resolved IP addresses.
	- command 
		- `` “nbtstat –c``
#### NetBIOS Enumerator
- NetBIOS Enumeration  Tools
	- NetBIOS Enumerator
	- Nmap
	-  Global Network Inventory (https://magnetosoft.com ) 
	- Advanced IP Scanner (https://www.advanced-ip-scanner.com) ▪
	- Hyena (https://www.systemtools.com) 
	- Nsauditor Network Security Auditor (https://www.nsauditor.com)

####  NetBIOS Enumeration using Terminal  
- command 
	- ``nbtscan <ip>``
-  "Get NetBIOS info for IP 10.10.1.11 and display the associated names”
	- command 
		- `` nmblookup -A 10.10.1.11 ``

- Nmap NetBIOS 
- command for NetBIOS  Enumeration
	- ``map -sV -v --script nbstat.nse <target IP address>``
#### Enumerating User Accounts 
- use tools like 
	- PsExec
	- PsGetSid
	-  PsKill
	-  PsInfo
	- PsList
	-  PsLoggedOn
	- PsLogList
	- PsPasswd
	- PsShutdown
- refer material for detailed info  

#### Enumerating Shared Resources Using Net View
Net View is a command-line utility that displays a list of computers in a specified workgroup or shared resources available on a specified computer. It can be used in the following ways.

-  The name or IP address of a specific computer, the resources of which are to be displayed.
	- command 
		- `` net view \\<computername>``
-  The  command displays all the shares on the specified remote computer, along with hidden shares.
	- command 
		- `` net view \\<computername> /ALL``
  - The  command displays all the shares in the domain.
	   - Command 
		   - ``net view /domain``
   - The command displays all the shares on the specified domain
	   - command 
		   - ``net view /dom ain:<domain name> ``
#### NetBIOS Enumeration using AI
- Example #1: ▪ "Perform NetBIOS enumeration on target IP 10.10.1.11”
	- command 
		- `` nbtscan 10.10.1.11 ``
- Example #2: ▪ "Get NetBIOS info for IP 10.10.1.11 and display the associated names”
	- command 
		- `` nmblookup -A 10.10.1.11``
- Example #3: ▪ "Enumerate NetBIOS on target IP 10.10.1.22 with nmap”

### SNMP Enumeration
 SNMP ( Simple Network Management Protocol) Enumeration
- Attackers use SNMP default community strings to extract information about a device 
- Attackers enumerate SNMP to extract information about network resources, such as hosts, routers, devices, and shares, and network information, such as ARP tables, routing tables, and traffic 

|          |                                                    |
| -------- | -------------------------------------------------- |
| Protocol | Application layer protocol using UDP ports 161/162 |
#### Enumerating SNMP using SnmpWalk 
- acttkers execute the following command to retrieve SNMP information from the target device: 
	- command 
		- `` snmpwalk -v1 -c public <Target IP Address>``
-  Command to enumerate SNMPv2 with a community string of public:
	- ``snmpwalk -v2c -c public <Target IP Address>``
-  Command to search for installed software: 
	- `` snmpwalk -v2c -c public <Target IP Address> hrSWInstalledName1``
-  Command to determine the amount of RAM on the host: 
	- ``snmpwalk -v2c -c public <Target IP Address> hrMemorySize``
-  Command to change an OID to a different value: 
	- ``snmpwalk -v2c -c public <Target IP Address> <OID> <New Value>``
-  Command to change the sysContact OID:
	- `` snmpwalk -v2c -c public <Target IP Address> sysContact <New Value>``

#### Enumerating SNMP using Nmap 
-  retrieves a list of all the running SNMP processes along with the associated ports on the target host. 
	- command 
		- `` nmap -sU -p 161 --script=snmp-processes <Target IP Address>`` 
-  Retrieves information regarding SNMP server type and operating system details.
	- command  
		- ``  nmap -sU -p 161 --script=snmp-sysdescr <Target IP Address>``
- Retrieves a list of all the applications running on the target machine.
	- command  
		- `` nmap -sU -p 161 --script=snmp-win32-software <Target IP Address> ``

#### SNMP Enumeration Tools 
- tools like 
	-  snmp-check (snmp_enum Module) 
	- SoftPerfect Network Scanner
	- Network Performance Monitor (https://www.solarwinds.com) 
	- OpUtils (https://www.manageengine.com) 
	- PRTG Network Monitor (https://www.paessler.com) 
	- Engineer’s Toolset (https://www.solarwinds.com)

#### SNMP Enumeration with SnmpWalk and Nmap using AI
- Example #1:  "Perform SNMP enumeration on target IP 10.10.1.22 using SnmpWalk and display the result here”.
	- command 
		- `` snmpwalk -c public -v1 10.10.1.22 ``
- Example #2: ▪ "Perform SNMP enumeration on target IP 10.10.1.22 using nmap and display the result here”.
	- command 
		- ``nmap -sU -p 161 --script snmp-info 10.10.1.22 ``
- Example #3: ▪ "Perform SNMP processes on target IP 10.10.1.22 using nmap and display the result here”.
	- command 
		- `` nmap -sU -p 161 --script snmp-processes 10.10.1.22``


### LDAP Enumeration
- lightweight directory access protocol (LDAP) is an Internet protocol for accessing distributed directory services 

- A client starts a LDAP session by connecting to a directory
system agent (DSA) on TCP port 389 and then sends an operation request to the DSA

- Attackers query the LDAP service to gather information, such as valid usernames, addresses, and departmental details, which can be further used to perform attacks

#### Manual and Automated LDAP Enumeration
##### Manual LDAP Enumeration

- [ ] to do 
##### LDAP Nmap
Attackers use the ldap-brute NSE script to brute-force LDAP authentication. By default, it uses the built-in username and password lists. The userdb and passdb script arguments can be employed to use custom lists. 
-  ``nmap -p 389 --script ldap.base='"cn=users,dc=CEH,dc=com ldap-brute "' <Target IP Address> --script args``

### NTP Enumeration

NTP Enumeration Tools
- nmap (https://nmap.org) 
	- Wireshark (https://www.wireshark.org) 
	- udp-proto-scanner (https://labs.portcullis.co.uk)  
	- NTP Server Scanner (http://www.bytefusion.com)

### NFS Enumeration
NFS is a type of file system that enables users to access, view, store, and update files over a remote server. These remote data can be accessed by the client in the same way it is accessed on the local system. Depending on the privileges assigned to the clients, they can either only read or both read and write the data.
- The remote procedure call (RPC) is used to route and process the request between clients and servers. 
- command 
	- ``rpcinfo -p <Target IP Address> ``
-  other commands and tools to gain access to the NFS server
	- command 
		- ``showmount -e <Target IP Address> ``

- NFS Enumeration Tools 
- RPCScan
	- command 
		- `` python3 rpc-scan.py <Target IP Address> --rpc``
- SuperEnum
- command 
	 ![[Pasted image 20250726154024.png]]

### SMTP Enumeration
ail systems commonly use SMTP with POP3 and IMAP, which enable users to save messages in the server mailbox and download them from the server when necessary. SMTP uses mail exchange (MX) servers to direct mail via DNS. It runs on TCP port 25, 2525, or 587.

- SMTP provides the following three built-in commands.
	1. VRFY: Validates users
	2.  EXPN: Displays the actual delivery addresses of aliases and mailing lists
	3.  RCPT TO: Defines the recipients of the message

##### SMTP Enumeration using Nmap

▪ The following command, when executed, lists all the SMTP commands available in the Nmap directory: 
- ``nmap -p 25, 365, 587 -script=smtp-commands <Target IP Address >``
▪ Run the following command to identify SMTP open relays:
- ``nmap -p 25 -script=smtp-open-relay <Target IP Address>``
▪ Run the following command to enumerate all the mail users on the SMTP server: 
* ``nmap -p 25 –script=smtp-enum-users <Target IP Address>``

##### SMTP Enumeration using Metasploit 
- Steps to Enumerate SMTP Users Using Metasploit 
- Step 1: Launch Metasploit msfconsole and switch to the relevant auxiliary scanner to initiate the process: auxiliary/scanner/smtp/smtp_enum. msf > use auxiliary/scanner/smtp/smtp_enum
-  Step 3: Use the option set RHOST to set the target SMTP server’s IP address or a range of IP addresses.
-  Step 4: By default, the Metasploit framework uses default wordlists located at /usr/share/60etasploit-framework/data/wordlists/unix_users.txt to enumerate SMTP users. The USER _FILE option can be set to use custom wordlists.
	- ``msf auxiliary(smtp_enum) > set USER_FILE <location of wordlists file>``
- step 5: run
##### SMTP Enumeration Tools
- tools such as 
	-  NetScanTools Pro
	- smtp-user-enum 
##### SMTP Enumeration using AI 
- Example #1: ▪ "Perform SMTP enumeration on target IP 10.10.1.19."
	- command 
	- `` map -p25 --script smtp-enum-users --script-args smtp-enum-users.methods={VRFY, EXPN, RCPT} 10.10.1.19 -oN ~/enumeration_results/smtp_enum_10.10.1.19.txt``
- Example #2: ▪ "Perform SMTP enumeration on target IP 10.10.1.19 with Metasploit."
	- command 
		- ``msfconsole -q -x "use auxiliary/scanner/smtp/smtp_enum; set RHOSTS 10.10.1.19; run; exit" ``
### DNS Enumeration

#### DNS Enumeration using Zone Transfer
NS zone transfer is the process of transferring a copy of the DNS zone file from the primary DNS server to a secondary DNS server. 

- to perform DNS  zone transfer we use tools 
	-  dig Command


##### DIG 
- command 
	- ``  dig ns <target domain>``
- attackers use one of the name servers from the output of the above command to test whether the target DNS allows zone transfers. They use the following command for this purpose:
	- command 
		- ``dig @<domain of name server> <target domain> axfr``

#####  nslookup Command
- command 
	- nslookup
	- set querytype=soa 
	- ``<target domain>`` 
- commnad  
	-  The following command is used to attempt to transfer the zone of the specified name server: 
		- ``/ls -d <domain of name server>``

##### DNSRecon 
- command
	-  ``dnsrecon -t axfr -d <target domain> ``
#### DNS Cache Snooping
 DNS cache snooping is a DNS enumeration technique whereby an attacker queries the DNS server for a specific cached DNS record
#####  Non-recursive Method 
- command 
	- `` dig @<IP of DNS server> <Target domain> A +norecurse``
#####  Recursive Method
- command 
	- `` dig @<IP of DNS server> <Target domain> A +recursedig @<IP of DNS server> <Target domain> A +recurse``

#### DNSSEC Zone Walking
-  DNSSEC zone walking is a DNS enumeration technique where an attacker attempts to obtain internal records of the DNS server if the DNS zone is not properly configured
- Attackers use tools, such as LDNS and DNSRecon, to exploit this vulnerability and obtain the network information of a target domain and further launch Internet-based attacks

- DNSSEC Zone Walking Tools
#####  LDNS
- command 
	- `` ldns-walk @<IP of DNS Server> <Target domain>``
####  DNSRecon
- command  
	- `` dnsrecon -d <target domain> -z ``
##### DNS Enumeration using OWASP Amass 
- command 
	- `` amass enum -d <Target Domain>``
Other OWASP Amass commands for DNS Enumeration: ▪ Run the following command to perform a passive enumeration: 
	- ``amass enum -passive -d <Target Domain> -src`` 
- Run the following command to perform an active enumeration through brute-forcing with a specified wordlist: 
	- ``amass enum -active -d <Target Domain> /usr/share/wordlists/amass/all.txt``
-  Run the following command to track or compare the last two enumeration scans performed on the target domain:
	- ``amass track -config /root/amass/config.ini -dir amass4owasp -d <Target Domain> -last 2``
-  Run the following command to display the results of enumeration stored in amass database (amass4owasp):
	- ``amass db -dir amass4owasp -list``
-  Run the following command to create a d3-force HTML visual graph:
	- ``amass viz -d3 -dir amass4owasp``

##### DNS and DNSSEC Enumeration using Nmap
-  Run the following command to list all the available services on the target host:
	- ``nmap --script=broadcast-dns-service-discovery <Target Domain>``
- Execute the following command to retrieve all the subdomains associated with the target host: 
	- ``nmap -T4 -p 53 --script dns-brute <Target Domain>``
-  Execute the following command to retrieve all the subdomains associated with the target host:
	- ``nmap -T4 -p 53 --script dns-brute <Target Domain>``
-  Run the following command to check whether DNS recursion is enabled on the target server: 
	- ``nmap -Pn -sU -p 53 --script=dns-recursion 192.168.1.150``

- DNS Security Extensions (DNSSEC) Enumeration using Nmap 
-  Execute the following command to retrieve the list of subdomains associated with the target domain:
	- ``nmap -sU -p 53 --script dns-nsec-enum --script-args dns-nsec-enum.domains= eccouncil.org <target>``

#### DNS Enumeration with Nmap using AI
- “Use Nmap to perform DNS Enumeration on target domain www.certifiedhacker.com”
	- `` ap --script dns-brute --script-args dns-brute.domain=certifiedhacker.com -oN ~/enumeration_results/dns_brute_certifiedhacker.txt && nmap --script dns-zone-transfer -p 53 certifiedhacker.com ~/enumeration_results/dns_zonetransfer_certifiedhacker.txt ``
### Other Enumeration 
#####  IPsec Enumeration
Psec is the most commonly implemented technology for both gateway-to-gateway (LAN-to-LAN) and host-to-gateway (remote access) enterprise VPN solutions. IPsec provides data security by employing various components such as Encapsulating Security Payload (ESP), Authentication Header (AH), and Internet Key Exchange (IKE) to secure communication between VPN endpoints.

- command 
	- ``  nmap –sU –p 500 <target IP address>``
The following command is used for initial IPsec VPN discovery with ike-scan tool: #
- ``ike-scan –M <target gateway IP address>``
##### VoIP Enumeration
VoIP is an advanced technology that has replaced the conventional public switched telephone network (PSTN) in both corporate and home environments. VoIP uses Internet infrastructure to establish connections for voice calls; data are also transmitted on the same network. However, VoIP is vulnerable to TCP/IP attack vectors. Session Initiation Protocol (SIP) is one of the protocols used by VoIP for performing voice calls, video calls, etc. over an IP network. This SIP service generally uses UDP/TCP ports 2000, 2001, 5060, and 5061.

Below screenshot shows an example for the enumeration of SIP device details using the Svmap tool through the following command: # 
- ``svmap <target network range/IP Address>``

#### RPC Enumeration
• Remote Procedure Call (RPC) allows clients and servers to communicate in distributed client/server programs
• Enumerating RPC endpoints enables attackers to identify any vulnerable services on these service ports

Attackers use the following Nmap scan commands to identify the RPC service running on the network: #
- command 
	- ``nmap -sR <target IP/network>`` 
	- `` nmap -T4 –A <target IP/network>``

 - attackers use tools such as 
	 - NetScanTools Pro

##### Unix/ Linux User Enumeration rusers
- rusers finger
	- Displays a list of users whoare logged on to remotemachines ormachines on local network
	- Syntax: /usr/bin/rusers [-a] [-l] [-u| -h| -i] [Host ...]
- rwho
	- Displays a list of users who are logged on to hosts on the local network
	- Syntax: rwho [ -a]
- finger
	- Displays information about systemusers, suchas loginname, real name, terminal name, idle time, login time, office location, and office phonenumbers 
	- Syntax: finger [-l] [-m] [-p] [-s] [user ...] [user@host ... ]

##### SMB Enumeration

▪ Attackers use SMB enumeration tools, such as Nmap, SMBMap, enum4linux, and nullinux, to perform a directed scan on the SMB service running on port 445
▪ SMB enumeration helps attackers to perform OS banner grabbing on the target
- ``nmap -p 445 -A <target IP>``

 - Nmap commands to enumerate the supported protocols and versions of the target SMB server: #
	 - ``nmap -p 445 –-script smb-protocols <Target IP>``
	 - ``nmap -p 139 –-script smb-protocols <Target IP>``

###### SMB Enumeration with AI
-  “Scan the target IP 10.10.1.22 for the port using SMB with nmap”.
	- command 
		- `` nmap -p 445 --script smb-enum-shares 10.10.1.22``

##### Create and Run Custom Script to Automate Network Enumeration Tasks with AI
- → “Develop and execute a script that will automate network enumeration tasks on target IP range 10.10.1.0/24”.



### NMap Scripts list for Enumerations 

| Protocols                   | SYNTAX                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NetBIOS                     | ``map -sV -v --script nbstat.nse <target IP address>``                                                                                                                                                                                                                                                                                                      |
| SNMP                        | ``nmap -sU -p 161 --script snmp-info 10.10.1.22 ``<br>`` nmap -sU -p 161 --script=snmp-processes <Target IP Address>``<br>``nmap -sU -p 161 --script=snmp-sysdescr <Target IP Address>``<br>``nmap -sU -p 161 --script=snmp-win32-software <Target IP Address>``                                                                                            |
| LDAP                        | ``nmap -p 389 --script ldap.base='"cn=users,dc=CEH,dc=com ldap-brute "' <Target IP Address> --script args``<br>                                                                                                                                                                                                                                             |
| SMPT                        | ``nmap -p 25, 365, 587 -script=smtp-commands <Target IP Address >``<br>``nmap -p 25 -script=smtp-open-relay <Target IP Address>``<br>``nmap -p 25 –script=smtp-enum-users <Target IP Address>``                                                                                                                                                             |
| DNS <br><br>&<br><br>DNSSEC | ``nmap --script=broadcast-dns-service-discovery <Target Domain>``<br>``nmap -T4 -p 53 --script dns-brute <Target Domain>``<br>``nmap -T4 -p 53 --script dns-brute <Target Domain>``<br>``nmap -Pn -sU -p 53 --script=dns-recursion 192.168.1.150``<br>``nmap -sU -p 53 --script dns-nsec-enum --script-args dns-nsec-enum.domains= eccouncil.org <target>`` |
| SMB                         | ``nmap -p 445 –-script smb-protocols <Target IP>``<br>``nmap -p 139 –-script smb-protocols <Target IP>``<br>`` nmap -p 445 --script smb-enum-shares <Target IP>``                                                                                                                                                                                           |

### References

Nbtstat Utility 
- ADD table here 
- make table about protocalls that runs in port numbers 
 