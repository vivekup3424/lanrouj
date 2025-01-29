---
tags:
  - bridge
  - bridges
  - LAN
---
# Bridges
---

## **Bridge in Computer Network**

- A **bridge** is a networking device that connects multiple **LANs** into a larger LAN.
- Operates at **Layer 2 (Data Link Layer)** of the **OSI model**.
- Helps in **network segmentation** by dividing the network into sections, reducing collisions.
- Improves network **performance** by filtering and forwarding data based on **MAC addresses**.

### **Example**

- A company has two separate LANs: **LAN A (10 PCs)** and **LAN B (15 PCs)**.
- A **bridge** connects both LANs, allowing communication while managing traffic efficiently.

---

## **Types of Bridges**

1. **Transparent Bridge**
    
    - Invisible to network devices.
    - **Filters/forwards** data using MAC addresses.
    - No need for reconfiguration when devices are added/removed.
    - **Example:** Common in Ethernet networks.
2. **Source Routing Bridge**
    
    - Designed by **IBM** for **Token Ring networks**.
    - The **source station** determines the path for data packets.
    - **Example:** Used in older networks where predefined routes were required.
3. **Translational Bridge**
    
    - Converts data between **different network types** (e.g., Ethernet ↔ Token Ring).
    - Ensures **compatibility** between different networking systems.
    - **Example:** Connecting an **Ethernet network** to a **Fiber-optic network**.

---

## **Working of a Bridge**

1. **Receiving Data** → Gets data packets (frames) from connected LANs.
2. **Building a MAC Table** → Learns device locations by examining data sources.
3. **Filtering Data** → Stops unnecessary traffic if the sender and receiver are on the same network.
4. **Forwarding Data** → Sends data to the correct destination LAN if needed.
5. **Repeating for Both Sides** → Performs the same process for incoming data from both networks.

### **Example**

- If **PC1 (LAN A) sends data to PC2 (LAN A)** → The bridge **blocks** it.
- If **PC1 (LAN A) sends data to PC3 (LAN B)** → The bridge **forwards** it.

---

## **Models of Bridging**

1. **Local Bridging**
    
    - Connects **LAN switches** using physical cables.
    - Used within the **same geographic location**.
    - **Example:** Connecting **two office networks** in the same building.
2. **Remote Bridging**
    
    - Connects **distant LANs** over a **WAN**.
    - Used when LANs are in **different cities or locations**.
    - **Example:** Connecting a **New York** office LAN to a **London** office LAN.

---

## **Uses of Bridges**

- Expands **network capacity** by integrating multiple LANs.
- Decides whether to **accept/reject** data packets.
- Transmits data in **multi-node networks** (OSI model).
- Broadcasts data when **MAC addresses are unknown**.
- Ensures **fault tolerance** by forwarding data despite faulty nodes.

---

## **Functions of Bridges**

- **Segments LANs** to improve performance.
- **Controls network traffic** by filtering packets.
- **Connects LANs** using similar protocols.
- **Filters data** based on MAC addresses.

---

## **Advantages of Bridges**

✔ **Network Extension** → Connects different LAN topologies.  
✔ **Increased Bandwidth** → Each segment has a separate collision domain.  
✔ **Protocol Compatibility** → Supports different MAC protocols.  
✔ **Reliability & Maintainability** → Easy to install and manage.  
✔ **No Additional Hardware** → Only requires the bridge itself.

---

## **Disadvantages of Bridges**

❌ **Expensive** → Costlier than hubs and repeaters.  
❌ **Slow Processing** → Needs time to analyze MAC addresses.  
❌ **High Broadcast Traffic** → Can lead to **broadcast storms**.  
❌ **Limited Data Filtering** → Cannot filter individual packets efficiently.