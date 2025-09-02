2025-08-23 15:43

Status:

Tags: #study 

# Radio Spectrum'

To capture the radio singles use SDR devices 
- RTL-SDR Blog V3 USB Dongle  
- RTL-SDR Blog V4 USB Dongle
buy link here [1](https://www.fabtolab.com/rtl-sdr-blog-v4-r828d-rtl2832u-1ppm-tcxo-sma-software-defined-radio-dongle-only) [2](https://www.indiamart.com/proddetail/software-defined-radio-rtl-sdr-v3-usb-dongle-22254853297.html)
## **Summary Table**

| Device         | Main Use                         | RX/TX | Price Range (INR) | Best For           |
| -------------- | -------------------------------- | ----- | ----------------- | ------------------ |
| RTL-SDR V3/V4  | Beginner, basic reception        | RX    | ₹3,400–₹5,900     | Beginner, learning |
| SDRplay RSP1A  | HF/VHF/UHF all-band, contesting  | RX    | ₹12,000–₹13,500   | Advanced receive   |
| Airspy Mini/R2 | VHF/UHF, digital, weak signal RX | RX    | ~₹10,000–₹20,000  | Signal Quality     |
| HackRF One     | Experiment, RF hacking, TX/RX    | RX/TX | ₹25,000–₹34,000+  | Research           |
| ADALM-Pluto    | Learning, portable, lab          | RX/TX | ~$22,000+         | Teaching/projects  |
| USRP           | Professional, research           | RX/TX | ₹40,000+ (varies) | Industry, R&D      |
### Analyzing Spectrum 
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

### Tools to Perform SDR-Based Attacks
Attackers use various tools such as RTL-SDR, GNU Radio, and Universal Radio Hacker to perform various types of attacks, such as reconnaissance attacks, replay attacks, and cryptanalysis attacks, on SDR-based devices. 
- Universal Radio Hacker
	Source: https://github.com
Universal Radio Hacker (URH) is software for investigating unknown wireless protocols used by various IoT devices. This tool allows attackers to perform the following activities:
-  Identify hardware interfaces for common SDRs
- Perform demodulation of signals 
- Assign participants to keep an overview of data 
- Crack even sophisticated encodings like CC1101 data whitening 
- Assign labels to reveal the logic of the protocol 
- Perform automatic reverse engineering of protocol fields 
- Perform fuzzing component to find security leaks 
- Perform modulation to inject the data back into the system

Listed below are some of the additional tools to perform SDR-based attacks: 
- BladeRF (https://www.nuand.com) 
- TempestSDR (https://github.com) 
- HackRF One (https://greatscottgadgets.com) 
- GP-Simulator (https://gpspatron.com) 
- Gqrx (https://gqrx.dk)

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
### BlueBorne Attack Using HackRF One
The devices involve wireless communication using RF, ZigBee, or LoRa. Attackers use HackRF One to perform attacks such as BlueBorne or AirBorne attacks, including replay, fuzzing, and jamming. HackRF One is an advanced hardware-and software-defined radio with a range of 1 MHz to 6 GHz. It transmits and receives radio waves in half-duplex mode, so it is easy for attackers to perform attacks using this device. It can sniff a wide range of wireless protocols from GSM to Z-wave

### Replay Attack using HackRF One
Steps to perform a replay attack on the target IoT device:
- Step 1: Record the device’s signal using the following command:
	- ``hackrf_transfer -r connector.raw -f [device frequency] Here, -r → used to record the signal, -f → frequency of the device
-  Step 2: Replay the signal to the target using the following command: 
	- ``hackrf_transfer -t connector.raw -f [device frequency] Here, -t → used to replay the signal

### SDR-Based Attacks using RTL-SDR and GNU Radio
  Hardware-based attack
- Attackers use hardware tools such as RTL-SDR to perform SDR-based attacks on IoT devices. 
-  RTL-SDR Source:
https://www.rtl-sdr.com 
RTL-SDR hardware is available in the form of a USB dongle that can be used to capture active radio signals in the vicinity (an Internet connection is not mandatory). It is available in different models, such as DVB-T SDR, RTL2832, RTL dongle, or DVB-T dongle. The RTL-STR tool can capture frequencies ranging from 500 kHz up to 1.75 GHz based on the selected SDR models.

Attackers use an RTL-SDR radio scanner to perform the following activities: 
- Receiving and decoding GPS signals 
- Analyzing spectrum 
- Listening to DAB broadcast radio 
- Listening to and decoding HD radio 
- Sniffing GSM signals 
- Listening to VHF amateur radio 
- Scanning trunked radio conversations •
- Scanning for cordless phones

 Software-based attack
- Along with hardware tools, attackers can also assault SDR-based IoT devices using various software tools, such as GNU Radio
 GNU Radio Source:
https://www.gnuradio.org

- The GNU Radio tool makes use of external RF hardware to generate SDR. It offers a framework and the required tools to generate software radio signals. It also offers processing units for signals to implement software radios. Attackers use GNU Radio to perform various SDR-based attacks on target IoT devices. Before attacking the target device, attackers need to build and configure GNU Radio. After the successful installation of GNU Radio, attackers use the tools below to perform further exploitation. GNU Radio consists of a number of pre-defined programs and tools, which can be used for a variety of tasks. 
- uhd_ft → A spectrum analyzer tool that can be connected to a UHD device to find the spectrum at a given frequency
- uhd_rx_cfile → Stores wave samples with the help of a UHD device; samples can be stored in a file and analyzed later using GNU Radio or similar tools such as Matlab or Octave
- uhd_rx_nogui → Used to obtain and listen to the incoming signals on the audio device
-  uhd_siggen_gui → Used to create simple signals such as sine, square, or noise • gr_plot → Used to present previously recorded samples saved in a file
start 2860 CEH IOT 

### References
