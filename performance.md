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