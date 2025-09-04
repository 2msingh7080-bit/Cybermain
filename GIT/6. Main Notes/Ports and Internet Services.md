2024-10-14 17:33

Status:

Tags:

# Ports and Internet Services

#### **What Are Ports in Networking?**

- **Ports** are the entry and exit points on a machine that allow messages and data to flow between devices and the internet.
- Every machine is equipped with multiple **ports** that handle different services and allow data to be transmitted for specific purposes, such as video streaming, email, browsing, etc.

#### **Role of Ports in Internet Services**

- Each network service, like **video streaming**, **email**, or **web browsing**, requires its own specific **port** for incoming or outgoing data.
    - **Example**:
        - **Video Streaming**: Requires a port for receiving video data.
        - **Email**: Requires a separate port for sending or receiving emails.
- Different network services use different **port numbers**, which act as identifiers for handling specific types of network traffic.

#### **Definition of a Port**

- A **port** is a **logical point** on a machine that provides access to specific **network services** or **protocols** over the internet.
- Ports are used to route information to the correct service on the device.

#### **Common Ports and Their Functions**

- **Port 20/21**: Used for **FTP (File Transfer Protocol)** for file sharing and transfer.
- **Port 23**: Used for **Telnet**, which provides remote command-line access to devices.
- **Port 53**: Used for **DNS (Domain Name System)**, which resolves domain names into IP addresses.
- **Ports 67/68**: Used for **DHCP (Dynamic Host Configuration Protocol)**, which dynamically assigns IP addresses to devices on a network.

#### **TCP and UDP Protocols**

- **TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are the two primary communication protocols that work with ports.
    - **TCP** is connection-oriented and ensures reliable transmission of data.
    - **UDP** is faster but does not guarantee delivery, making it useful for services like video streaming or voice chat.

#### **Summary of Key Port Numbers**:

- **Port 20/21**: **FTP** (File Transfer Protocol)
- **Port 23**: **Telnet**
- **Port 53**: **DNS** (Domain Name System)
- **Ports 67/68**: **DHCP** (Dynamic Host Configuration Protocol)

---

### **Key Takeaways**:

- **Ports** serve as the logical entry and exit points for data transfer between devices and the internet.
- Different services (e.g., FTP, DNS) operate on specific **well-known port numbers**.
- **TCP and UDP** protocols govern the type of communication over these ports.

Here is a table listing common **port numbers** along with their associated **network services** and **protocols**:

| **Port Number** | **Service**                                | **Protocol** |
| --------------- | ------------------------------------------ | ------------ |
| 20, 21          | FTP (File Transfer Protocol)               | TCP          |
| 22              | SSH (Secure Shell)                         | TCP          |
| 23              | Telnet                                     | TCP          |
| 25              | SMTP (Simple Mail Transfer Protocol)       | TCP          |
| 53              | DNS (Domain Name System)                   | TCP/UDP      |
| 67, 68          | DHCP (Dynamic Host Configuration Protocol) | UDP          |
| 80              | HTTP (HyperText Transfer Protocol)         | TCP          |
| 110             | POP3 (Post Office Protocol)                | TCP          |
| 143             | IMAP (Internet Message Access Protocol)    | TCP          |
| 443             | HTTPS (HyperText Transfer Protocol Secure) | TCP          |
| 465             | SMTPS (SMTP Secure)                        | TCP          |
| 993             | IMAPS (IMAP Secure)                        | TCP          |
| 995             | POP3S (POP3 Secure)                        | TCP          |
| 123             | NTP (Network Time Protocol)                | UDP          |
| 161, 162        | SNMP (Simple Network Management Protocol)  | UDP          |
| 3389            | RDP (Remote Desktop Protocol)              | TCP          |
| 53              | DNS (Domain Name System)                   | TCP/UDP      |

summary of the **three types of ports** and their **port ranges**.

| **Port Type**             | **Port Range**   | **Description**                                                                                                                                         |
| ------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Well-Known Ports**      | 0 - 1023         | These are used by widely known and standard internet services (e.g., HTTP, FTP, DNS). These ports are commonly recognized and assigned by the IANA.     |
| **Registered Ports**      | 1024 -    49,151 | These are registered by IANA for specific services that aren't in the well-known port range. Organizations and applications may register these ports.   |
| **Private/Dynamic Ports** | 49,152 - 65,535  | These are temporary ports assigned dynamically when a service is requested. They are used during a session and released after the connection is closed. |

This classification ensures efficient management of services and traffic within networks.

#### **1. Open Port**

- **Definition**: An open port is like an open door, allowing traffic to pass through it freely.
- **Functionality**:
    - The port is actively in use and allows data packets to enter or exit the device.
    - An application or service is listening for network connections on the port.
- **Network Usage**:
    - Commonly used for services that require constant communication, such as web servers (port 80 for HTTP, port 443 for HTTPS).
    - Open ports can pose security risks if not managed correctly, as they can be exploited by attackers.

---

#### **2. Closed Port**

- **Definition**: A closed port is similar to a closed door, preventing any traffic from passing through.
- **Functionality**:
    - No application is actively listening on the port, meaning no data or connections can be made.
    - The port is not currently in use, but it can be opened if required by a service.
- **Network Usage**:
    - A closed port can act as a safeguard, ensuring that unused or unnecessary ports are not vulnerable to attack.
    - Ports may transition from closed to open when services are initiated and need to start communicating.

---

#### **3. Filtered Port**

- **Definition**: A filtered port's status is ambiguous—it’s unclear whether the port is open or closed due to restrictions.
- **Functionality**:
    - It may be blocked by a firewall or network filter, preventing external traffic from interacting with it.
    - The system may not respond to network queries, meaning it's uncertain whether the port is actively accepting connections.
- **Network Usage**:
    - Filtered ports are commonly used in high-security networks, where specific ports are selectively blocked to prevent unauthorized access.
    - Firewalls and security protocols often control filtered ports, adding another layer of protection.

---

### **Key Takeaways**:

- **Open Ports** allow unrestricted traffic and are vital for running services but can introduce security risks if not properly managed.
- **Closed Ports** block all traffic and indicate that no application is listening, but can be opened if necessary.
- **Filtered Ports** are controlled by security measures like firewalls and may not respond to traffic, adding ambiguity but increasing security.

Understanding these port states is essential for managing network security, ensuring that services run effectively while minimizing potential threats.

## Using Nmap for Port Scanning

#### **Nmap Overview**

- **Nmap** is a widely used tool for network discovery and security auditing.
- It can reveal which ports are open, closed, or filtered, and detect the services running on those ports.
- Nmap uses various options/arguments to control the type and depth of the scan.

---

### **Steps for Basic Nmap Scanning**

1. **Open Terminal in Linux**:
    
    - Nmap is usually run from the command line in Linux. You can open the terminal and start by typing the command.
2. **Using the Nmap Command**:
    
    - Basic syntax: `nmap [arguments] [target]`.
    - Example command:
        
        css
        
        Copy code
        
        `nmap -A example.org`
        
        - `-A`: Enables OS detection, version detection, script scanning, and traceroute.
        - `example.org`: Target domain.
3. **Command Execution**:
    
    - When you run the Nmap command, the tool will perform a scan and search for open, closed, or filtered ports on the target machine.

---

### **Port Scan Results Interpretation**

After running an Nmap scan, it will return a list of open, closed, or filtered ports:

#### **Open Ports**:

- Indicate that the port is open for communication and that a service is actively listening.
- In the lecture, the following open ports were detected:
    - **Port 22 (SSH)**: Running an SSH service, allowing secure remote login.
    - **Port 80 (HTTP)**: Used for web traffic, serving an HTTP service.
    - **Ports 9929** and **31337**: Both are open and ready to accept traffic, although their specific services weren’t detailed in this scan.

#### **Closed Ports**:

- These ports are not open for traffic, meaning there is no service actively listening on them.
- Out of 1,000 scanned ports, 957 were reported as closed, meaning they are not responding to any network requests.

#### **Filtered Ports**:

- A filtered port means it cannot be determined whether the port is open or closed, often due to firewall or network filtering.
- In this scan, 39 ports were filtered, likely due to security settings on the target machine.

---

### **Additional Information Gathered from the Scan**

- **OS Detection**: Nmap can detect the operating system running on the target device. In this case, it identified the target as running a **Linux Kernel**.
- **Service Detection**: It detects specific services running on open ports, such as SSH on port 22 and HTTP on port 80.
- **Host Status**: The scan reports if the host is up (i.e., active and reachable on the network).

---

### **Key Takeaways**:

- **Nmap** is a crucial tool for identifying open, closed, and filtered ports, which can help in understanding the network environment and potential vulnerabilities.
- **Open Ports**: Indicate active services that can be accessed and interacted with.
- **Closed Ports**: Are inactive, blocking traffic, but could be opened if a service starts.
- **Filtered Ports**: Represent ports that are blocked by firewalls or network filters, making them hard to assess without further investigation.
## Port Availability and Vulnerability

#### **Port Availability**

- Open ports can be vulnerable to attack if not properly secured.
- Attackers can detect open ports using tools like **Nmap**, which can reveal which services are running and which ports are available for communication.

#### **Attacker's Perspective**

- An attacker might identify an open port (e.g., **Port 22**) using **Nmap** and launch an attack by sending a large volume of data (ping packets) to overload the target.
- Example scenario: An attacker notices **Port 23** is open and sends a massive amount of traffic in a short period, overwhelming the system.

---

### **Denial of Service (DoS) Attack**

- **DoS Attack**: A single attacker overwhelms a target system by sending more traffic than the system can handle, leading to failure or crash.
    - The **buffer** (the memory that stores incoming data packets) becomes full, and the system can no longer process new data.
    - The host or network device "gives up," resulting in a **denial of service** where legitimate users cannot access the system.

#### **Distributed Denial of Service (DDoS) Attack**

- **DDoS Attack**: A more severe attack where multiple attackers or systems work together to flood the target with traffic.
    - Unlike a single-source DoS attack, DDoS involves a group (or even a network) of attackers sending enormous volumes of traffic to overwhelm the system.
    - This coordinated effort makes DDoS attacks much harder to mitigate than standard DoS attacks.

---

### **Port Security**

- **Are your ports still vulnerable?** Yes, any open port can potentially be exploited if not secured.
- Attackers use **reconnaissance** to gather information about open ports and services, which is the first step in most cyberattacks.
    - **Reconnaissance**: The process of gathering as much information as possible about a target system to identify vulnerabilities.
    - Attackers can capture packets, discover running services, and gather detailed information that can be used for future attacks.

---

### **Recommendations for Port Security**

- **Close unnecessary ports**: Only keep essential ports open.
- **Use port security measures** to protect open ports and the services they host. Key measures include:
    1. **Port Forwarding**: Redirect traffic from a public port to a private one, limiting direct exposure to the internet.
    2. **MAC Address Filtering**: Restrict access to devices based on their MAC addresses, ensuring that only authorized devices can communicate with your system.
    3. **Firewalls**: Use firewall rules to block unauthorized traffic and manage port access.

These measures will be explored further in the upcoming lectures.

---

### **Key Takeaways:**

- Open ports pose a security risk, and attackers can use tools like **Nmap** to identify vulnerable ports and services.
- **DoS** and **DDoS** attacks can cripple a system by overwhelming it with traffic, leading to service unavailability.
- **Port security** is essential to defend against reconnaissance and attacks. Following best practices, such as closing unnecessary ports, implementing MAC address filtering, and using firewalls, can mitigate these risks.

## MAC Filtering and Port Forwarding

#### **MAC Filtering**

- **Definition**: MAC filtering is a security feature that allows you to control which devices can connect to a wireless network based on their **MAC address** (a unique identifier for network devices).
    
    - It works by **allowing** or **blocking** devices based on their MAC addresses.
    - Devices that are **blacklisted** or not on the allowed list cannot join the network.
- **Usage**:
    
    - You can create a **whitelist** of trusted devices that are allowed to access the network.
    - Any device not on the whitelist will be **blocked** from joining.

#### **Limitations of MAC Filtering**

- **MAC Spoofing**: While MAC filtering adds a layer of security, it is not foolproof. Hackers can **spoof** (fake) MAC addresses to mimic a legitimate device that is on the allowed list.
    
    - Hackers can easily find resources online (like YouTube videos) that demonstrate how to spoof a MAC address.
    - Once spoofed, the attacker can bypass MAC filtering and gain access to the network, making this method less effective against skilled attackers.
- **Example Scenario**:
    
    - If an attacker discovers that their device is blocked from accessing the network because their MAC address is not on the whitelist, they can spoof their MAC address to appear as an authorized device. This allows them to bypass MAC filtering and join the network undetected.

#### **Why MAC Filtering is Limited**:

- MAC filtering can **help reduce** unauthorized devices from joining your network but is **not reliable** against more advanced attacks like MAC spoofing.
- **Modern hackers** have access to easy tools and methods for bypassing this kind of protection.

---

### **Introduction to Port Forwarding**

- **Port Forwarding**: A more effective security measure than MAC filtering.
    - In port forwarding, traffic from specific **public ports** is forwarded to private ports within a network, limiting the exposure of sensitive systems.
    - Port forwarding enhances security by restricting external access to services that are only accessible via predefined, authorized ports.

---

### **Key Takeaways:**

- **MAC filtering** offers basic network security by controlling device access through MAC addresses, but it can be easily bypassed through MAC spoofing.
- **MAC spoofing** allows attackers to disguise their device's MAC address, making MAC filtering ineffective as a standalone security measure.
- **Port forwarding** is introduced as a more advanced method of network security, which will be discussed in detail in future sections.

## Port Forwarding and Network Address Translation (NAT)

#### **Port Forwarding**

- **Definition**: Port forwarding is a method of **NAT** that translates public IP addresses to private IP addresses and vice versa. It allows external devices on public networks (like the internet) to communicate with devices on a private network by mapping specific **ports** and **IP addresses**.
    - **NAT Recap**: NAT allows devices within a private network to use a **single public IP address** for internet communication, reducing the number of public IPs needed.
    - Port forwarding enhances this by mapping specific **port numbers** along with IP addresses for more precise communication.

#### **How Port Forwarding Works**:

1. **Mapping IP and Port**: Port forwarding maps a **combination of IP address** and **port number** from the private network to the public network, and vice versa. This combination is crucial in routing traffic to specific devices within the network.
    
    - **Example**: A request from a private network device (IP 192.168.0.1) using port 80 can be mapped to a public IP (e.g., 112.54.67.13) also using port 80.
2. **Private and Public Network Communication**:
    
    - When a device in a private network (like a PC) wants to access a public service (like YouTube), it sends a request to a **public server** (YouTube’s IP address).
    - The request is routed through a **router** which converts the private IP address of the device into a **public IP address** using the router’s public IP.
    - The public server receives the request, thinking it’s from the router’s public IP, and sends a response back to the router.
3. **Router’s Role**:
    
    - The router manages the translation between public and private IPs. When it receives the response from the public server, it knows which private IP made the original request and forwards the response to the correct device within the private network.
    - This process allows **multiple devices** in the private network to use the same public IP for internet communication.

#### **Detailed Example of Port Forwarding**:

- **Initial Request**:
    
    - A device in a private network with IP **192.168.0.3** wants to access YouTube.
    - The request goes out to YouTube’s public IP **112.54.67.13** via **port 80**.
    - The router translates the private IP **192.168.0.3** to the router’s public IP (e.g., **123.45.67.89**), so the YouTube server sees the request as coming from this public IP.
- **Response**:
    
    - YouTube responds to **123.45.67.89** (the router's public IP).
    - The router receives the response and knows the original request came from the private IP **192.168.0.3** using **port 80**.
    - The router forwards the YouTube response to **192.168.0.3**, allowing the device in the private network to access the content.

#### **Why Use Port Forwarding?**

- **Efficient Use of Public IPs**: Public IP addresses are limited, and port forwarding allows many devices in a private network to share a single public IP.
- **Service Access**: It enables access to specific services (like web servers) running on private networks from public networks.
- **Traffic Control**: Port forwarding helps control and secure traffic by only allowing specific types of traffic (based on port numbers) to access certain devices.

---

### **Key Takeaways**:

- **Port forwarding** is an advanced NAT technique that maps combinations of **IP addresses** and **port numbers** to enable communication between private and public networks.
- It allows efficient usage of scarce public IP addresses by enabling multiple devices on a private network to use a single public IP.
- The router plays a vital role in **translating** between private and public IPs, ensuring that data is routed to the correct device within the private network.
- Port forwarding is crucial for enabling external devices or networks to access specific services within a private network.
### Dynamic Host Configuration Protocol (DHCP)

#### Overview

- **Definition**: DHCP is an Internet protocol used to assign IP configurations to nodes that connect to a network.
- **Purpose**: Automates the process of configuring devices on IP networks, allowing them to communicate on a network.

#### Key Concepts

- **IP Address**: A unique 32-bit address assigned to devices on a network.
- **Client-Server Model**: DHCP operates on a client-server model where the client requests configuration details and the server provides them.

---


### References
