2025-08-01 22:28

Status:

Tags:

# Sniffing (Concepts )

### Network Sniffing
![[Pasted image 20250801222947.png]]
![[Pasted image 20250801223008.png]]

Types of Sniffing
-  Passive sniffing 
- ![[Pasted image 20250801223059.png]]
- Active sniffing
The following is a list of different active sniffing techniques: ▪ MAC flooding ▪ DNS poisoning ▪ ARP poisoning ▪ DHCP attacks ▪ Switch port stealing ▪ Spoofing attack

### ARP Spoofing/Poisoning Tools
here we use arpspoof 
- syantx 
	- `` arpspoof –i [Interface] –t [Target Host]``
		- `` arpspoof -i eth0 -t 10.10.1.13 10.10.1.11

# Lab 1: Perform Active Sniffing
## Task 1: Perform MAC Flooding using macof
1. open wireshark and select eth0
2. open terminal as sudo user 
	- run command in root directory
	- ``macof -i eth0 -n 10``
3. done and check in wireshark 

## Task 2: Perform a DHCP Starvation Attack using Yersinia
uses 68 port to perform 
1. open wireshark and select eth0
2. open terminal as sudo user 
	- run command in root directory
3. to open Yersinia in interactive mode.
		- ``yersinia -I ``
	- press **h** for help.
	-  to select DHCP mode. In DHCP mode
		- press `` F2``  ``
	- to list available attack options
	- press `` x``
	-  to start a DHCP starvation attack.
		- `` 1``
4. done and check on wireshark 

# Lab 2: Perform Network Sniffing using Various Sniffing Tools

## Task 1: Perform Password Sniffing using Wireshark
- we will use windows server  2019
1. open sireshark on windows 2019 and start capturing
2. open windows 11
	- Open any web browser, and go to ``http://www.moviescope.com/``
	- login as `` sam:test``
3. **Apply a display filter field**, type ``http.request.method == POST``
	-  navigate to **Edit** --> **Find Packet** from menu bar.
	- Click **Display filter**, select **String** from the drop-down options, click **Narrow & Wide** and select **Narrow (UTF-8 / ASCII)** from the drop-down options and click **Packet list**, select **Packet details** from the drop-down options.
    - In the field next to **String**, type **pwd** and click the **Find** button.
4. open remote desktop app
	- type ip=``10.10.1.11``
	- ``Jason:qwerty``
5. open control panel
	- system  and security -> windows tools -> services 
	- select remote capture protocol and start 
6. open wireshark 
	- click on capture options -> manage interface
	- click on remote interfaces 
	- click on ``+``
	- enter ``ip:10.10.1.11`` and ``port:2002`` \
	- select the **Password authentication** 
		- enter Jason:qwerty
7. open windows 11 as Jason
	- go to ``http://www.goodshopping.com``
	- open wireshark 
	- done 
# Lab 3: Detect Network Sniffing
## Task 1: Detect ARP Poisoning and Promiscuous Mode in a Switch-Based Network

1. open windows 2019 server 
	- search ``cain``
	- click on configure
	- clcik on ``start/stop`` as in second icon 
	- click on sniffer tacb -> click on ``+`` icon 
	- select  ``Scan MAC Addresses``
	- Select the **All Tests** checkbox; then, click **OK**.
	- click the **APR** tab at the bottom of the window.
	- click and start/stop arp 
	- add new ARP poison routing 
	- select  ``10.10.1.11`` from left and ``10.10.1.13`` from right  
2. open parrot  
	-  open terminal 
	- `` sudo su hping3 -c 100000``
3. open windows server 2019
	- open wireshark 
		- click on edit -> preferences
		- click ``ARP/RAP`` 
		- select ``Detect ARP request storms``
		-   **Wireshark** begins to capture the traffic between the two machines
			- switch cain
		- **Stop packet capturing** on wireshark 
		- click ``Analyze`` and select  ``Expert Information``
		- click **Duplicate IP address configured** (running ARP/)
4.  we shall perform promiscuous mode detection using Nmap.
- open Ubuntu 
	- ``nmap --script=sniffer-detect <ip> ``
### References
- [x] make wireshark display filters list or cheatsheet
- [ ]  