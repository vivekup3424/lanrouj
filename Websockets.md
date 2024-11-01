Before the RFC 6455 (proposal of websockets), in RFC 6202 *long polling and streaming is used for bidirectional http*
1. HTTP is often used for asynchronous client-server communication, and often abused for server to client communication using a thing called "server push"
## Below are ways we abuse http for birectional communication (before the advent of websockets)
1. HTTP Polling
	1. For getting some new message from server i.e. any sort of update (server push) we can poll the server at regular intervals
	2. the client repeatedly sends HTTP requests at regular intervals to check if the server has new information
	3. This is considered an abuse because it creates unnecessary load on the server, because it forces the server to process new requests even though there may not be any new information on the server for the client.
	4. This can lead to higher bandwidth usage and resource consumption.
2. Long Polling
	1. It aims to minimise the latency in server-client delivery, by only creating a new connection if there are any new information that the server needs to send to the client.
	3. The basic life cycle of an application using HTTP long polling is as follows
		1. The client makes an initial request and then waits for a response.
	    2. The server defers its response until an update is available or until a particular status or timeout has occurred.
	    3. When an update is available, the server sends a complete response to the client, and the server closes the connection
	    4. The client typically sends a new long poll request, either immediately upon receiving a response or after a pause to allow an acceptable latency period.
3. HTTP Streaming
	1. **What it is**: Here, the server keeps an HTTP connection open indefinitely, continuously sending data to the client as events occur.
	2. **Why it's considered abuse**: HTTP was not designed to handle prolonged open connections like this, which can strain server resources. Streaming works but often leads to issues like connection timeouts and load balancer complications, as traditional HTTP infrastructures may struggle to manage long-lived connections.

## Some points observer from Hussein Nassar's video for 
