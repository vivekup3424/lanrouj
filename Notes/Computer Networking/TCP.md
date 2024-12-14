---
tags:
  - transport-layer
  - network
  - tcp
---
Since TCP allows a single ackowledgment (ACK) for multiple incoming packets, the receiver must advertise to the sender on much space it has available (receiver buffer), before it sends an ackowledgement.
When a program reads data on a connection, it reads it from the buffer of the client and server.
ACK packets contains *window size* which is the number of bytes  the sender can send the data to receiver without requiring an acknowledgement.

 ---

### Sliding Window
Both the client and the server keep track of each other’s window size and
do their best to completely fill each other’s receive buffers. 
This method of *receiving the window size in an ACK packet, sending data, receiving an*
*updated window size in the next ACK*, and then sending more data—is
known as a sliding window.

![[Pasted image 20241209221518.png]]

 ---
 
### Graceful Termination of TCP Session

Either side (client or server) of the connection may initiate the termination sequence by sending a finish (**FIN**) packet.  
![[Pasted image 20241209221806.png]]  

#### Importance of TIME_WAIT

The **TIME_WAIT** state plays a critical role in the termination process:  
- After the server sends a **FIN** packet, the client acknowledges it by sending an **ACK** packet.  
- The client then enters the **TIME_WAIT** state, whose purpose is to ensure the server receives the client’s final **ACK** packet.  

During the **TIME_WAIT** state:  
1. The client waits for **twice the maximum segment lifetime (MSL)**.  
   - By default, MSL is set to **two minutes**, as specified in **RFC 793**.  
   - This value can typically be configured in the operating system.  
2. After waiting, the client transitions the connection state to **CLOSED**, requiring no further input from the server.  

---

### Abrupt Termination of TCP Connections

Not all TCP connections close smoothly. Sometimes, the application using the connection may crash or stop suddenly.  

When this happens:  
1. The TCP connection is closed immediately.  
2. If the other side tries to send data:  
   - The closed side responds with a **reset (RST)** packet.  
   - The **RST packet** tells the sender that the connection is no longer available and no more data will be accepted.  
3. The sender should stop sending data and close its side of the connection, knowing that any unacknowledged packets were ignored.  

Additionally:  
- Intermediate devices like firewalls can also send **RST packets** to both sides of a connection, effectively ending it from the middle.  

> [!NOTE]
> The **RST packet** immediately terminates a TCP connection when one side crashes, stops, or an intermediate node interrupts, signaling the sender to stop communication.

---

### Creating TCP Server
1