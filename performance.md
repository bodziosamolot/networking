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