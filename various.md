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