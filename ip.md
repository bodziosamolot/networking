# IP Address

- layer 3
- packets: source ip address, destination ip address
- 4 bytes, 32 bits
- 2 parts:
    - network - used for eliminating networks
    - device
- 192.168.253.0/24
    - 2^24 networks
    - each network has 2^* (255) hosts - which are represented by the bytes left after 24 bytes for the network
    - the /24 is a subnet mask
- If a packet being sent is identified as being on the same subnet, then the MAC address is used for addressing. If the packet is being sent to a different network, it goes through the gateway and the ip address has to be used.
- Identitification if the packet is destined to the same subnet happens on the host sending the packet. It uses the network mask to check if destination address is on the same network. It sends the packet to the gateway and the gateway is on the same network so it can use the MAC address for it.
- Gateway has two network interfaces. One for every subnet it is in.
- Database should be in the same subnet as the host communicating with it. That's because of possible router congestion slowing the communication down.

## IP Packet

- MTU - Maximum Transmission Unit
- MTU forces packet fragmentation