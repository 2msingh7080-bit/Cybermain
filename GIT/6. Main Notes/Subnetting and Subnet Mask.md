2024-10-14 12:23

Status:

Tags:

# Subnetting and Subnet Mask
#### **Introduction to Subnetting**

- **Subnet**: A subnet is a smaller, logical subdivision of a larger network.
    - Example: A network with 100 nodes can be divided into 5 smaller subnets of 20 nodes each.
    - **Purpose**: Subnetting reduces traffic on the main network by breaking it into smaller, manageable segments.
    - **Advantage**: Each subnet handles its own traffic, acting as an individual network.
- **Problem with Subnets**:
    - When subnets are formed, they become isolated, functioning as independent entities.
    - **Intercommunication Challenge**: Subnets need routing to communicate with each other.

#### **Example of Subnetting**

- Consider a **parent network** with 100 nodes:
    
    - This parent network (Network E) is divided into four subnets (A, B, C, D).
    - Subnet addresses:
        - **Subnet E**: 100.0.0.0
        - **Subnet B**: 100.1.0.0
        - **Subnet C**: 100.100.1.0
        - **Subnet D**: 100.123.17.0
- **Address Structure**:
    
    - The first part of the subnet address (e.g., "100") is inherited from the parent network.
    - This part of the address ensures that the subnet is identified as part of the original network.

#### **Subnet Mask**

- **Subnet Mask**: Essential for defining how a network is divided into subnets.
    - The subnet mask helps determine which part of an IP address is allocated to the network and which part is reserved for the host.

---

### **Key Takeaways**:

- **Subnet**: A smaller division of a larger network, allowing for better traffic management.
- **Routing**: Necessary to enable communication between isolated subnets.
- **Subnet Mask**: A critical tool used to define network divisions when subnetting.
### IP Address and Subnet Mask

---

#### **Understanding the Structure of an IP Address**

- **Two main parts of an IP address**:
    - **Network Part**: Identifies the specific network.
        - Example: In a network address like "Network E", the first part of the IP indicates it.
    - **Host Part**: Refers to the specific node (device) within the network.
        - Example: The host portion provides the address of a node within the network, such as a machine labeled "1123" inside "Network X".

#### **How IP Address Parts Work Together**

- **Network Part**:
    - Tells which network a device is located in.
- **Host Part**:
    - Pinpoints the specific device within that network.

#### **What is a Subnet Mask?**

- A **subnet mask** is similar to an IP address but serves a unique purpose—it helps divide the IP address into the **network** and **host** portions.
    - The subnet mask splits the IP address, helping identify which part is allocated to the network and which part is for the host.

#### **Bit Length and Subnet Masks**

- **Subnet masks** can have different bit lengths based on the **class** of the IP address:
    - **Class A**: Uses an 8-bit mask (e.g., 255.0.0.0).
    - **Class B**: Uses a 16-bit mask (e.g., 255.255.0.0).
    - **Class C**: Uses a 24-bit mask (e.g., 255.255.255.0).
- **Subnet Mask Multiples**: The subnet mask is generally represented in multiples of 8 bits, such as:
    - 255.0.0.0 (8 bits)
    - 255.255.0.0 (16 bits)
    - 255.255.255.0 (24 bits)

#### **Classless Inter-Domain Routing (CIDR) and Subnet Mask**

- **CIDR Notation**: A more flexible way of representing IP addresses and subnet masks.
    - In CIDR, subnet masks do not have to be multiples of 8 (e.g., /17, /26).
    - **Variable-Length Subnet Masks (VLSM)**: These allow the use of subnet masks of various lengths, reducing IP address wastage.
    - Examples:
        - 255.255.128.0 (17 bits)
        - 255.255.252.0 (22 bits)
        - 255.255.255.252 (30 bits)

#### **Key Differences Between Classful and CIDR Addressing**

- **Classful Addressing**: Requires subnet masks in multiples of 8 bits.
- **CIDR**: Allows flexible subnet mask lengths to conserve address space, reducing the wastage of IP addresses in classful networks.

---

### **Key Takeaways**:

- An IP address has **two parts**: the **network part** (identifying the network) and the **host part** (identifying the device in that network).
- A **subnet mask** helps split an IP address into the network and host parts.
- **Classful** addressing follows a rigid structure (multiples of 8 bits), while **CIDR** uses flexible subnet masks to optimize IP address allocation.
### Subnet Mask and Bitwise AND Operation

---

#### **Bitwise Comparison of IP Address and Subnet Mask**

- When an IP address and a subnet mask are compared, they undergo a **bitwise AND operation**.
- **Bitwise AND** is a logical operation performed on each corresponding bit of the IP address and the subnet mask, one bit at a time.

#### **What is a Bitwise AND Operation?**

- The **AND** operation checks both bits, and the result is:
    - **1 (True)** only if both input bits are 1.
    - **0 (False)** if either of the bits is 0.
- In simpler terms:
    - If both inputs are **True (1)**, the output is **True (1)**.
    - If either or both inputs are **False (0)**, the output is **False (0)**.

#### **Applying Bitwise AND to IP Address and Subnet Mask**

- Example:
    - **IP Address**: `192.168.123.456`
    - **Subnet Mask**: `255.255.255.0` (a 24-bit subnet mask)
    - **Binary Representation**:
        - **IP Address** in binary: A long string of binary digits representing `192.168.123.456`.
        - **Subnet Mask** in binary: A corresponding string representing `255.255.255.0`.
- **Bitwise AND Operation**:
    - Start from the **rightmost bit** (Least Significant Bit - LSB) and work towards the **leftmost bit** (Most Significant Bit - MSB).
    - Each bit of the IP address is compared with the corresponding bit of the subnet mask.

#### **Example of Bitwise AND Operation**

- In this example, the comparison is done bit by bit:
    - **0 AND 0 = 0** (or False AND False = False)
    - **1 AND 1 = 1** (or True AND True = True)
    - **1 AND 0 = 0** (or True AND False = False)
- This process is repeated for all the bits of the IP address and subnet mask.

#### **Resulting Network Address**

- After performing the bitwise AND operation on all bits, the result is a **network address**.
    - Example output: `192.168.123.0` (after ANDing `192.168.123.456` and `255.255.255.0`).
    - The last part of the address becomes **0** because the subnet mask determines the portion of the address allocated to the network.

#### **Key Points to Remember**

- The **Bitwise AND operation** is performed from the **rightmost** bit (LSB) to the **leftmost** bit (MSB).
- The **network address** is the result of the bitwise AND operation.
    - The output represents the network portion of the IP address.

---

### **Key Takeaways**:

- A **bitwise AND operation** compares each bit of an IP address and a subnet mask to determine the **network address**.
- In the **AND operation**, both input bits must be **1 (True)** for the result to be **1 (True)**.
- The result of the operation gives the **network address**, where the last part of the address (host portion) may be set to **0** depending on the subnet mask.
### Host Address in Networking

---

#### **Host Address and Network Address**

- **Host address** is the portion of the IP address that identifies a specific device within a network.
- After extracting the **network address** from the IP address, the remaining part is the **host address**.
    - Example:
        - **IP Address**: `192.168.123.456`
        - **Network Address**: `192.168.123.0` (obtained by the bitwise AND operation with the subnet mask).
        - **Host Address**: `456` (remaining part of the IP address after extracting the network address).

#### **Binary Representation of Host Address**

- In the **binary representation**, the **host address** appears after applying the **bitwise AND operation**.
- The portion reserved for the **network address** will have all **zeros** in the corresponding binary digits of the host address.
    - Example: The host address may look like `0000 0000 0000 0456` (binary form of the host portion).

#### **Separation of IP Address**

- The IP address is divided into two parts:
    
    1. **Network Address**: Identifies the overall network.
    2. **Host Address**: Identifies individual devices within that network.
- **Example** (continued):
    
    - Network portion: `192.168.123.0`
    - Host portion: `0.0.0.456`
    - Together, they form the full IP address: `192.168.123.456`.

#### **Function of Subnet Mask**

- The **subnet mask** is essential for determining where the network address ends and the host address begins.
- By performing a **bitwise AND operation** between the **IP address** and the **subnet mask**, the network address is identified, and the remaining part becomes the host address.

#### **Key Points to Remember**

- The **host portion** must be zero in the network address.
- The remaining part of the IP address that is not part of the network address is the **host address**.
- The **bitwise AND operation** helps separate the network and host portions.

#### **Variable Outputs**

- Depending on the **IP address** and **subnet mask** used, the results of the **network address** and **host address** will change.
- This concept remains the same across different examples:
    - **Bitwise AND operation** between an IP address and subnet mask results in the **network address**.
    - The leftover part is the **host address**.

---

### **Key Takeaways**:

- **Host address** is the portion of the IP address that uniquely identifies a device in a network.
- The **network address** is extracted by performing a **bitwise AND operation** between the IP address and subnet mask.
- After extracting the network address, the **remaining part** of the IP address is the **host address**.
### Subnetting and Routing

---

#### **Subnetting and Its Role in Networking**

- **Subnetting** divides a large network into smaller, more manageable **sub-networks (subnets)**.
- The main goal is to organize and control the traffic by separating a network into **logical subdivisions**.
- **Router's Role**:
    - The router's responsibilities are twofold:
        1. **Find the network address** where the data packet is headed.
        2. **Identify the host** within that network to deliver the packet accurately.

#### **Router Operation Using IP Address and Subnet Mask**

- Example IP: `192.168.123.456` and **Subnet Mask**: `255.255.255.0` (also known as `/24`).
    - The router extracts the **network address** using a **bitwise AND operation**.
    - **Network Address**: `192.168.123.0` (first three octets are the network portion).
    - The remaining **host portion**: `0.0.0.456` identifies the specific device within the network.

#### **Steps Taken by a Router**

1. **Perform Bitwise AND Operation**:
    - The router performs a bitwise AND operation between the IP address (`192.168.123.456`) and the subnet mask (`255.255.255.0`).
    - **Result**: The router finds the network address `192.168.123.0`.
2. **Identify the Host Inside the Network**:
    - The router checks the **host portion** in the IP address (the remaining part after determining the network address).
    - **Host Address**: `0.0.0.456`.

#### **Importance of Subnet Masks**

- **Subnet Mask**:
    - Helps identify the division between the **network address** and the **host address**.
    - Example: **Subnet Mask** `/24` (`255.255.255.0`) indicates that the first 24 bits are reserved for the network.
    - The remaining bits represent the **host portion**.

#### **Determining Network and Host**

- **Network Address**: The portion of the IP address that identifies a network.
    
- **Host Address**: The specific device within that network.
    
- **Example (continued)**:
    
    - **Network Address**: `192.168.123.0`
    - **Host Address**: `0.0.0.456`

#### **Subnets and Subnet Mask Characteristics**

- Subnets are used to divide large networks into smaller **logical networks**.
- **Subnet Masks** assist in:
    - Determining the **network portion** of an IP address.
    - Identifying the **host portion** inside a subnet.
    - Deciding whether a host is on a **local network** or **remote network** (beyond current discussion scope).

#### **Key Points on Subnetting**

- **All '1's** in the subnet mask represent the **network address**.
    
- **All '0's** represent the **host address**.
    
- **Example**:
    
    - IP: `192.168.123.456`
    - Subnet Mask: `255.255.255.0`
    - **Network Address**: Formed by all '1's in the subnet mask.
    - **Host Address**: Formed by the remaining '0's after the network portion is extracted.

---

### **Key Takeaways**:

- **Subnetting** divides larger networks into smaller sub-networks.
- **Subnet mask** is essential for determining the **network address** and **host address**.
- **Routers** perform bitwise AND operations to separate network and host portions in an IP address.
- Subnet masks help in determining whether a host is on the **local network** or **remote network**.





### References
