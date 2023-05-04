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

- IP packet must fit into a single frame
    - MAC addresses operate at the data link layer (Layer 2) of the OSI model, while IP addresses operate at the network layer (Layer 3)
- MTU - Maximum Transmission Unit
    - MTU is most commonly associated with the network layer (Layer 3), where it refers to the maximum size of a packet, including the payload and the network layer headers (e.g., IP header).
    - MTU forces packet fragmentation
    - If a packet exceeds the MTU, it must be fragmented into smaller packets before being transmitted over the network. This fragmentation can occur at the network layer, with each smaller packet then encapsulated into a frame for transmission. Fragmentation can also happen at the data link layer, depending on the specific network technology being used.
- TTL - counter, decremented with each hop
- Protocol - header indicating the protocol of the data being transmitted with this IP packet
- ECN - explicit congestion notification
- congestion 
    - packets are being dropped
    - routers have memory, if this memory fills up, packets will be dropped
    - when router memory is about to fill it will start setting the ECN so the receiver sees there is the danger of congestion
    - the client will respond to the server with ECN bit set so client and server know about congestion

## ARP

- Address Resolution Protocol
- When we know the IP Address and don't know the MAC address.
- ARP table is a cached mapping of IP address to MAC address
- ARP operates at the network layer (Layer 3) and the data link layer (Layer 2) of the OSI model, facilitating communication between devices on a local network.
- There is an attack called "ARP Poisoning" where someone says they have the MAC address asked for.

### Example

1. **Device A wants to send data to Device B**:
   - Device A knows Device B's IP address, but not its MAC address.

2. **Device A broadcasts an ARP request**:
   - The request contains:
     - Device A's IP and MAC addresses.
     - Device B's IP address.
   - The request asks for the MAC address associated with Device B's IP address.

3. **All devices on the network receive the ARP request**:
   - Only Device B, whose IP address matches the requested IP, responds to the ARP request.

4. **Device B sends an ARP reply to Device A**:
   - The reply contains Device B's MAC address.

5. **Device A updates its ARP cache**:
   - Device A stores the new IP-to-MAC mapping in its temporary ARP cache.
   - This cache reduces the need for frequent ARP requests if the devices communicate frequently.

6. **Device A sends data to Device B**:
   - Device A creates a frame containing the data.
   - The frame is addressed using Device B's MAC address.
   - The frame is transmitted over the network.

# Private IP Addresses

- Private IP addresses are a range of IP addresses reserved for use within private networks, such as home, office, or enterprise networks.
- Private IP addresses help conserve the limited IPv4 address space and provide an additional layer of security by keeping internal network devices hidden from the public Internet.
- when a private ip address is detected on the public internet, the packets are dropped
- There are three reserved IP address ranges for private networks, as specified by RFC 1918:
   - 10.0.0.0 to 10.255.255.255 (10.0.0.0/8)
   - 172.16.0.0 to 172.31.255.255 (172.16.0.0/12)
   - 192.168.0.0 to 192.168.255.255 (192.168.0.0/16)
