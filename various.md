# Interfaces

- A machine has multiple network interfaces. Each one of them has it's own IP address.
- 0.0.0.0:8080 - listen on all interfaces, on port 8080
- ::1 - ipv6 version of 127.0.0.1

# Host to host communication

- Happens in Layer 2 (sometimes layer 3)
- Each host has a network card with a unique Media Access Control (MAC) address
- Message is sent to everyone on the network
- Everyone else than the recepient will drop the message (in layer 2)
- In order not to send it to everyone routability is required, the IP address is required
- If only MAC addresses were used we would need to scan all MAC addresses in the world

# NAT

- networking technique that allows multiple devices within a private network to share a single public IP address when accessing the Internet.
- NAT works by translating the private IP addresses of the devices within the network to a public IP address, and vice versa, when communicating with the Internet.
- A more specific form of dynamic NAT is Port Address Translation (PAT), also known as NAT Overloading or IP Masquerading. PAT maps multiple private IP addresses to a single public IP address by using different port numbers for each connection

# DHCP

- is a network protocol that automates the process of assigning IP addresses and other network configuration parameters to devices on a network
- When a device connects to a network, it sends a DHCP discovery message, requesting an IP address and other network configuration information. The DHCP server, upon receiving the discovery message, responds with a DHCP offer, which includes an available IP address and other network parameters. The device then sends a DHCP request, accepting the offered IP address and configuration. Finally, the DHCP server sends a DHCP acknowledgment, confirming the assignment of the IP address and configuration to the device.
- e.g. device learns the address of the gateway through DHCP

# Kestrel VS ASP.NET

**Kestrel:**
- Listens for incoming HTTP and HTTPS requests.
- Manages secure connections using TLS/SSL.
- Handles low-level network communication, such as parsing HTTP requests and formatting HTTP responses.
- Passes incoming requests to the appropriate middleware or application components in the ASP.NET Core pipeline.

Kestrel is involved in the decryption process as part of the secure connection management. To clarify, Kestrel operates primarily at the Application layer (Layer 7) of the OSI model, but when handling HTTPS, it also deals with encryption and decryption at the Transport layer (Layer 4), as it leverages the TLS/SSL protocol for secure communication.

**ASP.NET Core:**
- Provides a framework for building web applications, including tools, libraries, and components for routing, authentication, authorization, and more.
- Processes application logic, such as handling requests, executing business rules, and generating responses.
- Consists of a middleware pipeline that processes requests and responses in a modular, customizable manner.

In a typical ASP.NET Core application, Kestrel receives an incoming HTTP request, processes it, and then passes it to the ASP.NET Core middleware pipeline. The middleware processes the request, executes application logic, and eventually generates an HTTP response. This response is then sent back through the middleware pipeline, and Kestrel takes care of sending the response to the client.

The boundary between Kestrel and ASP.NET Core is maintained by having Kestrel delegate request processing to the middleware pipeline, allowing developers to focus on building application logic while Kestrel manages low-level networking tasks and secure communication.

## How is a request passed from Kestrel to Asp.Net middleware pipeline

1. The client establishes a secure connection with Kestrel using the TLS/SSL protocol. During this process, the client and server exchange cryptographic keys, agree on cipher suites, and create an encrypted communication channel.
2. Once the secure connection is established, the client sends an encrypted HTTP request to the server. This request is transmitted as a series of data packets, which are then assembled into a complete request by the server's network stack.
3. Kestrel receives the encrypted request, decrypts it using the negotiated TLS/SSL encryption parameters, and parses it into an `HttpRequest` object.
4. Kestrel passes the `HttpRequest` object to the ASP.NET Core middleware pipeline, where it's processed by various middleware components and the application logic.
5. After processing the request, the middleware pipeline generates an `HttpResponse` object. Kestrel then takes this response, serializes it into an HTTP response format, encrypts it using the TLS/SSL encryption parameters, and sends it back to the client.

Before reaching Kestrel, the data goes through several OSI model layers:

1. At the Transport layer (Layer 4), the data is received as TCP segments.
2. At the Network layer (Layer 3), these segments are transmitted within IP packets.
3. At the Data Link layer (Layer 2) and Physical layer (Layer 1), the IP packets are further encapsulated and transmitted as frames over the network medium.

The lower layers of the OSI model (Layers 1-4) are handled by the operating system's network stack, which takes care of assembling and disassembling the various components like frames, IP packets, and TCP segments.