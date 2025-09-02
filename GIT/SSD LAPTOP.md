2025-04-04 23:46

Status:

Tags:

# SSD LAPTOP


Name of Laptop- LAPTOP-96PLO7DC IdeaPad 3 15IIL05
ssd name - SAMSUNG_MZALQ256HAJD-000L2
Bus type -Nvme
your laptop only supports PCIe Gen 3.0, not Gen 4 or Gen 5

## best option 
Samsung 970 EVO Plus 1TB
WD Black SN750 1TB
SK Hynix Gold P31 1TB
Crucial P3 Plus or P5 1TB
Kingston NV2 1TB

by at 8000 at 700 for 11 months 

best use 
https://www.amazon.in/Samsung-500GB-Internal-Solid-MZ-V8V500/dp/B08TJ2649W/ref=sr_1_3?nsdOptOutParam=true&s=computers&sr=1-3

https://www.amazon.in/Crucial-PCIe-NAND-NVMe-3500MB/dp/B0B25LZGGW/ref=sr_1_4?nsdOptOutParam=true&s=computers&sr=1-4

https://www.amazon.in/Western-Digital-Green-SN350-NVMe/dp/B09DVQQL9G/ref=sr_1_9?nsdOptOutParam=true&s=computers&sr=1-9

Let me clarify the difference between the two images:

The first image shows a 2.5-inch SATA SSD, while the second image shows an M.2 NVMe SSD. These are two completely different form factors and interfaces.

Based on your HWiNFO report, your current SSD is definitely an M.2 NVMe SSD (like the second image), not a 2.5-inch SATA SSD.

Here's the breakdown:

1. **Your current SSD (SAMSUNG_MZALQ256HAJD-000L2)**:
    - M.2 form factor (a small rectangular chip that connects directly to the motherboard)
    - NVMe interface over PCIe
    - Looks like the second image you shared (the small, gum-stick sized SSD)
2. **The first image you shared** ([https://reimg-teknosa-cloud-prod.mncdn.com/mnresize/600/600/productimage/784951968/784951968_0_MC/5696efc73f0f492db0dcdcd5cf4e696d.jpg](https://reimg-teknosa-cloud-prod.mncdn.com/mnresize/600/600/productimage/784951968/784951968_0_MC/5696efc73f0f492db0dcdcd5cf4e696d.jpg)):
    - This is a 2.5-inch SATA SSD
    - This is NOT compatible with your NVMe slot
    - This larger form factor requires a different type of connection than what your current SSD uses
3. **The second image you shared** ([https://m.media-amazon.com/images/I/419dpKuUuiL._SX450_.jpg](https://m.media-amazon.com/images/I/419dpKuUuiL._SX450_.jpg)):
    - This is an M.2 NVMe SSD (Samsung 980)
    - This IS compatible with your laptop
    - This is the correct form factor and interface for your laptop

When upgrading, you need to get the M.2 NVMe SSD (like in the second image), specifically the Samsung 980 NVMe SSD model MZ-V8V1T0B, not a 2.5-inch SATA SSD.
## SATA
General Information                                                             
Device Name:                                                                    Intel Ice Lake-U/Y PCH-LP - SATA Controller (AHCI) [D0]
Original Device Name:                                                           Intel Ice Lake-U/Y PCH-LP - SATA Controller (AHCI) [D0]
Device Class:                                                                   SATA AHCI Controller
Revision ID:                                                                    30 [D0]
PCI Address (Bus:Device:Function) Number:                                       0:23:0
PCI Latency Timer:                                                              0
Hardware ID:                                                                    PCI\VEN_8086&DEV_34D3&SUBSYS_381F17AA&REV_30

System Resources                                                                
Interrupt Line:                                                                 N/A
Interrupt Pin:                                                                  INTA#
Memory Base Address 0                                                           8122A000
Memory Base Address 1                                                           81233000
I/O Base Address 2                                                              3080
I/O Base Address 3                                                              3088
I/O Base Address 4                                                              3060
Memory Base Address 5                                                           81232000

Features                                                                        
Bus Mastering:                                                                  Enabled
Running At 66 MHz:                                                              Capable
Fast Back-to-Back Transactions:                                                 Capable

SATA Host Controller                                                            
Interface Speed Supported:                                                      Gen3 6.0 Gbps
Number Of Ports:                                                                1
External SATA Support:                                                          Not Capable
Aggressive Link Power Management:                                               Capable
Staggered Spin-up:                                                              Not Capable
Mechanical Presence Switch:                                                     Not Capable
Command Queue Acceleration:                                                     Capable
64-bit Addressing:                                                              Capable
AHCI Status:                                                                    Enabled
AHCI Version:                                                                   1.31
Ports Implemented:                                                              0

SATA Port#0                                                                     
Port Status:                                                                    Phy in offline mode
External SATA Port:                                                             Not Capable
Hot Plug:                                                                       Not Capable

Driver Information                                                              
Driver Manufacturer:                                                            Intel Corporation
Driver Description:                                                             Intel(R) 400 Series Chipset Family SATA AHCI Controller
Driver Provider:                                                                Intel Corporation
Driver Version:                                                                 18.36.1.1016
Driver Date:                                                                    23-Jul-2021
DeviceInstanceId                                                                PCI\VEN_8086&DEV_34D3&SUBSYS_381F17AA&REV_30\3&11583659&1&B8
Location Paths                                                                  PCIROOT(0)#PCI(1700)

### References
