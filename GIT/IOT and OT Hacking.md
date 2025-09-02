2025-08-20 16:12

Status:

Tags:

# IOT and OT Hacking
- **IoT** stands for **_Internet of Things_**: a network of physical devices (e.g., smart thermostats, cameras, sensors, vehicles, home appliances) connected to the internet, capable of collecting, sending, and receiving data.
- **OT** stands for **_Operational Technology_**: hardware and software used to control and monitor industrial equipment, processes, and critical infrastructure (e.g., power plants, factories, water treatment facilities).
## IOT  Hacking
### IOT Architecture 

![[Pasted image 20250820161626.png]]
### IoT Technologies and Protocols
![[Pasted image 20250820161809.png]]
### Security issues of IOT Arc
![[Pasted image 20250820161902.png]]


### Hacking IoT Devices: General Scenario 
![[Pasted image 20250820162324.png]]

### DDoS Attack
![[Pasted image 20250820162423.png]]
### Exploit HVAC
Many organizations use Internet-connected heating, ventilation, and air conditioning (HVAC) systems without implementing security mechanisms, giving attackers a gateway through which to hack corporate systems. 
![[Pasted image 20250820162532.png]]

### Rolling Code Attack 
-  Most smart vehicles use smart locking systems that involve the transmission of an RF signal in the form of a code from a modern key fob, which locks or unlocks the vehicle, to the receiver in the vehicle
- This code that locks or unlocks a vehicle or garage is called a Rolling Code or Hopping Code
- The attacker uses a jammer to thwart the transmission of a code
- After obtaining the code, the attacker can use it to unlock and steal the vehicle
![[Pasted image 20250820162655.png]]
### BlueBorne Attack

-  A BlueBorne attack is performed on Bluetooth connections to gain access and take full control of the target device 
- It is a collection of various techniques based on the known vulnerabilities of the Bluetooth protocol
- BlueBorne is compatible with all software versions and does not require any user interaction, precondition, or configuration, except that the Bluetooth should be activated
- After gaining access to a device, the attacker can penetrate any corporate network using that device to steal critical information about the organization and spread malware to nearby devices
![[Pasted image 20250820162805.png]]
### IoT Malware 
- KmsdBot
-  WailingCrab 
- P2PInfect 
-  NKAbuse 
- IoTroop 
- XorDdos

## IoT Hacking Methodology
IoT Hacking Methodology The following are the different phases in hacking an IoT device: ▪ Information Gathering 
- Vulnerability Scanning 
- Launch Attacks 
- Gain Remote Access 
- Maintain Access
### Information Gathering using Shodan 
Attackers can gather information on a target device using the filters given below: 
- Search for webcams using geolocation 
	- ``webcamxp country:US`` (Obtains all the webcamxp webcams present in US.)
-  Search using city
	- ``webcamxp city:paris
- Find webcams using longitude and latitude 
	- ``webcamxp geo:-50.81,201.80 
### Information Gathering using MultiPing 
- Open the MultiPing application and select File → Add Address Range 
- In the Add Range of Addresses pop-up window: 
	- Select the router’s gateway IP address from the Initial Address to Add drop-down field
-  Set the Number of addresses to “255”
	 - Click OK
### Information Gathering using FCC ID Search
### Information-Gathering Tools 
-  Censys 
- FOFA
### Information Gathering through Sniffing
Steps used by attackers to sniff wireless traffic of a web camera: 
- Run Nmap to identify IoT devices using insecure HTTP ports for transmitting data:
	- ``nmap -p 80,81,8080,8081 <Target IP address range>
-  Now, set up your wireless card in monitor mode and identify the channel used by the target router for broadcasting. For this, run ifconfig to identify your wireless card, here:
	- ``wlan0``
- Run airmon-ng to put the wireless card in monitor mode: 
	- ``airmon-ng start wlan0``
- Next, run Airodump-ng to scan all the nearby wireless networks: 
	- ``airodump-ng start wlan0mon``
- Now, discover the target wireless network and note down the corresponding channel to sniff the traffic using Wireshark
- Next, set up your wireless card to listen to the traffic on the same channel. For example, if the target network’s channel is 11, run ``airmon-ng`` to set your wireless card listening on channel 11: 
	- airmon-ng start wlan0mon 11
▪ Launch Wireshark and double-click the interface that was kept in monitor mode, here`` wlan0mon``  and start capturing the traffic
### Vulnerability Scanning
#### Vulnerability Scanning using IoTSeeker 
- For example, attackers run the following command to find devices with default credentials: 
	- ``perl iotScanner.pl <IP address/range of IP’s>``
#### Vulnerability Scanning using Genzai
- ackers can run the following command to scan a target IoT device’s dashboard and save the output in .json format:
	- ``./genzai <target_host> -save scan.json``
#### Vulnerability Scanning using Nmap
- Attackers use the following Nmap command to scan a specific IP address:
	- ``nmap -n -Pn -sS -pT:0-65535 -v -A -oX <Name><IP>``
- To perform a complete scan of the IoT device that checks for both TCP and UDP services and ports: 
	- ``nmap -n -Pn -sSU -pT:0-65535,U:0-65535 -v -A -oX <Name><IP>``
- To identify the IPv6 capabilities of a device:
	- ``nmap -6 -n -Pn -sSU -pT:0-65535,U:0-65535 -v -A -oX <Name><IP>``
#### Vulnerability-Scanning Tools
-  beSTORM
-  Metasploit (https://www.rapid7.com) 
- IoTsploit (https://iotsploit.co) 
- IoTSeeker (https://www.rapid7.com) 
- IoTVAS (https://firmalyzer.com) 
- Enterprise IoT Security (https://www.paloaltonetworks.com
### Analyzing Spectrum and IoT Traffic
#### Analyzing Spectrum using Gqrx
Steps to analyze the spectrum using Gqrx: 
- The Gqrx and GNU Radio packages consist of all the Gqrx utilities. Run the following commands to download and install this package from GitHub: 
	- ``git clone https://github.com/gqrx-sdr/gqrx.git gqrx.git 
	- `cd gqrx.git
	- ``mkdir build 
	- ``cd build 
	- ``cmake ..
	- ``make
attackers use hardware tools such as FunCube Dongle Pro+, which connects it to a USB port on a PC to analyze various frequency bands.
▪ Launch Gqrx using the following command: gqrx
▪ The Gqrx central window displays frequencies, and their noises can be heard via headphones or speakers

### Launch Attacks

#### Rolling Code Attack using RFCrack
Attackers use the RFCrack tool to obtain the rolling code sent by the victim to unlock a vehicle and later use the same code for unlocking and stealing the vehicle. RFCrack is used for testing RF communications between physical devices that communicate over sub-GHz frequencies. It is used along with a combination of hardware such as yardsticks to jam, replay, and sniff the signal coming from the sender. 
Attackers perform the following attacks using RFCrack: 
- Perform replay attacks (-i -F) 
- Send saved payloads (-s –u) 
- Perform rolling-code bypass attacks (-r -F -M) 
- Perform jamming (-j -F) 
- Scan incrementally through frequencies (-b -v -F) 
- Scan common frequencies (-k)
Commands used by an attacker to perform rolling-code attack are given below: 
- Live replay:
	- ``python RFCrack.py -i
- Rolling code: 
	- ``python RFCrack.py -r -M MOD_2FSK -F 314350000
- Adjust RSSI range:
	- ``python RFCrack.py -r -M MOD_2FSK -F 314350000 -U -100 -L -10
- Jamming:
	- ``python RFCrack.py -j -F 314000000``
- Scan common frequencies:
	- ``python RFCrack.py -k``
- Scan with your list:
	- ``python RFCrack.py -k -f 433000000 314000000 390000000
- Incremental scan:
	- ``python RFCrack.py -b -v 5000000``
- Send saved payload:
	- ``python RFCrack.py -s -u ./captures/test.cap -F 315000000 -M MOD_ASK_OOK``


## OT Hacking Methodology
- [ ]  add  notes 


# Lab 1: Perform Footprinting using Various Footprinting Techniques
## Task 1: Gather Information using Online Footprinting Tools
1. open any browser 
	- open ``Whois Domain Lookup`` or  whois.com
	- type  in search ``www.oasis-open.org`` 
2. open a new tab, and go to google-hacking-database 
	-  ``https://www.exploit-db.com/google-hacking-database``
	-  type ``SCADA`` in the **Quick Search** field and press **Enter**.
3.  new tab and go
	- ``"login" intitle:"scada login" ``
	- click link ``SEAMTEC SCADA login``
	- now we can brute force to get login 
	- we can  also use **intitle:"index of" scada** to search sensitive SCADA directories
- now using shodan.io
1. browser window, open a new tab and go to
	- `` https://account.shodan.io/login``
	- type **port:1883** in the address bar and press **Enter**.
```bash
Port 1883 is the default MQTT port; 1883 is defined by IANA as MQTT over TCP. 
```
	- click on any IP 
-  additional information on a target device using the following Shodan filters:
	-  **Search for Modbus-enabled ICS/SCADA systems:**
	    port:502
	- **Search for SCADA systems using PLC name:**
	    "Schneider Electric"
	- **Search for SCADA systems using geolocation:**
	    SCADA Country:"US"

# Lab 2: Capture and Analyze IoT Device Traffic

## Task 1: Capture and Analyze IoT Traffic using Wireshark
- open windows 2019 server 
1. installing  **MQTT Broker**
	- Navigate to **Z:\CEHv13 Module 18 IoT and OT Hacking\Bevywise IoT Simulator**
	- click on ``Bevywise_MQTTRoute_4.exe``
	-  MQTTRoute is using 1883
- open windows  2022 server 
1. To create IoT devices, we must install the **IoT simulator** on the client machine.
	- Navigate to **Z:\CEHv13 Module 18 IoT and OT Hacking\Bevywise IoT Simulator**
	- click ``Bevywise_IoTSimulator_3.exe*``
	-  To launch the **IoT simulator**, navigate to the **C:\Bevywise\IotSimulator\bin** directory and double-click on the **runsimulator.bat**
	- go to ``http://127.0.0.1:9000/setnetwork?network=HEALTH_CARE``
2. we will create a **virtual IoT network** and **virtual IoT devices**
	- Click on the **menu** icon and select the **+New Network** option.
	- **Create New Network** popup appears. Type any name
3. we will setup the **Simulator Settings**. Set the ``Broker IP`` Address as ``10.10.1.19`` (the IP address of the **Windows Server 2019** and port as ``1883``
	- Since we have installed the Broker on the web server, the created network will interact with the server using MQTT Broker. Do not change default settings and click on **Save**.
4. To add IoT devices to the created network, click on the ``Add blank Device`` button.
	- **Create New Device** popup opens. Type the device name (here, we use **Temperature_Sensor**), enter Device Id (here, we use **TS1**), provide a **Description** and click on **Save**.
	- The device will be added to the created network 
	-   To connect the Network and the added devices to the server or Broker, click on the **Start Network** red color circular icon in right corner.
- open windows 2019 server 
1.  Open a web browser, and go to ``http://localhost:8080`` and login using ``admin/admin``
- open windows 2022
1.  we will create the **Subscribe command** for the device Temperature_Sensor.
2.   Click on the **Plus** icon in **the top right corner** and select the **Subscribe to Command** option.
3. **Subscribe for command - TS1** popup opens. Select **On start** under the **Subscribe on** tab, type **High_Tempe** under the **Topic tab**, and select **1 Atleast once** below the **Qos** option. Click on **Save**.
4. Scroll down the page, you can see the **Topic** added under the **Subscribe to Commands** section.
5. we will capture the traffic between the **virtual IoT network and the MQTT Broker** to monitor the secure communication.
6. Minimise the Edge browser. Click **Type here to search** field on the **Desktop**, search for **wireshark** in the search bar and select **Wireshark** from the results.
7.  open wireshark and start capture
- switch to the Windows 2019
1. Navigate to **Devices** menu and click on connected device i.e.**TS1**.
2.  command to **TS1** using the **High_Tempe** topic.
3. **Send Command** section, select **Topic** as **High_Tempe**, type **Alert for High Temperature** in **Message** field and click on the **Submit** button.
4. **Message sent to TS1** appears under **Message** box which indicates that the message was successfully sent to TS1.
- open windows  2022
1. We have left the IoT simulator running in the web browser. To see the alert message, maximise the Edge browser and expand the arrow under the connected **Temperature_Sensor**, **Device Log** section.
2. You can see the alert message "**Alert for High Temperature**"
3. To verify the communication, we have executed **Wireshark** application, switch to the Wireshark traffic capturing window.
4. Type **mqtt** under the **filter** field and press **Enter**. To display only the MQTT protocol packets
5.  Select any **Publish Message** packet from the **Packet List** pane. In the **Packet Details** pane at the middle of the window, expand the **Transmission Control Protocol**, **MQ Telemetry Transport Protocol**, and **Header Flags** nodes.
6. Under the **MQ Telemetry Transport Protocol** nodes, you can observe details such as **Msg Len**, **Topic Length**, **Topic**, and **Message**.
7. Publish Message can be used to obtain the message sent by the MQTT client to the broker.

```bash
 Note: After establishing a successful connection with the MQTT broker, the MQTT client can publish messages. The headers in the Publish Message packet are given below:

- Header Flags: Contains information regarding the MQTT control packet type.
- DUP flag: If the DUP flag is 0, it indicates the first attempt at sending this PUBLISH packet; if the flag is 1, it indicates a possible re-attempt at sending the message.
- QoS: Determines the assurance level of a message.
- Retain Flag: If the retain flag is set to 1, the server must store the message and its QoS, so it can cater to future subscriptions matching the topic.
- Topic Name: Contains a UTF-8 string that can also include forward slashes when it needs to be hierarchically structured.
- Message: Contains the actual data to be transmitted.
- Payload: Contains the message that is being published.
```
1.   Now, scroll down, look for the **Publish Complete** packet from the **Packet List** pane, and click on it. In the **Packet Details** pane at the middle of the window, expand the **Transmission Control Protocol**, **MQ Telemetry Transport Protocol**, and **Header Flags** nodes.
2. Under the **MQ Telemetry Transport Protocol** nodes, you can observe details such as **Msg Len** and **Message Identifier**.
3. 1. Similarly you can select **Ping Request**, **Ping Response** and **Publish Ack** packets and observe the details.
4. This concludes the demonstration of capturing and analyzing MQTT protocol packets. Here, we analyzed different processes involved in the communication between an MQTT client and an MQTT broker using Wireshark. Understanding these metrics as well as the workflow can help you in quickly identifying the MQTT-related issues.

# Lab 3: Perform IoT Attacks
## Task 1: Perform Replay Attack on CAN Protocol
- open ubuntu as sudo 
1. to setup a virtual CAN interface issue following commands:
	- ``sudo modprobe can``
	- ``sudo modprobe vcan``
	- ``sudo ip link add dev vcan0 type vcan``
	- ``sudo ip link set up vcan0``
	-   To check  Virtual CAN interface is setup successfully, run ``ifconfig``
2.  to give permissions to the ICSim folder.
	- ``chmod -R 777 ICSim``
	- ``cd ICSim``
	- command to create two executable files for IC Simulator and CANBus Control Panel.
		- ``make``
3. To start the ICSim simulator.
	- ``./icsim vcan0``
4. open new terminal as  sudo and ``cd ICSim``
	-  to start the CANBus Control Panel.
		- ``./controls vcan0``
5. we will start sniffer to capture the traffic sent to the ICSim Simulator by CANBus control panel simulator.
	- open new terminal as  sudo and ``cd ICSim``
	- to start sniffing on the vcan0 interface
		- ``cansniffer -c vcan0 ``
	- To capture the logs run
	- open new terminal as  sudo and ``cd ICSim``
		- ``candump -l vcan0``
6. to perform replay attack
	- ``canplayer -I candump-2024-05-07_063502.log`` 



### References
