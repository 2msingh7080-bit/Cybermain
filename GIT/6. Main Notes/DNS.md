2024-10-14 22:07

Status:

Tags:

# DNS (Domain Name System) Overview

**Introduction to DNS:**

- DNS (Domain Name System) is a service responsible for converting domain names (like facebook.com) into corresponding IP addresses and vice versa.
- Every time you type a web address in your browser (e.g., facebook.com or instagram.com), DNS resolves this human-readable address into a machine-readable IP address to load the website.

**How DNS Works:**

1. **Domain Names & IP Addresses:**
    
    - Domain names are human-readable strings like "facebook.com" or "instagram.com."
    - Each domain name corresponds to an IP address that identifies the website's server on the internet (e.g., Facebook might have an IP address like 157.240.23.9435).
    - DNS maps these domain names to their IP addresses.
2. **Example:**
    
    - Typing "facebook.com" in your browser is converted into the IP address associated with Facebook's server.
    - You can also access Facebook by typing its IP address directly in the browser, which will take you to the same webpage.

**Domain Name Structure:**

- Domain names consist of multiple parts:
    - **Host Name:** The part before the first dot (e.g., "www" in "[www.facebook.com](http://www.facebook.com)").
    - **Domain Name:** The main part, like "facebook."
    - **Top-Level Domain (TLD):** The part after the last dot, like ".com," ".org," ".net."
    - **Fully Qualified Domain Name (FQDN):** The full domain, including the host, domain name, and TLD (e.g., "[www.facebook.com](http://www.facebook.com)").

**Levels of Domain Names:**

1. **Top-Level Domain (TLD):** The highest level in the DNS hierarchy (e.g., ".com," ".net").
2. **Second-Level Domain:** Directly below the TLD, usually the main brand or organization (e.g., "facebook").
3. **Host Name:** The specific server or service (e.g., "www").

**Fully Qualified Domain Name (FQDN):**

- A complete domain name that specifies both the host and the domain, including the TLD (e.g., "[www.myPC.com](http://www.myPC.com)").

### Key Takeaways:

- DNS simplifies internet browsing by converting domain names into IP addresses.
- Domain names are structured into host names, domain names, and top-level domains.
- FQDN combines all these parts to form a fully specified address.

### DNS Lookup Process

**Introduction to DNS Lookup:**

- DNS lookup is the process where a domain name is translated into its corresponding IP address, or vice versa.
- It allows devices on the internet to locate each other by resolving human-readable domain names to machine-readable IP addresses.

**Types of DNS Lookup:**

1. **Forward DNS Lookup:** Converts a domain name into its corresponding IP address.
2. **Reverse DNS Lookup:** Converts an IP address back into a domain name.

**How DNS Lookup Works:**

1. **Cross Conversion:** DNS lookup performs a cross conversion between domain names and IP addresses.
    
    - Example: When you type "facebook.com" in your browser, a forward DNS lookup is performed to find the IP address of Facebook's server.
    - A reverse DNS lookup finds the domain name corresponding to an IP address.
2. **DNS Servers:**
    
    - DNS servers store millions of domain names and their corresponding IP addresses. This means users don't need to memorize IP addresses.
    - These servers are organized into a **hierarchy** of four types:
        1. **Root Name Servers:** The highest level, which directs DNS queries to the appropriate top-level domain (TLD) servers.
        2. **Top-Level Domain (TLD) Servers:** Handle domains like ".com," ".org," ".net," and direct the query to the appropriate server for that domain.
        3. **Authoritative Name Servers:** Store the actual IP addresses and other DNS records for the domain being queried.
        4. **Resolving Name Servers:** These are typically maintained by ISPs (Internet Service Providers) and handle the initial DNS query before passing it on to other DNS servers if needed.

**Example of DNS Lookup in Action:**

- **Step-by-Step Process:**
    1. You type "facebook.com" in your browser.
    2. The request goes to a resolving DNS server, which checks if it has the IP address for Facebook.com cached.
    3. If not, the request is passed to the root server, which directs the query to a TLD server (for ".com").
    4. The TLD server directs the query to Facebook's authoritative DNS server, which provides the IP address.
    5. The IP address is returned to your browser, allowing it to connect to Facebook's server and display the homepage.

### Key Takeaways:

- DNS lookup is essential for converting domain names to IP addresses and vice versa.
- DNS servers are organized into a hierarchy, ensuring that domain names can be efficiently translated across the internet.

### DNS Lookup Activity (Behind the Scenes of Domain Resolution)

**Overview:** When you enter a domain name such as Facebook.com or Amazon.com into your browser, the network (DNS servers) doesn’t understand these human-readable domain names directly. Instead, these domain names are simply characters for the network, and the DNS system works behind the scenes to translate them into IP addresses that the network can understand and use to direct your request to the correct server.

**Steps of Domain Resolution:**

1. **Browser Cache Check:**
    
    - When you type a URL (like Facebook.com), the browser first checks its **cache** (memory) to see if it has recently stored the IP address of that domain.
    - If the IP address is already cached (for example, from a previous visit), the browser retrieves it and loads the website directly.
2. **Local Host File Check:**
    
    - If the browser cache doesn't contain the IP, the browser checks the **local host file** (stored in the system’s files, e.g., Windows/System32/etc/hosts).
    - The host file contains a list of manually mapped domain names and their corresponding IP addresses.
    - If the IP address is found here, the local host file provides it to the browser, and the website is loaded.
3. **DNS Server Query:**
    
    - If neither the browser cache nor the local host file knows the IP address, the system sends a **DNS query** to a **DNS server**.
    - The DNS server (or **resolving name server**) contains a vast database of domain names mapped to their IP addresses.
    - The DNS server searches for the IP address corresponding to the domain (e.g., Facebook.com) and returns it to the browser.
4. **Displaying the Website:**
    
    - Once the browser receives the IP address (from the cache, host file, or DNS server), it uses the IP to connect to the web server hosting the website and loads the content for the user to see.

**Example:**

- **Scenario 1:** You type **Amazon.com** in your browser.
    - If the browser cache has the IP, it loads the website directly.
    - If not, it checks the local host file.
    - If the IP is not in the host file, the request is sent to a DNS server, which resolves the domain to an IP, and the browser displays the website.
- **Scenario 2:** A local host file contains the mapping for **Amazon.com** to a specific IP. The browser uses the local file’s information to load the website without querying DNS servers.

**Interesting Fact:**

- There is one default entry in the host file for most systems: **127.0.0.1**, which refers to the **localhost** or your own machine. This address is used for internal testing or server configuration.

**Summary of DNS Process:**

- **Browser Cache → Local Host File → DNS Server**: These steps are followed in sequence to resolve a domain name into its corresponding IP address.
- DNS servers map domain names to IP addresses, enabling browsers to display websites using the IP.

This process is practical and happens in milliseconds whenever you access a website, making the entire browsing experience seamless for the user.

### Networking Concepts and Address Resolution Protocol (ARP)

#### Key Concepts for Sending Data on a Network

- To send messages between nodes in a network, four essential addresses are required:
    
    1. **Sender's MAC Address**
    2. **Sender's IP Address**
    3. **Receiver's MAC Address**
    4. **Receiver's IP Address**
- **IP (Internet Protocol) Address**: Unique identifier for each device on a network at Layer 3 of the OSI model.
    
- **MAC (Media Access Control) Address**: Physical hardware address of a network interface card at Layer 2 of the OSI model.
    

#### Practical Example in Cisco Packet Tracer

1. **Setup**: Two devices, PC2 and another device, are connected via a switch.
    
    - Using command prompt (`cmd`), the user can check the device’s IP and MAC addresses using commands like `ipconfig /all`.
    - Example of sender’s details:
        - IP Address: `10.0.0.3`
        - MAC Address: `00:01:96:97:88`
2. **Ping Command**: When trying to communicate with another node (e.g., `ping 10.0.0.1`), you need:
    
    - Sender's IP and MAC addresses.
    - Receiver’s IP address.
    - If you don’t know the receiver’s MAC address, the Address Resolution Protocol (ARP) can help.

#### Address Resolution Protocol (ARP)

- **Function**: Maps a device's IP address (Layer 3) to its MAC address (Layer 2).
- **Process**:
    - When a sender knows the receiver’s IP but not the MAC, ARP broadcasts a request to find the MAC corresponding to that IP.
    - Once the receiver responds with its MAC, communication can proceed.
    - Example in the Packet Tracer simulation: ICMP (Internet Control Message Protocol) pings rely on ARP to resolve the receiver’s MAC before sending data.

#### How ARP Works

- ARP sends a broadcast request to all devices within the local network, asking "Who has this IP?".
- The device with the matching IP replies with its MAC address.
- Once the sender knows the receiver’s MAC, data can be transmitted.

#### Conclusion

- **Four Addresses for Communication**: Sender's and receiver’s IP and MAC addresses are essential.
- **ARP's Role**: Resolves IP to MAC address to ensure Layer 2 communication.
- The concept of ARP highlights the interaction between Layer 2 and Layer 3 for network communication.

---

### Summary:

- **Network communication requires four addresses**: two IPs and two MACs (sender and receiver).
- **ARP** maps IP addresses to MAC addresses, facilitating communication within a local network.
- In real-world scenarios, ARP resolves the receiver's MAC if the sender knows the IP, enabling successful message delivery.

### References
