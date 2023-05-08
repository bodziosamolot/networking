# TCP

- Transmission Control Protocol
- Layer 4
- Ability to address processes in host using ports
- Controls the transmission unlike UDP (UDP is a firehose)
- Has the concept of a connection
    - there is a session between the server and the client
    - this means there is state maintained
    - which means resources are required (memory)
    - requires a handshake
    - connection is layer 5
- Use cases:
    - reliable connection
    - database connections
    - chats
- TCP segment slides into an IP packet as Data field
- Segments are:
    - seqenced
    - ordered
    - acknowledged
    - lost segments are retransmitted

# Connection

- Connection is an agreement between client and server
- Must create a connection to send data
- Handshake is required if data is to be sent
- Connection is identified by:
    - source Ip & source Port
    - destination Id & destination Port
    - all of those values are:
        - taken by the operating system
        - hashed
        - stored in a lookup called a file descriptor
- When the system receives a data transmission if first checks if it has a file descriptor for the source of the data (ip address and port). If it has a file descriptor that means there is a connection and the data can be received.
- An application can send another segment before an ACK for the previous one is acknowledged. There is a limit to how many segments can be sent without acknowledgment.
- Connection can be closed by the client with a FIN message.
- When the client closes a connection, the file descriptor on their side is not removed. It switched to TIMED_WAIT state to be able to receive all retransmitted segments.

## TCP Socket

- A TCP (Transmission Control Protocol) socket is an endpoint for sending and receiving data through a reliable, connection-oriented, and stream-based communication channel between two network nodes.
- A TCP socket is an abstraction provided by the operating system that allows applications to communicate with each other using the TCP protocol.

# Maximum Segment Size

- Maximum Segment Size (MSS): The MSS is specific to the Transport Layer (Layer 4) of the OSI model and is a parameter of the TCP protocol. It defines the maximum amount of data that can be carried in a single TCP segment, excluding the TCP header. 
- The MSS is negotiated during the TCP connection setup through a process called the "three-way handshake.". Each side of the connection sends its own MSS value, and the lower of the two values is used as the MSS for the entire connection. 
- Maximum Transmission Unit (MTU): The MTU is related to the Network Layer (Layer 3) of the OSI model and is a property of the data link or network interface over which packets are transmitted. It defines the maximum size of a packet, including both the header and payload, that can be transmitted over the link without fragmentation. If a packet exceeds the MTU, it will be fragmented into smaller packets before being sent.
- while both MSS and MTU deal with the size of data packets, they operate at different layers of the networking stack. The MSS is specific to TCP and determines the maximum amount of payload data in a single TCP segment, while the MTU is related to the network interface and sets the maximum size of a packet that can be transmitted without fragmentation. 

# Flow Control

- How much data can the receiver handle.
- When the receiver gets the segments it can't process them immediately. They are placed in a buffer. If that buffer fills then the coming segments will be dropped.
- Segment's Window Size field allows to inform the sender how much data the receiver can handle.
- Both sender and receiver can put a value into the Windows Size because TCP is bidirectional. Receiver's window is refered to as RWND Receiver Window.
- Window scaling. The maximum window size that can be represented by the 16-bit field is 65,535 bytes (2^16 - 1). However, this limit can be too small for high-speed networks or networks with high latency, leading to inefficient use of the available bandwidth. The window scaling extension addresses this limitation by introducing a scale factor, which allows the effective window size to be much larger than 65,535 bytes.

# Congestion Control

- How much the network can handle. This means the network gear between the sender and receiver. A bit like flow control of the routers.
- Sender parameter: Congestion Window (CWND)
- There are two algorithms for congestion control

## Slow Start

- CWND increases by 1 with each acknowledgment
- Slow start is an essential part of the TCP (Transmission Control Protocol) congestion control mechanism that aims to prevent network congestion by gradually increasing the amount of data sent over a connection. It allows the sender to probe the network to determine the available capacity, ensuring that it does not send data too aggressively, which could lead to network congestion.

1. Initialize congestion window (cwnd): The sender sets the initial size of its congestion window to a small value, typically equal to the Maximum Segment Size (MSS) or a few times the MSS (e.g., 2 or 3 times MSS), as specified by the latest standards (RFC 5681 and RFC 6928).
2. Send data: The sender transmits data segments up to the size of the congestion window.
3. Acknowledgment (ACK) reception: For each ACK received from the receiver, the sender increases the size of the congestion window by one MSS. This effectively doubles the congestion window size each round-trip time (RTT), leading to an exponential growth in the amount of data sent. This process is also known as "window inflation."
4. Monitoring the congestion window size: The slow start phase continues until the congestion window size reaches a threshold called the "slow start threshold" (ssthresh) or until congestion is detected. The ssthresh is initially set to a large value, and its value is updated dynamically throughout the connection based on network conditions.
5. Transition to congestion avoidance: Once the congestion window size reaches the slow start threshold or if congestion is detected (e.g., through packet loss), the sender transitions to the congestion avoidance phase. In congestion avoidance, the sender increases the congestion window size more conservatively, using a linear growth algorithm, to avoid causing network congestion.

1. Initially, the sender sets the cwnd to 1 MSS. It sends one packet.
2. The receiver acknowledges the packet with an ACK. The sender increases the cwnd by 1 MSS. Now, the cwnd is 2 MSS. The sender sends two packets.
3. The receiver acknowledges both packets with two ACKs. For each ACK, the sender increases the cwnd by 1 MSS. Now, the cwnd is 4 MSS. The sender sends four packets.
4. The receiver acknowledges all four packets with four ACKs. For each ACK, the sender increases the cwnd by 1 MSS. Now, the cwnd is 8 MSS. The sender sends eight packets.

## Congestion avoidance

- Once the slow start phase has completed (i.e., the congestion window has reached the slow start threshold or congestion is detected), the congestion avoidance phase begins.

1. Additive Increase: For each round-trip time (RTT), the sender increases the congestion window size by a constant value, typically 1 MSS (Maximum Segment Size) per RTT. This leads to a linear increase in the congestion window size, allowing the sender to probe the network capacity gradually. This phase continues until congestion is detected (e.g., through packet loss).
2. Congestion Detection: When congestion is detected, it is assumed that the network has reached its capacity. TCP typically detects congestion by monitoring packet loss through mechanisms like duplicate ACKs or retransmission timeouts.
3. Multiplicative Decrease: Once congestion is detected, the sender reduces the congestion window size multiplicatively to alleviate network congestion. The congestion window is typically reduced to a fraction of its current size, often by setting it to half the current value. This step is designed to react quickly to network congestion and back off the sending rate.
4. Update slow start threshold (ssthresh): After reducing the congestion window size, the sender also updates the slow start threshold to the new reduced congestion window value. This ensures that if the slow start phase is re-entered, it will start with an updated threshold to adapt to the network conditions.
5. Resume congestion avoidance: The sender then resumes the congestion avoidance phase by increasing the congestion window size additively, as described in step 1.

- The difference here is that windows is increased by 1 MSS per round trip, not per ACK like for slow start.