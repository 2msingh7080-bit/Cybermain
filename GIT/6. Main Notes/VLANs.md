2024-10-13 20:57
[[Network Fundamentals]]
Status: done 

Tags:

# VLANs
### Virtual Local Area Networks (VLANs)

**Concept of VLANs**:

- **Definition**: A VLAN (Virtual Local Area Network) is a segmented portion of a larger local area network (LAN) that allows for efficient data communication within smaller, isolated groups.
- **Functionality**: Just as physical LANs operate within a defined range, VLANs serve a similar purpose but are created virtually using switches.

### Characteristics of VLANs

- **Segmentation**: VLANs divide a larger LAN into smaller segments (sub-networks), enabling better organization and management of network resources.
- **Virtual Nature**: Unlike physical LANs, VLANs do not require separate physical infrastructure for each department or segment; instead, they utilize a single switch that is partitioned.

### Use Case: Company Departments

1. **Example Scenario**:
    
    - A tech company has several departments (e.g., Sales, Marketing, Customer Care) that require distinct networks for data management.
    - Instead of purchasing multiple switches for each department, one switch can be used to create several VLANs.
2. **Benefits**:
    
    - Each department operates within its own VLAN without interfering with others, allowing for organized data flow and security.

### Communication within VLANs

- **Node Communication**:
    
    - Nodes (devices) within the same VLAN can communicate freely.
    - Nodes in different VLANs cannot communicate directly without additional routing functionality.
- **Routing Requirement**:
    
    - For communication between different VLANs (e.g., Sales needing to communicate with Marketing), a router must be implemented. This router facilitates inter-VLAN communication.

### Routing Functionality

- **Segregation**: Each VLAN remains independent, meaning that nodes can only send messages to devices within their own VLAN unless routing is enabled.
- **Router Role**: The router connects the VLANs, allowing devices in different VLANs to communicate when necessary.

### Summary

- **VLANs**:
    
    - VLANs are virtual partitions of a larger network that enable multiple segments to function independently.
    - They enhance network management, security, and efficiency without requiring extensive physical infrastructure.
- **Communication Dynamics**:
    
    - Devices within the same VLAN can communicate freely, while communication across different VLANs requires a routing device.
- **Importance of Routers**: To enable communication between VLANs, routers must be integrated into the network architecture.
    

### Next Steps:

- The next discussion will cover the types of VLANs based on the services they provide and how they can be effectively utilized in network management.

## Types of VLANs Based on Services

**1. Default VLAN**:

- **Description**: The default VLAN is pre-configured and exists in every switch.
- **Functionality**:
    - All connected devices (nodes) are part of this VLAN with no segmentation.
    - If no specific configuration is applied, all nodes connect to the default VLAN (e.g., all four nodes connected will belong to this VLAN).

---

**2. Data VLAN**:

- **Purpose**: Primarily used to handle data traffic between nodes.
- **Functionality**:
    - Focuses on managing user data traffic over the network.
    - Prioritizes data transfer, ensuring efficient handling of data packets.

---

**3. Voice VLAN**:

- **Purpose**: Designed to prioritize voice traffic, specifically Voice over IP (VoIP).
- **Functionality**:
    - Optimizes network resources for voice traffic, ensuring high-quality audio communication.
    - Provides utmost priority to voice traffic over other types of data, facilitating clearer and uninterrupted calls.

---

**4. Management VLAN**:

- **Purpose**: Utilized for managing network resources and monitoring VLAN performance.
- **Functionality**:
    - Observes and controls network operations across different VLANs.
    - Ideal for network administrators to track performance and ensure proper management of devices connected within different VLANs.

---

**5. Native VLAN**:

- **Purpose**: A special type of VLAN that supports both internal and external traffic.
- **Functionality**:
    - Associated with IEEE 802.1Q trunking, it handles traffic from both devices within the VLAN and devices that are outside of it.
    - For example, if there are eight nodes in a VLAN and two additional nodes not part of the VLAN, the native VLAN will manage traffic for all ten nodes.
    - Ensures seamless communication by managing traffic from both VLAN nodes and non-VLAN nodes.

---

### Summary

- **VLAN Types**:
    - **Default VLAN**: All nodes connect without segmentation.
    - **Data VLAN**: Focuses on user data traffic management.
    - **Voice VLAN**: Prioritizes voice communications, particularly VoIP.
    - **Management VLAN**: Used for monitoring and managing network resources.
    - **Native VLAN**: Supports traffic for both VLAN and non-VLAN nodes.

These VLAN types help in organizing network traffic efficiently, providing better performance and management tailored to different communication needs within a network.

# Collision Domains and Broadcast Domains

## Introduction

- **Key Concepts**: The focus is on two critical areas in networking:
    - **Collision Domain**
    - **Broadcast Domain**

### Definitions

- **Domain**: Refers to an area where specific events can occur.
    - **Collision Domain**: An area where packet collisions can occur when nodes share a communication channel.
    - **Broadcast Domain**: An area where all nodes can receive broadcast messages sent by any device within that area.

## Collision Domain

- **Definition**: An area where data packet collisions can occur due to nodes using a shared medium.
- **Characteristics**:
    - Collisions happen when multiple nodes attempt to send packets simultaneously.
    - Common in networks using Ethernet hubs (which are not intelligent devices and flood the network).
    - In half-duplex communication, only one node can send data at a time, leading to potential collisions.

### Key Points:

1. **Hub**:
    - All ports on a hub share the same collision domain.
    - If a collision occurs, it affects all devices connected to the hub.
2. **Switch/Router**:
    - Each port on a switch or router is a separate collision domain.
    - This design reduces the chances of collisions by isolating traffic.

### Example Scenario:

- If two devices connected to a hub send packets simultaneously, a collision occurs because they share the same communication channel.

## Broadcast Domain

- **Definition**: An area where nodes can receive broadcast messages sent by any device within that area.
- **Characteristics**:
    - Broadcast messages reach all devices within the broadcast domain.
    - Routers separate broadcast domains, preventing broadcast messages from crossing to other domains.

### Key Points:

1. **Broadcast Message**:
    - When a node sends a broadcast message, all nodes within that broadcast domain receive it.
2. **Separation of Domains**:
    - Each port of a router creates a new broadcast domain, meaning messages do not propagate across router boundaries.

### Example Scenario:

- If a node sends a broadcast message, all other nodes in that same broadcast domain will receive it.

## Differences Between Collision Domains and Broadcast Domains

| Feature                   | Collision Domain                                  | Broadcast Domain                            |
| ------------------------- | ------------------------------------------------- | ------------------------------------------- |
| **Definition**            | Area where packet collisions can occur            | Area where broadcast messages are received  |
| **Device Type**           | Typically defined by Ethernet hubs                | Defined by routers and VLANs                |
| **Separation**            | Each port of a switch/router is a separate domain | Each port of a router is a separate domain  |
| **Impact on Performance** | Affects data transmission due to collisions       | Affects message delivery across the network |

## Conclusion

- **Collision Domain**: Defined as an area under which packet collisions can occur due to shared communication channels, typically seen in Ethernet hubs.
- **Broadcast Domain**: Defined as an area where broadcast messages can be received by all nodes, separated by routers.
- Understanding these concepts is crucial for effective network design and management.
Here's a detailed summary of the video transcription regarding the identification of collision and broadcast domains in a network:

## Summary of Collision and Broadcast Domains

#### 1. Introduction

- The video introduces a Semitic network and tasks viewers with determining the number of **collision domains** and **broadcast domains** present in the network.

#### 2. Understanding Domains

- **Broadcast Domain**: A network segment where a broadcast message is transmitted to all devices. Broadcast domains are separated by routers.
- **Collision Domain**: A network segment where data packets can collide with one another. Each port of a switch or router creates a separate collision domain. Hubs, on the other hand, share a single collision domain for all ports.

#### 3. Identifying Broadcast Domains

- The focus is initially on **broadcast domains** as they are simpler to identify.
- In the presented network:
    - There is **one router**.
    - Each port of the router creates separate broadcast domains.
    - The network is divided into **two broadcast domains**:
        - **Broadcast Domain A**: Includes all devices connected to the left side of the router.
        - **Broadcast Domain B**: Includes all devices connected to the right side of the router.

#### 4. Behavior of Broadcast Messages

- When a device sends a broadcast message:
    - The switch receives it and forwards it to all devices in the respective broadcast domain, but it does not cross into the other domain due to the router acting as a barrier.

#### 5. Identifying Collision Domains

- **Collision Domains** are more complex to identify:
    - Each port on a switch or router acts as a separate collision domain.
    - In the network:
        - **Left Side**:
            - Two hubs, each connected to three nodes.
            - A switch with four ports creates four collision domains.
        - **Right Side**:
            - The router also has two ports creating additional collision domains.
- Total collision domains calculation:
    - **Four collision domains** from the switch.
    - **Two collision domains** from the router.
    - Total collision domains = **4 (left) + 4 (right) + 2 (router) = 10 collision domains**.

#### 6. Conclusion

- The final count for the network is:
    - **10 collision domains**
    - **2 broadcast domains**

### Key Takeaways

- Each port of a switch or router is a separate collision domain.
- Broadcast domains are determined by routers, while collision domains are influenced by switches and hubs.
- Understanding these domains is crucial for network design and troubleshooting, ensuring efficient data transmission and minimizing packet collisions.

This structured approach provides a clear understanding of the concepts discussed in the video, focusing on the distinctions between collision and broadcast domains and their relevance in network architecture.


### References
