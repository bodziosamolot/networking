# MSS vs MTU vs PMTUD

- MTU
    - Maximum Transmission Unit.
    - IP
    - Layer 3
    - largest size of a data packet or frame that can be sent over a network link in a single transmission. MTU is measured in bytes and includes the size of the payload data as well as the headers 
    - default is 1500
    - The value of MTU is usually equal to hardware MTU
- MSS
    - Maximum Segment Size
    - TCP
    - Layer 4
    - largest amount of data, in bytes, that a device can receive in a single TCP segment
    - TO fit date into a single segment 
        - max amount of data that ca be sent to fit in one segment = MTU - IP Headers - TCP Headers
- PMTUD
    - Path MTU Discovery
    - Client sends a packet with a DF flag (Don't Fragment). If a part of the network path can't handle this size, an ICMP message is returned that fragmentation is required. MTU is lowered and tried again.

# Nagle's aglorithm

- Used on the client-side.

1. If the sender has a new packet to send and there is no unacknowledged data already in transit, the new packet is sent immediately.
2. If the sender has a new packet to send and there is unacknowledged data in transit, the sender waits until either:
    a. An acknowledgment is received for the outstanding data, at which point the new packet is sent, or
    b. A maximum waiting time (typically 200 ms) has passed, at which point the new packet is sent regardless.
3. If the sender receives an acknowledgment for previously sent data and still has data in its buffer waiting to be sent, the sender can combine this buffered data with any new data and send it as a single packet.

- The algorithm is enabled by default in many operating systems and networking devices, as it helps to prevent network congestion and improve overall performance.
- Nagle's algorithm is still in use and can provide benefits in many situations, its relevance and necessity may vary depending on the specific network conditions and application requirements.

# Delayed Acknowledgment algorithm

- Used on the server side
- It's waistfull to acknowledge right away
- Waits a little and acknowledges a set of segments
- May lead to retransmission
- Combined with Nagle's algorithm can lead to up to 400ms of delay

# Head of the line blocking

Head-of-line (HOL) blocking can occur in both the HTTP and TCP layers. Let's break down a step-by-step example of how HOL blocking can happen in each layer.

HTTP Layer:
Step 1: A client, such as a web browser, sends multiple HTTP requests to a web server to load different resources like images, scripts, or stylesheets.

Step 2: The web server processes the requests and starts sending responses back to the client. Due to various factors like server load or response size, some responses may take longer to process than others.

Step 3: The client receives and processes the responses in the order they were requested. If a large or slow-loading response is blocking the queue, the client will wait for that response to be fully received before processing the subsequent responses, even if they are already available.

Step 4: The result is that the entire page loading process is delayed, leading to a poor user experience.

TCP Layer:
Step 1: An application sends data to be transmitted over the network. The data is divided into smaller chunks called segments by the TCP layer.

Step 2: The TCP segments are encapsulated in IP packets and sent over the network through routers and switches.

Step 3: At a switch or router, the packets are placed into an output queue for transmission to the next hop.

Step 4: If a packet at the head of the queue experiences an issue (e.g., link congestion, an error in transmission, or the destination is temporarily unreachable), it will block the packets behind it from being transmitted, even if their intended destinations are different and available.

Step 5: The blocked packets experience increased latency and potential timeout, which can lead to poor application performance and degraded user experience.

# TCP Fast Open (TFO)

TCP Fast Open (TFO) is an optimization of the [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) protocol, designed to reduce latency in establishing a connection. It achieves this by sending data within the initial SYN packet, allowing the client and server to exchange data sooner.

## How TFO Works

1. **TFO Cookie Request**: On the first connection, the client sends a SYN packet with a TFO option requesting a cookie from the server.
2. **TFO Cookie Response**: The server generates a cookie and sends it back to the client in the SYN-ACK packet.
3. **Subsequent Connections**: In future connections, the client includes the cookie in the initial SYN packet along with data. The server validates the cookie and processes the data immediately.

## Benefits

- Reduces latency by sending data in the initial SYN packet
- Improves performance for short-lived connections and time-sensitive applications

## Limitations

- Not supported by all servers and clients
- Security concerns due to potential amplification attacks

