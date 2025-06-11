---
id: Websockets
aliases: []
tags: []
---

### Pre-WebSocket Communication: HTTP Abuses and Alternatives  

Before the advent of WebSockets as defined in **RFC 6455**, bidirectional communication over HTTP relied on techniques like **long polling** and **streaming**, introduced in **RFC 6202**. These methods often "abused" HTTP, which wasn't designed for persistent server-to-client communication.

---

### HTTP Abuses for Bidirectional Communication  
#### 1. **HTTP Polling**  
   - **Usage**: The client sends requests at regular intervals to check for updates (server push).  
   - **Drawbacks**:  
     1. Generates unnecessary server load due to frequent, redundant requests.  
     2. Increases bandwidth usage, even if no new data exists on the server.  
     3. Resource-intensive, leading to inefficiency.  

#### 2. **Long Polling**  
   - **Purpose**: Reduces latency by keeping the connection open until new data is available.  
   - **Lifecycle**:  
     1. Client sends a request and waits for a response.  
     2. Server holds the connection until data is available or a timeout occurs.  
     3. Server sends the response, and the connection closes.  
     4. Client sends another request if needed, ensuring minimal delay for new data.  
   - **Advantages**: Better than polling for real-time updates but still not ideal.  
   - **Issues**: High resource usage as connections remain open longer.  

#### 3. **HTTP Streaming**  
   - **What It Is**: The server keeps the connection open and sends updates to the client as events occur.  
   - **Challenges**:  
     1. Strains server resources, as HTTP wasn't designed for prolonged open connections.  
     2. Issues with connection timeouts and load balancers.  

---

### WebSocket Benefits and Use Cases  

#### **Notable Uses**:  
1. **Messaging Apps**: WhatsApp and similar platforms rely on WebSockets for low-latency communication.  
2. **Multiplayer Games**: WebSocket connections enable stateful, real-time interaction.  
   - **Challenges**:  
     1. Each client maintains a connection with the server, making the system stateful.  
     2. Scaling becomes difficult: Horizontal scaling is inefficient; vertical scaling (e.g., upgrading hardware) is required.  
   - **Example**:  
     - Supporting 100 players is feasible.  
     - Scaling to 1000+ players requires substantial infrastructure upgrades.  
3. **File Transfers**: Track upload/download progress dynamically.  

> **Tip**: Don't be attached to any one technology. Alternatives can solve specific problems more effectively.

---

### WebSocket Communication Lifecycle  

#### **Opening Handshake**  
1. **Request**: Initiated over HTTP/1.1 using an **upgrade request**.  
```http
   GET /chat HTTP/1.1  
   Host: server.example.com  
   Connection: upgrade  
   Upgrade: websocket  
   Origin: http://example.com  
   Sec-WebSocket-Key: NnRlZW4gYnl0ZXMgbG9uZw==  
   Sec-WebSocket-Protocol: html-chat, text-chat  
   Sec-WebSocket-Version: 13
```

2. **Meaning of Headers**:  
   - **`GET /chat`**: Specifies the WebSocket endpoint.  
   - **`Host`**: Server hostname.  
   - **`Connection: upgrade`**: Requests a protocol switch.  
   - **`Upgrade: websocket`**: Specifies the desired protocol.  
   - **`Origin`**: Indicates the client's origin for CORS validation.  
   - **`Sec-WebSocket-Key`**: A unique Base64-encoded key for handshake validation (16 bytes before encoding, 24 characters after).  
   - **`Sec-WebSocket-Protocol`**: Specifies supported subprotocols like `html-chat`.  
   - **`Sec-WebSocket-Version`**: Indicates protocol version (13 is standard).  

#### **Server Response**:  
- If accepted, the server responds:  
```http
   HTTP/1.1 101 Switching Protocols  
   Connection: upgrade  
   Upgrade: websocket  
   Sec-WebSocket-Accept: 5TJpHv9RoAl7w8ytsXcWxTOZ9Q==  
   Sec-WebSocket-Protocol: new-chat
```  
> [!NOTE]
> - **101 Status Code**: Indicates a successful protocol switch.  
> - **`Sec-WebSocket-Accept`**: A hashed response derived from `Sec-WebSocket-Key` to validate the handshake.  

Once this exchange is complete, the WebSocket connection enters the **OPEN** state for full-duplex communication.  

--- 

> [!WARNING] 
>  While WebSockets are powerful, evaluate their necessity. Alternatives like Server-Sent Events (SSE) or HTTP/3 can address specific use cases.

#### How server computes the Sec-WebSocket-Accept from Sec-Websocket-Key ??

1. **Read `Sec-WebSocket-Key`**:  
   Extract the key from the request headers. Example:  
   ```
   Sec-WebSocket-Key: NnRlZW4gYnl0ZXMgbG9uZw==
   ```

2. **Concatenate with Magic String**:  
   Append the constant `258EAFA5-E914-47DA-95CA-C5AB0DC85B11` to the key:  
   ```
   NnRlZW4gYnl0ZXMgbG9uZw== + 258EAFA5-E914-47DA-95CA-C5AB0DC85B11
   ```

3. **Compute SHA-1 Hash**:  
   Generate the SHA-1 hash of the concatenated string:  
   ```
   SHA1(NnRlZW4gYnl0ZXMgbG9uZw==258EAFA5-E914-47DA-95CA-C5AB0DC85B11) = e53269001eff51a0097bc3ccadb17716c53399f5
   ```

4. **Base64 Encode the Hash**:  
   Convert the hash into a Base64-encoded string:  
   ```
   Base64(e53269001eff51a0097bc3ccadb17716c53399f5) = 5TJpHv9RoAl7w8ytsXcWxTOZ9Q==
   ```

5. **Send Response**:  
   Include the computed `Sec-WebSocket-Accept` in the response header to validate the handshake:  
   ```
   Sec-WebSocket-Accept: 5TJpHv9RoAl7w8ytsXcWxTOZ9Q==
   ```  

### Purpose of `Sec-WebSocket-Accept`

`Sec-WebSocket-Accept` is used in the WebSocket handshake process to **validate the server's ability and willingness to establish a WebSocket connection**. Here's the fundamental reasoning behind it:

1. **Proof of Server Compliance**:  
   - The client sends a randomly generated `Sec-WebSocket-Key` during the handshake.  
   - The server computes `Sec-WebSocket-Accept` using the `Sec-WebSocket-Key` and a predefined "magic string."  
   - This process ensures that the server understands the WebSocket protocol and can perform the required cryptographic operations.

2. **Preventing Fake Handshakes**:  
   - By requiring the server to compute `Sec-WebSocket-Accept` based on the client-provided key, it ensures that only a genuine WebSocket-capable server can respond correctly.  
   - This avoids simple HTTP-based spoofing attempts.

3. **One-Time Validation**:  
   - The client knows the algorithm to compute `Sec-WebSocket-Accept`. After receiving the server's response, it verifies that the `Sec-WebSocket-Accept` matches the expected value.  
   - If the values don't match, the client terminates the connection, ensuring security and protocol integrity.

**In summary**, `Sec-WebSocket-Accept` acts as a cryptographic handshake token, proving that the server is compliant with the WebSocket protocol and enabling a trusted, bidirectional communication channel to be established.
