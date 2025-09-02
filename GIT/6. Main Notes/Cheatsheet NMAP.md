# Cheatsheet NMAP(M3)

## Default

1. nmap will perfrom host discovery before port scan
2. namp will perform port scan on common 1000 ports
-  -sn As user - 
	- TCP SYN 80 & SYN 443(connect scan ) 
*  As root - 
	* ARP (local network ) - TCP SYN 433, ACK 80, ICMO echo request, ICMP timestamp request
	* To see service runnig netstat -antp. gh

## Nmap port info (status)
* Open - Application on the target machine is listening for connections/packets.
* Closed - No application is listening on these ports (though they could open up at any time).
* Filtered - A firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed.
* Unfiltered - Responding to Nmap's probes, but Nmap cannot determine whether they are open or closed.
* open filtered and closed filtered when nmap cannot determine which of the two states describe a port.
* slow scan means it can be firewall 

## Nmap extensions list

| Nmap extensions list                       | use case                                         |
| ------------------------------------------ | ------------------------------------------------ |
| --resson                                   | gives rea                                        |
| --vv (verbose)                             | verbose                                          |
| -Pn                                        | skips host machine                               |
| -n                                         | skips DNS                                        |
| -p                                         | specifies port                                   |
| -p-                                        | all ports                                        |
| -F                                         | fast Scan                                        |
| --top-ports 5(numbers )                    | specifies top ports                              |
| -T<0-5>  <br>-T0 (slow)  <br>-T4  <br>- T5 | how fast scan you want                           |
| -sV                                        | service version detection                        |
| -sC                                        | default scripts                                  |
| --open                                     | shows only open ports                            |
| -sn                                        | (No port scan) Ping scan to discover live hosts. |
  
| Scans        | SYNTAX | OPEN    | ClOSED |
| ------------ | ------ | ------- | ------ |
| ARP scan     | -sn    |         |        |
| connect scan | -sT    | SYN/ACK | RST    |
| SYN Scan     | -sS    | SYN/ACK | RST    |
| NULL sacn    | -sN    | -       | RST    |
| FIN Scan     | -sF    | -       | RST    |
| Xmas scan    | -sX    | -       | RST    |

| -A                             | Aggressive scan |     |     |
| ------------------------------ | --------------- | --- | --- |
| ACK or Firewall detection Scan | -sA             | -   | RST |
| UDP Scan                       | -sU             |     |     |
| OS detection Scan              | -O              |     |     |
## Common nmap commands 
- `` sudo nmap -sS -Pn - p80 <IP>`` (SYN Scan)
- `` nmap -Pn -n <IP>`` (Connect Scan)
- ``sudo map -Pn -n <IP>`` (SYN Scan)
- ``nmap - Pn -n -p21,22,80 <I>`` (Connect Scan)
* `` nmap - p10-100 <IP>`` (range)
- ``sudo nmap -p--sT example.com``
- `` nmap <publicip>``(no ARP)
- ``sudo nmap -Pn -sV 10.10.10.6`` (-sV service version detection )

# main
Host discovery 

| Scans                     | SYNTAX | OPEN | ClOSED |
| ------------------------- | ------ | ---- | ------ |
| ARP                       | -PR    |      |        |
| UDP                       | -PU    |      |        |
| ICMP Ping Scan            | -PE    |      |        |
| ICMP Timestamp Ping Scan  | -PP    |      |        |
| ICMP Address Mask Ping Sc | -PM    |      |        |
| TCP SYN Ping Scan         | -PS    |      |        |
| TCP ACK Ping Scan         | -PA    |      |        |
| IP Protocol Ping Scan     | -PO    |      |        |
Port scan 

| Scans                                                                                           | SYNTAX                                  | OPEN        | ClOSED       |
| ----------------------------------------------------------------------------------------------- | --------------------------------------- | ----------- | ------------ |
| TCP Connect/Full-open Scan                                                                      | -sT                                     |             |              |
| Stealth Scan (Half-Open Scan)                                                                   | -sS                                     |             |              |
| Inverse TCP Flag Scan <br>       Xmas Scan <br>	   FIN Scan<br>	   Null Scan<br>	   Maimon Scan | <br>-sX<br>-sF<br>-sN<br>-sM<br>        |             |              |
| ACK Flag Probe Scan<br>       TTL-Based ACK Flag Probe scanning                                 | <br>-sW<br>                             |             |              |
| IDLE/IPID Header Scan                                                                           | `` -Pn -p- -sI <spoof ip> <target ip>`` |             |              |
| UDP Scan                                                                                        | -sU                                     | No response | unreachable  |
| SCTP INIT Scan                                                                                  | -sY                                     |             |              |
| SCTP COOKIE ECHO Scan                                                                           | -sZ                                     |             |              |
| List Scan                                                                                       | -sL                                     |             |              |
| IPv6 Scan                                                                                       | -6                                      |             |              |
| ACK scans                                                                                       | -sA                                     |             |              |
Service Version Discovery

| Scans           | SYNTAX | OPEN | ClOSED |
| --------------- | ------ | ---- | ------ |
| Service Version | -sV    |      |        |
OS Discovery

| Scans        | SYNTAX | OPEN | ClOSED |
| ------------ | ------ | ---- | ------ |
| OS Discovery | -O     |      |        |
OS Discovery Scripts 

| Scans        | SYNTAX                                    | OPEN | ClOSED |     |
| ------------ | ----------------------------------------- | ---- | ------ | --- |
| SMB script   | ``nmap --script smb-os-discovery <ip>  `` |      |        |     |
| NetBIOS (Eu) | ``nmap -sV -v --script nbstat.nse``       |      |        |     |
packet Fragmentation

| supported scan for fragmented IP | SYNTAX | OPEN | ClOSED |
| -------------------------------- | ------ | ---- | ------ |
| SYN/FIN                          | -sS -f |      |        |
| UDP Scan                         | -sU -f |      |        |
| NULL                             | -sN -f |      |        |
| FIN                              | -sF -f |      |        |
| XMAS                             | -sX -f |      |        |
| ACK scans                        | -sA -f |      |        |

IP Address Decoy

| supported scan for IP Address Decoy | SYNTAX                        | OPEN | ClOSED |     |
| ----------------------------------- | ----------------------------- | ---- | ------ | --- |
| SYN/FIN                             | -sS  ``nmap -D RND: 10 <ip>`` |      |        |     |
| UDP Scan                            | -sU ``nmap -D RND: 10 <ip>``  |      |        |     |
| NULL                                | -sN ``nmap -D RND: 10 <ip>``  |      |        |     |
| FIN                                 | -sF ``nmap -D RND: 10 <ip>``  |      |        |     |
| XMAS                                | -sX ``nmap -D RND: 10 <ip>``  |      |        |     |
| ACK scans                           | -sA ``nmap -D RND: 10 <ip>``  |      |        |     |

subnet Scan 
 - ``nmap -A [Target Subnet]** (here, target subnet is 10.10.1.*``
	 - or
 - `` nmap -A 10.10.10.1/24``

 (here, target IP address is **10.10.1.11**).

 In this command, **-mtu**: specifies the number of Maximum Transmission Unit (MTU) (here, **8** bytes of packets).
 - command
	 - ``nmap -mtu 8 <ip>`` 


