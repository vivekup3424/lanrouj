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
### Three-way Handshake
<img src="3-s2.0-B9780128182000000160-f05-09-9780128182000.jpg" width="600">

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

### TCP States
- CLOSED: There is no connection.
- LISTEN: The local end-point is waiting for a connection request from a remote end-point i.e. a passive open was performed.
- ESTABLISHED: The third step of the three-way connection handshake was performed. The connection is open.
- FIN-WAIT-1: The first step of an active close (four-way handshake) was performed. The local end-point has sent a connection termination request to the remote end-point.
- CLOSE-WAIT: The local end-point has received a connection termination request and acknowledged it e.g. a passive close has been performed and the local end-point needs to perform an active close to leave this state.
- FIN-WAIT-2: The remote end-point has sent an acknowledgement for the previously sent connection termination request. The local end-point waits for an active connection termination request from the remote end-point.
- LAST-ACK: The local end-point has performed a passive close and has initiated an active close by sending a connection termination request to the remote end-point.
- CLOSING: The local end-point is waiting for an acknowledgement for a connection termination request before going to the TIME-WAIT state.
- TIME-WAIT: The local end-point waits for twice the maximum segment lifetime (MSL) to pass before going to CLOSED to be sure that the remote end-point received the acknowledgement.

FIN_WAIT_2 seems to occur when the server has an active connection with a client and wants to shut down the TCP connection (probably in response to a normal application layer "exit"). The server sends the client a packet with a "FIN" bit set. At this point, the server is in FIN_WAIT_1 state. The client gets the FIN packet and goes into CLOSE_WAIT state, and sends an acknowledgment packet back to the server. When the server gets that packet, it goes into FIN_WAIT_2 state. From the server's perspective, the connection is now closed, and the server can't send any more data. However, under the TCP protocol, the client needs to shut down also by sending a FIN packet, which the server TCP implementation should ACK. The server should close after a period of time defined by the Maximum Segment Lifetime (MSL).


![893-screen-shot-2015-08-03-at-52034-pm.png](https://www.googlecloudcommunity.com/gc/image/serverpage/image-id/3799i814E8606C2F3E657/image-size/large?v=v2&px=999 "893-screen-shot-2015-08-03-at-52034-pm.png")
