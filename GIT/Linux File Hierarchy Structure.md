2025-02-19 17:06

Status:

Tags:

# Linux File Hierarchy Structure

#### **Overview**

The **Linux File Hierarchy Structure** defines how directories and files are organized in **Unix-like** operating systems. It is maintained by the **Linux Foundation** and follows a standardized format.

- The root directory **`/` (slash)** is the top-level directory.
- **All files and directories** appear under `/`, even if they exist on different physical or virtual devices.
- **Only the root user** can write to the `/` directory.

---

### **1. Common Directories in Linux File System**

|**Directory**|**Purpose**|**Examples**|
|---|---|---|
|`/bin`|Essential user command binaries.|`ls`, `cat`, `cp`|
|`/home`|User directories containing personal files and settings.|`/home/user1`, `/home/user2`|
|`/sbin`|System administrator commands for system maintenance.|`reboot`, `ifconfig`|
|`/boot`|Bootloader files for system startup.|GRUB files|
|`/etc`|Configuration files required by the system and applications.|`resolv.conf`|
|`/lib`|Shared libraries essential for `/bin` and `/sbin` binaries.|Dynamic libraries (`.so` files)|
|`/dev`|Device files, including USBs and terminal devices.|`/dev/null`, `/dev/sda1`|
|`/opt`|Optional application software packages.|Custom installed software|
|`/proc`|Virtual directory containing system process and kernel info.|`/proc/cpuinfo`|
|`/mnt`|Temporary mount point for file systems.|Mounted drives|
|`/var`|Variable data like logs and temporary files.|System logs (`/var/log`)|
|`/media`|Mount points for removable media (e.g., CDs, USB drives).|`/media/cdrom`|
|`/tmp`|Temporary files created by system and users.|Temporary session data|
|`/srv`|Site-specific data for services (e.g., web servers).|Web server files|
|`/usr`|Binaries, libraries, documentation, and source code for system programs.|`/usr/bin`, `/usr/lib`|

---

### **2. Key Takeaways**

- **Linux follows a hierarchical directory structure** with `/` as the root.
- **Each directory serves a specific purpose**, making system management and organization efficient.
- **Understanding these directories** is crucial for Linux administration, troubleshooting, and system navigation.
****




### References
