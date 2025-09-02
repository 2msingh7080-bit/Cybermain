2025-01-30 14:20

Status:

Tags:

# Bus Topology

### **1. Introduction to Bus Topology**

- **Definition**: A network topology where all nodes (devices) are connected to a **single central cable**, called the **backbone cable**.
- **Why "Bus" Topology?**:
    - The backbone resembles a **bus** that carries data between devices.
    - Every node is directly connected to this main cable.

---

### **2. How Bus Topology Works**

- **Data Transmission**:
    - When a node sends data, it travels along the backbone cable.
    - Every node on the network receives the data **regardless** of whether it is the intended recipient.
- **Issue**: Wastage of bandwidth occurs since all nodes receive every transmission.
- **Solution**: **Token-Based Transmission**
    - Each node is assigned a **unique token number**.
    - Data is sent with both:
        - **Sender’s token**
        - **Recipient’s token**
    - Nodes ignore data unless their **token number matches**, reducing unnecessary transmissions.

---

### **3. Example Scenario**

![[Pasted image 20250130142111.png]]

1. A **laptop** (Node 1) wants to send data to a **printer** (Node 5).
2. The message is broadcasted to **all nodes** along with a **recipient token** (Token 5).
3. Nodes that **don’t match** the token **discard the message**.
4. The **printer recognizes its token**, accepts the message, and prints the data.

---

### **4. Advantages & Disadvantages of Bus Topology**

#### ✅ **Advantages**:

- **Cost-effective**: Requires less cabling.
- **Easy to install**: Simple setup, making it ideal for **small offices or networks**.
- **Requires minimal hardware**: No need for complex switches or routers.

#### ❌ **Disadvantages**:

- **Limited scalability**: As more nodes are added, performance **degrades**.
- **High data collisions**: Since multiple devices send data on a single channel.
- **Single point of failure**: If the **backbone cable** fails, the entire network **stops working**.
- **Slower performance**: More devices lead to network congestion.

---

### **5. When to Use Bus Topology?**

- **Best suited for**:
    - **Small networks** (e.g., home networks, small offices).
    - **Temporary setups** where quick installation is needed.
    - **Simple networks** that do not require high-speed data transmission.

---

### **Key Takeaways**

- **Bus topology uses a single backbone cable** to connect all devices.
- **Data is broadcasted to all nodes**, which can **cause bandwidth wastage**.
- **Token-based transmission** improves efficiency by allowing only the recipient node to accept data.
- **Best for small networks**, but **scalability and reliability issues** limit its use in large setups.






### References
