2025-07-24 22:41

Status:

Tags:

# Scanning Networks (concept)
### Network Scanning Concepts
- Network scanning refers to a set of procedures used for identifying hosts, ports, and services in a network
- Attackers use tools such as Nmap, Hping3, Metasploit, and NetScanTools Pro to perform network scanning
 
### Types of Scanning 
- types of scanning
	- port scanning 
	- Network Scanning 
	- vulnerability scanning 

###  TCP Communication Flags 
 Six TCP control flags manage the connection between hosts and give instructions to the system. Four of these flags (SYN, ACK, FIN, and RST) govern the establishment, maintenance, and termination of a connection. The other two flags (PSH and URG) provide instructions to the system. The size of each flag is 1 bit. As there are six flags in the TCP Flags section, the size of this section is 6 bits. When a flag value is set to “1,” that flag is automatically turned on.
- Types of TCP flags 
	- SYN
	- ACK 
	- FIN
	- RST (6 bites)  
	- PSH
	- URG(1 bites )

- Synchronize or “SYN”: It notifies the transmission of a new sequence number. This flag generally represents the establishment of a connection (three-way handshake) between two hosts.
-  Acknowledgement or “ACK”: It confirms the receipt of the transmission and identifies the next expected sequence number. When the system successfully receives a packet, it sets the value of its flag to “1,” thus implying that the receiver should pay attention to it.
-  Push or “PSH”: When it is set to “1,” it indicates that the sender has raised the push operation to the receiver; this implies that the remote system should inform the receiving application about the buffered data coming from the sender. The system raises the PSH flag at the start and end of data transfer and sets it on the last segment of a file to prevent buffer deadlocks.
-  Urgent or “URG”: It instructs the system to process the data contained in packets as soon as possible. When the system sets the flag to “1,” priority is given to processing the urgent data first and all the other data processing is stopped.
-  Finish or “FIN”: It is set to “1” to announce that no more transmissions will be sent to the remote system and the connection established by the SYN flag is terminated.
-  Reset or “RST”: When there is an error in the current connection, this flag is set to “1” and the connection is aborted in response to the error. Attackers use this flag to scan hosts and identify open ports.
![TCP/IP 3 Way handshake for client-server communication on Internet](https://lh7-us.googleusercontent.com/0f9ILAa6xCmdJre8rmlopHCX_aclNQmIlq1IPbmCL4YESypVnr6QuKhawMHGySNBlyD2sw9kRcYJ9IIByRywyM0lThXAj_QPrfLOmSP0Yk4hfa_zWvR4_8f-ChpBeDAwQs5_eJoUoskMeHaVSZIi3Fk)


### Scanning Tools
- we use scanning tools such as 
	- Nmap
	- Hping3
	- Zenmap 
	- Metasploit 
	- NetScanTools Pro
	- sx (https://github.com) 
	- RustScan (https://github.com) 
	- MegaPing (http://magnetosoft.com) 
	- SolarWinds®Engineer's Toolset (https://www.solarwinds.com) 
	- PRTG Network Monitor (https://www.paessler.com)
### Host Discovery
-  Host Discovery Techniques

-  ARP Ping Scan 
- UDP Ping Scan 
- ICMP Ping Scan o
	- ICMP ECHO Ping 
	-  ICMP ECHO Ping Sweep
		- ICMP Timestamp Ping 
		- ICMP Address Mask Ping
-  TCP Ping Scan
	- TCP SYN Ping 
	- TCP ACK Ping
- IP Protocol Scan

####  ARP Ping Scan
- ![[Pasted image 20250724231016.png]]
- command for ARP scan
	- `` namp -PR  -sn <ip>  (-sn no port scan )
#### UDP Ping Scan 
![[Pasted image 20250724232446.png]]
- command for UDP ping scan 
	- `` sudo nmap  -sn -PU 192.168.0.114 `` ``
#### ICMP ECHO Ping Scan
![[Pasted image 20250724233004.png]]
- command for ICMP ECHO Ping Scan 
	- ``sudo nmap  -PE -sn  192.168.0.114
`
#### ICMP ECHO Ping Sweep 
![[Pasted image 20250724233304.png]]
-  ICMP ECHO Ping sweep is used for  wide rage of IP
- command for ICMP ECHO ping sweep 
	- `` nmap -PE -sn 10.10.10.1/24``
####  ICMP Timestamp Ping Scan
 the attackers query a timestamp message to acquire the information related to the current time from the target host machine.
- command for ICMP Timestamp ping Scan  
	- `` nmap -PP -sn 10.10.10.1``
#### ICMP Address Mask Ping Scan
 where the attackers send an ICMP address mask query to the target host to acquire information related to the subnet mask.
- command for ICMP Address Mask Ping Scan
	- `` nmap -PM -sn 10.10.10.1``
#### TCP SYN Ping Scan
![[Pasted image 20250724234142.png]]
- command for TCP SYN Ping Scan
	- `` nmap -PS -sn 10.10.10.1``

#### TCP ACK Ping Scan
![[Pasted image 20250724234441.png]]
- command for TCP SYN Ping Scan
	- `` nmap -PA -sn 10.10.10.1``
#### IP Protocol Ping Scan 
![[Pasted image 20250724234557.png]]
- command for IP Protocol Ping Scan
	- `` nmap -PO -sn 10.10.10.1``

####  Host Discovery with AI 
- Example #1: An attacker can use ChatGPT to perform this task by using an appropriate prompt such as: “Scan the target network 10.10.1.0/24 for active hosts and place only the IP addresses into a file scan1.txt”
- command 
	-  ```nmap -sn 10.10.1.0/24 -OG -| awk '/Up$/{print $2}' > scan1.txt ``

- Example #2: An attacker can use ChatGPT to perform this task by using an appropriate prompt such as: “Run a fast but comprehensive Nmap scan against scan1.txt with low verbosity and write the results to scan2.txt”
- command 
	-  ``nmap -T4 -iL scan.txt -oN scan2.txt -v0``

- Example #3: Attackers can leverage AI-powered technologies to enhance and automate host discovery tasks. With the aid of AI, attackers can effortlessly find out the live hosts on a target with the help of Nmap.
- command 
	- `` `nmap -sn -PE 10.10.1.0/24``

#### Ping Sweep Tools 
- Angry IP Scanner
- SolarWinds Engineer’s Toolset (https://www.solarwinds.com) 
- NetScanTools Pro (https://www.netscantools.com) 
- Colasoft Ping Tool (https://www.colasoft.com) 
- Advanced IP Scanner (https://www.advanced-ip-scanner.com) 
- OpUtils (https://www.manageengine.com)
### Port and Service Discovery
- common list of ports  (for full refer 319 material )

| **Application** | **Port Number** | **Full forms**                                         |
| --------------- | --------------- | ------------------------------------------------------ |
| FTP             | 20/21           | File Transfer Protocol - (Data Transfer) / (Control)   |
| SSH             | 22              | Secure Shell                                           |
| Telnet          | 23              | Telnet                                                 |
| SMTP            | 25              | Simple Mail Transfer Protocol                          |
| DNS             | 53              | Domain Name System                                     |
| DHCP            | 67/68           | Dynamic Host Configuration Protocol (Server)/ (Client) |
| HTTP            | 80              | Hypertext Transfer Protocol                            |
| POP3            | 110             | Post Office Protocol version 3                         |
| NTP             | 123             | Network Time Protocol                                  |
| IMAP            | 143             | Internet Message Access Protocol                       |
| SNMP            | 161             | Simple Network Management Protocol                     |
| SNMP Trap       | 162             | SNMP Trap                                              |
| HTTPS           | 443             | HTTP Secure - Encrypted Web Communication              |

#### Port Scanning Techniques
- TCP Scanning: 
	- Open TCP Scanning Methods 
		- TCP Connect/Full-open Scan
-  Stealth TCP Scanning Methods o
	- Half-open Scan 
	- Inverse TCP Flag Scan 
		- Xmas Scan 
		- FIN Scan 
		- NULL Scan 
		- Maimon Scan
	- ACK Flag Probe Scan 
		- TTL-Based Scan 
		- Window-Based Scan
-  Third Party and Spoofed TCP Scanning Methods 
	- IDLE/IP ID Header Scan
- UDP Scanning: 
	- UDP Scanning
- SCTP Scanning: 
	- SCTP INIT Scanning 
	- SCTP COOKIE/ECHO Scanning
- SSDP Scanning: 
	- SSDP and List Scanning
- IPv6 Scanning: 
	- IPv6 Scanning
#### TCP Connect/Full-Open Scan 
![[Pasted image 20250725123843.png]]
- command for TCP Connect/Full-open Scan 
	-  ```nmap -sT <ip>```

#### Stealth Scan (Half-Open Scan) 
![[Pasted image 20250725124539.png]]
- command for Stealth Scan (Half-openScan) 
	-  ```nmap -sS <ip>```

#### Inverse TCP Flag Scan
Attackers send TCP probe packets with a TCP flag (FIN, URG, PSH) set or with no flags.
![[Pasted image 20250725124930.png]]
- command for Inverse TCP Flag Scan 
	- `` nmap -sF 192.168.1.100    # FIN scan
	- ``nmap -sN 192.168.1.100    # NULL scan ``
	- ``nmap -sX 192.168.1.100    # XMAS scan``
##### Xmas Scan
![[Pasted image 20250725125322.png]]
- command for Inverse Xmas Scan 
	-  ``nmap -sX 192.168.1.100    # XMAS scan``
##### TCP Maimon Scan
![[Pasted image 20250725125921.png]]
- command for Inverse TCP Maimon Scan 
	-  ``nmap -sM 192.168.1.100 ``
#### ACK Flag Probe Scan 
Attackers send TCP probe packets with the ACK flag set to a remote device and then analyze the header information (TTL and WINDOW field) of the received RST packets to find out if the port is open or closed. The ACK flag probe scan exploits the vulnerabilities within the BSD-derived TCP/IP stack. Thus, such scanning is effective only on those OSs and platforms on which the BSD derives TCP/IP stacks. 
##### TTL-Based ACK Flag Probe scanning
![[Pasted image 20250725130542.png]]
- **If the TTL value in the RST packet is less than 64**, the port is considered **open**.
- If the TTL value is **greater than or equal to 64**, the port is considered **closed**.

- command for TTL-Based ACK Flag Probe scanning
	- ``nmap –ttl [time] [target]``
#####  Window-Based ACK Flag Probe scanning
![[Pasted image 20250725131921.png]]
- command for Window-Based ACK Flag Probe scanning
	- ``nmap -sW <ip>``
![[Pasted image 20250725132001.png]]
![[Pasted image 20250725132017.png]]

#### IDLE/IPID Header Scan
The IDLE/IPID header scan is a TCP port scan method that can be used to send a spoofed source address to a computer to determine what services are available. 
- command for IDLE/IPID Header scan  
	- `` nmap -Pn -p- -sI <spoof ip> <target ip>> ``

#### UDP Scan
-  UDP Raw ICMP Port Unreachable Scanning
![[Pasted image 20250725133514.png]]
- command for UDP Raw ICMP Port Unreachable Scanning 
	- `` nmap -sU <ip>``
#### SCTP INIT Scan 
Stream Control Transport Protocol (SCTP) is a reliable message-oriented transport layer protocol. It is used as an alternative to the TCP and UDP protocols, as its characteristics are similar to those of TCP and UDP. 
![[Pasted image 20250725134220.png]]
![[Pasted image 20250725134235.png]]
![[Pasted image 20250725134247.png]]
- command for SCTP INIT Scan 
	- `` nmap -sY <ip> ``

#### SCTP COOKIE ECHO Scan
SCTP COOKIE ECHO scan is a more advanced type of scan. In this type of scan, attackers send the COOKIE ECHO chunk to the target, and if the target port is open, it will silently drop the packets onto the port and you will not receive any response from the target. If the target sends back the ABORT chunk response, then the port is considered as a closed port. The COOKIE ECHO chunk is not blocked by non-stateful firewall rule sets as in the INIT scan. Only an advanced IDS can detect the SCTP COOKIE ECHO scan.

![[Pasted image 20250725134527.png]]
- command for SCTP COOKIE ECHO Scan
	- `` nmap -sZ <ip> ``
#### SSDP and List Scan
##### SSDP Scan
- Simple Service Discovery Protocol (SSDP) is a network protocol that generally communicates with machines when querying them with routable IPv4 or IPv6 multicast addresses. The SSDP service controls communication for the Universal Plug and Play (UPnP) feature. It generally works when the machine is not firewalled; however, it can sometimes work through a firewall. The SSDP service will respond to a query sent over IPv4 or IPv6 broadcast addresses. This response includes information about the UPnP feature associated with it. The attacker uses SSDP scanning to detect UPnP vulnerabilities that may allow him/her to launch buffer overflow or DoS attacks.
##### List Scan
 a list scan, the discovery of the active network host is indirect. A list scan simply generates and prints a list of IPs/Names without actually pinging or scanning the hosts. As a result, the list scan shows all IP addresses as “not scanned” (0 hosts up).
- command for List Scan
	- `` nmap -sL <ip> ``

#### IPv6 Scan

- command for IPV6 Scan  
	- ``sudo nmap -6 -sV <target IPv6 address or hostname>``

#### Port Scanning with AI 
Example: 1 
“Use Nmap to find open ports on target IP 10.10.1.11”

Example: 2
“Perform stealth scan on target IP 10.10.1.11 and display the results”

Example: 3
“Perform an XMAS scan on target IP 10.10.1.

Example: 4
“Use Nmap to scan for open ports and services against a list of IP addresses in scan1.txt and copy only the port, service and version information with the respective IP address to a new file called scan3.txt

Example: 5
"Use Metasploit to discover open ports on the IP address 10.10.1.22"

### Service Version Discovery

- command for Service Version Discovery
	- ``sudo nmap -6 -sV <ip>``

#### Service Version Discovery with AI
- Example: 1
"Use Nmap to scan open ports, MAC details, services running on open ports with their versions on target IP 10.10.1.11"
- command 
	- `` nmap -sV --reason -v -sT 10.10.1.11``
### Nmap Scan Time Reduction Technique

### OS Discovery (Banner Grabbing/OS Fingerprinting)
How to Identify Target System OS
![[Pasted image 20250725141032.png]]
OS Discovery using Wireshark 
To identify the target OS, sniff/capture the response generated from the target machine to the request-originated machine using packet-sniffing tools such as Wireshark, etc., and observe the TTL and TCP window size fields in the first captured TCP packet. By comparing these values with those in the above table, you can determine the target OS that has generated the response
- use above table to check TTL value to see OS 
#### OS Discovery using Nmap and Unicornscan
OS Discovery using Nmap 
- command for OS Discovery 
	- `` nmap -O 10.10.1.11``

#### OS Discovery using Unicornscan
In Unicornscan, the OS of the target machine can be identified by observing the TTL values in the acquired scan result. 
-  Command for OS Discovery using Unicornscan
	 - ``unicornscan <target IP address>`` 

#### OS Discovery using Nmap Script Engine
Nmap, ``smb-os-discovery`` is an inbuilt script used for collecting OS information on the target machine through the SMB protocol.  If the custom scripts are to be specified, then attackers can use the ``--script option``.
-  Command for OS Discovery using using Nmap Script Engine
	 - ``nmap --script smb-os-discovery <ip>  # SMB-OS  `` 

#### OS Discovery using IPv6 Fingerprinting 
-  Command for OS Discovery IPv6 Fingerprinting 
	 - ``nmap -6 -O <ip>>`` 


#### OS Discovery with AI
- Example #1: Use TTL to identify the operating system running on the target IP address 10.10.1.11
- Command 
	- ping -c 1 10.10.1.11 && echo "Check the TTL value from the response to infer the OS (Linux/Unix: 64, Windows: 128)"

- Example #2: Use TTL to identify the operating system running on the target IP address 10.10.1.9
- commnad 
	- ping -c 1 10.10.1.9 | grep "ttl

- Example #3: "Use Nmap script engine to perform OS discovery on the target IP addresses in scan1.txt"
- command 
	- nmap -iL scan1.txt -O --script=default --script-args=newtargets -oN os_discovery_results.txt

#### Create and Run Custom Script to Automate Network Scanning Tasks with AI

"Develop a script that will automate network scanning efforts and find out live systems, open ports, running services, service versions, etc. on target IP range 10.10.1.0/24"


### Scanning Beyond IDS and Firewall
- attackers can send intended packets to the target that evade the IDS/firewall by implementing the following techniques: 
	- Packet Fragmentation 
	- Source Routing 
	- Source Port Manipulation 
	- IP Address Decoy 
	- IP Address Spoofing 
	- MAC Address Spoofing 
	- Creating Custom Packets 
	- Randomizing Host Order 
	- Sending Bad Checksums 
	- Proxy Servers 
	- Anonymizers

#### Packet Fragmentation
Packet fragmentation refers to the splitting of a probe packet into several smaller packets (fragments) while sending it to a network. When these packets reach a host, the IDS and firewalls behind the host generally queue all of them and process them one by one. However, since this method of processing involves greater CPU and network resource consumption, the configuration of most IDS cause them to skip fragmented packet

##### SYN/FIN Scanning Using IP Fragments
![[Pasted image 20250725145345.png]]
- command 
	- ``nmap -sS -T4 -A -f -v  192.168.0.103``
	- ``-f IP Fragments # ``

#### Source Routing 
**Source Routing** is a networking technique that allows the sender of a packet to specify the exact route that the packet should take through the network, instead of letting routers decide the path automatically. This can be useful for diagnostic or testing purposes, but it is often considered a security risk because it can be manipulated to bypass security controls or redirect traffic in unintended ways.
![[Pasted image 20250725151315.png]]

#### Source Port Manipulation
- Source port manipulation refers to manipulating actual port numbers with common port numbers in order to evade an IDS or firewall
- It occurs when a firewall is configured to allow packets from well-known ports like HTTP, DNS, FTP, etc. 
- Nmap uses the -g or --source-port options to perform source port manipulation
![[Pasted image 20250725151803.png]]
- -g or --source-port is used in nmap
- command 
	- `` nmap -g 80 <ip>``

In this command, **-mtu**: specifies the number of Maximum Transmission Unit (MTU) (here, **8** bytes of packets).
 - command
	 - ``nmap -mtu 8 <ip>``

#### IP Address Decoy
-  IP address decoy technique refers to generating or manually specifying the IP addresses of decoys in order to evade an IDS or firewall
-  It appears to the target that the decoys as well as the host(s) are scanning the network
- This technique makes it t difficult for the IDS or firewall to determine which IP address was actually scanning the network and which IP addresses were decoys

you can perform two types of decoy scans using Nmap:

1. ``nmap -D RND:10 [target]``
- Using this command, Nmap automatically generates a random number of decoys for the scan and randomly positions the real IP address between the decoy IPs. 
	- command 
		- ``  nmap -D RND: 10 10.10.10``

2. ``nmap -D decoy1,decoy2,decoy3,...,ME,... [target]``
- Using this command, you can manually specify the IP addresses of the decoys to scan the victim’s network.
- command 
	- ``  nmap -D 192.168.0.1,172.120.2.8,192.168.2.8,10.10.1.19,10.10.1.5 10.10.1.11``

#### IP Address Spoofing 
IP spoofing using Hping3: 
- command 
	- ``Hping3  -a <spoof ip>  <target ip> ``
#### MAC Address Spoofing
- The MAC address spoofing technique involves spoofing a MAC address with the MAC address of a legitimate user on the network
- Attackers use the --spoof-mac Nmap option to set a specific MAC address for the packets to evade firewall
Performing MAC Address Spoofing to Scan Beyond IDS and Firewall Using Nmap: 
- Attackers use the --spoof-mac Nmap option to choose or set a specific MAC address for packets and send them to the target system/network. 
- command 
	- `` nmap -sT -Pn --spoof-mac 0 [Target IP]``
		- or 
	- ``  nmap -sT -Pn --spoof-mac [Vendor] [Target IP] ``
 

#### Creating Custom Packets
- Creating Custom Packets by using Packet Crafting Tools
- Attackers create custom TCP packets using various packet crafting tools like 
	- Colasoft Packet Builder
	- NetScanTools Pro
##### Colasoft Packet Builder 
- [ ] To do up 

#### Randomizing Host Order and Sending Bad Checksums
##### Randomizing Host Order 
The attacker scans the number of hosts in the target network in a random order to scan the intended target that is lying beyond the firewall. The option used by Nmap to scan with a random host order is --randomize-hosts
- command 
	- `` nmap --randomize-hosts <ip>

##### Sending Bad Checksums
The attacker sends packets with bad or bogus TCP/UDP checksums to the intended target to avoid certain firewall rule sets. TCP/UDP checksums are used to ensure data integrity. Sending packets with incorrect checksums can help attackers to acquire information from improperly configured systems by checking for any response. If there is a response, then it is from the IDS or firewall, which did not verify the obtained checksum. If there is no response or the packets are dropped, then it can be inferred that the system is configured. This technique instructs Nmap to send packets with invalid TCP, UDP, or SCTP checksums to the target host. The option used by Nmap is --badsum.
- command 
	- `` nmap  --badsum <ip>``

#### Proxy Servers
![[Pasted image 20250725155117.png]]


#### Proxy Chaining
![[Pasted image 20250725155202.png]]
- Proxy Tools 
	-  Proxy Switcher 
	- CyberGhost VPN 
#### Anonymizers
Anonymizer tools use various techniques such as SSH, VPN, and HTTP proxies, which allow access to blocked or censored content on the Internet with advertisements omitte
- tools such as
	-  Whonix 
	-  Psiphon (https://psiphon.ca) 
	- TunnelBear (https://www.tunnelbear.com) 
	- Invisible Internet Project (I2P) (https://geti2p.net) 
	- Bright Data Proxy API (https://brightdata.com)
#### Censorship Circumvention Tools
- AstrillVPN
- Tails





### References
