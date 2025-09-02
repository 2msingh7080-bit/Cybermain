2024-10-13 20:09
[[Network Fundamentals]]
Status:

Tags: 

# OSI Model (Open Systems Interconnection)
## 1. Introduction to the OSI Model's Upper Layers

- The OSI model is divided into seven layers, each responsible for different networking functions.
- The **upper layers** of the OSI model include:
    1. **Application Layer (Layer 7)**
    2. **Presentation Layer (Layer 6)**
    3. **Session Layer (Layer 5)**
- These upper layers are primarily responsible for application-related services and end-to-end communication management.

---

## 2. Layers in Detail

### a. **Application Layer (Layer 7)**

- **Role**:
    
    - Interfaces directly with software applications.
    - Handles the protocols and services required for communication between applications on different devices.
- **Functions**:
    
    - Manages protocols such as **DHCP** (Dynamic Host Configuration Protocol), **DNS** (Domain Name System), and **HTTP** (Hypertext Transfer Protocol).
    - All communication that your software applications require (like web browsing or file transfers) is initiated and managed by this layer.
- **Example**:
    
    - When using an application like **Facebook**, the data exchange and communication process between Facebook's servers and your device is governed by the Application Layer.

### b. **Presentation Layer (Layer 6)**

- **Role**:
    
    - Converts the data format used by the application into a format that the network layers can understand and vice versa.
- **Functions**:
    
    - Acts as a translator between the application and the network.
    - Ensures that the data format used by an application (e.g., Facebook) is translated into a language the computer can understand and process.
- **Example**:
    
    - If Facebook uses a specific data format (e.g., Language X) that is not understood by the computer (which understands Language Y), the Presentation Layer converts Language X to Language Y, enabling the network to process the data.
- **Explanation**:
    
    - It ensures data integrity by formatting, encrypting, and compressing data as necessary before sending it to the lower layers for transmission.

### c. **Session Layer (Layer 5)**

- **Role**:
    
    - Manages sessions (communication channels) between two devices or nodes.
- **Functions**:
    
    - Establishes, maintains, and terminates communication sessions.
    - Ensures that the devices have a communication channel before transmitting data.
- **Session Lifecycle**:
    
    - **Session Creation**: Opens a channel for communication when both devices are ready.
    - **Session Maintenance**: Manages data exchange during communication.
    - **Session Termination**: Closes the communication channel once data exchange is complete.
- **Example**:
    
    - Before two devices exchange messages, a session (or channel) is created by the Session Layer. Once communication ends, the session is terminated.

---

## 3. Summary of Key OSI Upper Layers

- **Layer 7 (Application Layer)**:
    - Provides services for software applications (e.g., web browsing, file transfers).
- **Layer 6 (Presentation Layer)**:
    - Translates data between application formats and formats the computer or network can understand.
- **Layer 5 (Session Layer)**:
    - Establishes and manages communication sessions between devices.

---

## 4. Conclusion

Understanding the roles of these upper layers is crucial for efficient data transmission between applications and devices. Each layer serves a unique function that ensures data is properly formatted, transmitted, and received without errors, enabling smooth communication over networks.

### **Key Takeaways**:

- **Application Layer** (Layer 7) interacts directly with software and manages application-level services.
- **Presentation Layer** (Layer 6) ensures data format compatibility between the application and the network.
- **Session Layer** (Layer 5) manages the start, maintenance, and termination of communication channels.
### Physical Layer

#### 1. **Transport Layer (Layer 4)**

- **Heart of the OSI Model**: Known for its critical role in ensuring data is transported efficiently and accurately between devices.
- **Functions**:
    - Manages data transportation over established channels.
    - **Flow Control**: Ensures data is transmitted in an orderly and managed fashion.
    - **Sequencing**: Keeps track of the order in which data packets are sent and received.
    - **Port Numbers**: Responsible for defining port numbers used by communicating applications.
    - **Protocols**: Uses **TCP (Transmission Control Protocol)** or **UDP (User Datagram Protocol)** for data transmission.
    - **Segmentation**: Breaks data into smaller packets for transmission and reassembles them upon reception.
- **Importance**: Oversees where and how messages are sent.

#### 2. **Network Layer (Layer 3)**

- **Role**: Handles the routing of data across different networks using IP addresses.
- **Functions**:
    - **IP Addressing**: Adds IP addresses of the sender and receiver to ensure correct delivery.
    - **Routing & Switching**: Manages the path through which data packets travel across networks.
    - **Gateways & Subnetting**: Handles the technical aspects of moving data through different networks and subnetworks.
- **Key Concept**:
    - **IP Address = Layer 3 Address**: IP addresses are associated with Layer 3, and are also called **Layer 3 addresses**.
    - **Packets**: Data at this layer is referred to as **data packets**.

#### 3. **Data Link Layer (Layer 2)**

- **Role**: Ensures reliable data transfer between adjacent network nodes by managing the physical link between devices.
- **Functions**:
    - **MAC Addressing**: Adds **MAC (Media Access Control) addresses**, used for identifying hardware addresses within the same network.
    - **Error Detection**: Checks for transmission errors to ensure data integrity.
    - **Flow Control**: Manages the speed of data transfer to prevent overloading a device.
- **Key Concept**:
    - **MAC Address = Layer 2 Address**: MAC addresses are specific to this layer, often referred to as **Layer 2 addresses**.
    - **Frames**: Data at this layer is packaged as **data frames** instead of packets.

#### 4. **Physical Layer (Layer 1)**

- **Role**: Converts data frames into physical signals for transmission over communication media.
- **Functions**:
    - **Signal Conversion**: Converts data frames from the Data Link Layer into binary signals (0s and 1s) to be sent over cables, radio waves, or other transmission media.
    - **Physical Transmission**: Responsible for actual data transmission over Ethernet cables, Wi-Fi, or fiber optics.
    - **Cable Characteristics & Frequency**: Determines the type of cables, voltage levels, and transmission frequencies required for data transfer.
- **Transmission Modes**:
    - **Full Duplex**: Allows simultaneous two-way communication.
    - **Half Duplex**: Supports two-way communication but not at the same time.
    - **Simplex**: One-way communication only.

#### Key Concepts to Remember:

- **Layer 4 (Transport Layer)**: Manages transport of data between devices.
- **Layer 3 (Network Layer)**: Focuses on routing and IP addressing.
- **Layer 2 (Data Link Layer)**: Manages MAC addressing and prepares data for physical transmission.
- **Layer 1 (Physical Layer)**: Handles the actual sending of signals and data over physical media.

- ### Key Takeaways

- The **Transport Layer** handles data flow and ensures messages are correctly transmitted and received.
- The **Network Layer** is responsible for routing and logical addressing (IP addresses) of data packets.
- The **Data Link Layer** adds hardware (MAC) addresses and manages data frames.
- The **Physical Layer** handles the conversion of data into signals for transmission through a physical medium.
## Real-World Application with Facebook Messenger Example

The video explains how the **OSI model**'s seven layers interact when sending a message through a Facebook Messenger-like application, breaking down the role of each layer in the process.

#### 1. **Application Layer**

- The sender types a message ("Hello") using Facebook Messenger.
- Facebook Messenger operates at the **Application Layer**.
- The message is passed from the sender’s application to the receiver’s application, which also runs Facebook Messenger.

#### 2. **Presentation Layer**

- **Converts** the message into a format understood by the computer, typically binary or **ASCII codes**.
- Example: "Hello" is converted into binary digits or ASCII codes that the system can interpret.

#### 3. **Session Layer**

- **Establishes a session** (communication link) between the sender and receiver's devices.
- Creates a **tunnel** between the two applications (sender and receiver).
- Ensures that a communication channel exists between the devices before data transfer happens.
- The session is **terminated** when communication is no longer needed.

#### 4. **Transport Layer**

- **Adds port numbers** to the message for application identification.
    - Example: Facebook Messenger might use **Port 50**.
- Ensures that the data is transported reliably, handling transport protocols such as **TCP** or **UDP**.

#### 5. **Network Layer**

- **Adds IP addresses** of both the sender and receiver to the data packet.
    - This allows the data to be routed to the correct device.
- Adds **routing, switching**, and **subnet information** to the packet for proper delivery.

#### 6. **Data Link Layer**

- Adds **MAC addresses** (physical addresses) of both the sender and receiver.
    - Data is referred to as a **frame** at this layer.
    - Ensures data is sent to the correct device on the network.

#### 7. **Physical Layer**

- Converts the data into **binary bits** (signals) to transmit over a wired or wireless channel.
- The signals are sent from the sender’s physical medium (hardware) to the receiver’s.

---

### Message Reception Process

#### 1. **Physical Layer**

- The receiver’s **Physical Layer** accepts the incoming signals.
- Converts the binary signals back into **frames**.

#### 2. **Data Link Layer**

- The **Data Link Layer** extracts the sender's and receiver’s **MAC addresses** from the frame.
- Passes the frame (now referred to as a packet) to the **Network Layer**.

#### 3. **Network Layer**

- **Extracts IP addresses** from the packet.
- Routes the data based on these addresses and forwards the packet to the **Transport Layer**.

#### 4. **Transport Layer**

- Verifies the **port numbers** to ensure the data is sent to the correct application.
    - Example: Verifies that the data is meant for Port 50 (used by Facebook Messenger).

#### 5. **Session Layer**

- Maintains the **session** between the sender and receiver.

#### 6. **<span style="color:rgb(20, 196, 255)">Presentation Layer</span>**

- Converts the **binary/ASCII codes** back into a readable format.
- Transforms the data back into something Facebook Messenger can understand, such as the original "Hello" message.

#### 7. **<span style="color:rgb(20, 196, 255)">Application Layer</span>**

- Facebook Messenger displays the message ("Hello") to the receiver.

---

### <span style="color:rgb(20, 196, 255)">Key Takeaways:</span>

- **OSI model layers** work together to ensure seamless data transmission.
- The **Application Layer** interacts directly with user applications like Facebook Messenger.
- Layers add specific information to data as it passes down through the stack (e.g., **IP addresses, port numbers, MAC addresses**).
- At the receiver’s end, the process is reversed, extracting the added information layer by layer to display the original message.
# Networking Devices and OSI Model Layers

- **OSI Model Overview**:
    - The OSI (Open Systems Interconnection) model consists of seven layers. Networking devices operate on specific layers of this model.

#### **Physical Layer (Layer 1)**:

- **Devices**: Repeater and Hub
    - **Function**: These devices transfer data signals from one node to another without considering the addresses of the nodes.
    - **Layer 1 Focus**: They operate purely on the physical transmission of data signals, not on addressing or packet structure.

#### **Data Link Layer (Layer 2)**:

- **Devices**: Switch and Bridge
    - **Function**: These devices work with MAC (Media Access Control) addresses, which are Layer 2 addresses.
    - **Layer 2 Focus**: Switches and bridges use MAC addresses to identify devices and route data within the network based on these addresses.

#### **Network Layer (Layer 3)**:

- **Device**: Router
    - **Function**: A router works with IP addresses (Layer 3 addresses) to route data across networks.
    - **Layer 3 Focus**: This layer is responsible for packet forwarding, including routing through different networks based on IP addresses.

#### **Multilayer Switch**:

- **Special Device**: Multilayer Switch (or Layer 3 Switch)
    - **Function**: This switch can operate on multiple layers of the OSI model, including both Layer 2 (MAC addresses) and Layer 3 (IP addresses).
    - **Role**: It combines the functionality of both a router (Layer 3) and a switch (Layer 2) in one device, allowing it to handle both MAC and IP addresses.

### Summary:

- **Layer 1 (Physical)**: Repeater, Hub
- **Layer 2 (Data Link)**: Switch, Bridge
- **Layer 3 (Network)**: Router
- **Multilayer Device**: Multilayer Switch (combines Layer 2 and Layer 3 functionalities)

### Networking Switching Techniques

**Concept of Switching**:

- **Definition**: In networking, switching refers to the process of selecting the most efficient path for a message to travel from the sender to the receiver.
- **Application**: This involves choosing the best route out of multiple available options for effective communication between devices.

## Types of Switching in Networking

1. **Message Switching**:
    
    - **Definition**: This technique involves intermediary nodes between the sender and receiver.
    - **Process**:
        - The message (or data) is divided into smaller packets.
        - Each packet is sent to an intermediary device, which stores them temporarily.
        - The intermediary device collects all packets and forwards them to the next node.
    - **Example**:
        - If a 10 MB file is sent, it gets split into 10 packets of 1 MB each. Each packet is stored at the intermediary nodes until all packets are received.
2. **Circuit Switching**:
    
    - **Definition**: This technique establishes a preplanned connection between the sender and receiver before the transmission of messages.
    - **Process**:
        - A dedicated communication path is created for the entire duration of the message transmission.
        - Once the connection is established, packets are sent through this predetermined path.
    - **Characteristics**:
        - The path is allocated in advance, ensuring consistent data transfer.
3. **Packet Switching**:
    
    - **Definition**: In this method, messages are divided into packets, and each packet is sent independently across the network.
    - **Types**:
        - **Datagram Approach**:
            - Each packet is sent individually with both the sender's and receiver's addresses included.
            - There is no preplanned connection; packets may take different routes to reach the destination.
        - **Virtual Circuit Approach**:
            - A preplanned path is established for the packets.
            - Each packet also contains both addresses, combining features of both datagram and circuit switching.
            - This approach ensures that packets follow a specific route while still being addressed properly.

### Summary:

- **Switching** is essential in networking for determining the most efficient path for data transmission.
- **Types of Switching**:
    - **Message Switching**: Involves intermediary devices and temporary storage.
    - **Circuit Switching**: Preplanned connection with dedicated paths for communication.
    - **Packet Switching**: Uses packets sent independently, with two main approaches—datagram (no preplanned path) and virtual circuit (with preplanned path).



### References

