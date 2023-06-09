# Switch

- connects devices within a single network
- operates at the data link layer (Layer 2) of the OSI model, using MAC addresses to forward data frames to the appropriate devices.
- forward data frames based on the destination MAC address. They maintain a MAC address table that maps each connected device's MAC address to the corresponding physical port, enabling efficient data frame forwarding within the local network
- typically do not perform NAT, as their main function is to facilitate communication within the local network
- Switches generally do not have built-in DHCP functionality, although some managed switches may support DHCP relay or snooping features
- A switch does not broadcast a request to all connected devices when it receives a frame destined for a specific device. Instead, a switch uses its MAC address table to determine the appropriate port to forward the frame based on the destination MAC address. However, if the switch does not have an entry for the destination MAC address in its table, it will "flood" the frame, sending it to all connected devices, except the one on the incoming port. This is called "unknown unicast flooding." When the destination device responds, the switch learns its MAC address and updates its MAC address table for future reference.

# Router

- connects multiple networks together and routes data packets between them
- operates at the network layer (Layer 3) of the OSI model, using IP addresses to determine the best path for data transmission.
- typically perform Network Address Translation (NAT), allowing multiple devices within a private network to share a single public IP address for accessing the Internet
- Many routers include built-in DHCP servers, which automatically assign IP addresses to devices on the network

# Hub

- hub is dumb, it replicates the electric signal to everyone connected to it