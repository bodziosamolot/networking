# NAT

- 4,294,967,296 is the limit of possible IPv4 addresses
- How WAN sees internal devices
- Goal of NAT: one public IP address for the network gateway and all devices behind it have the same public ip address (of the gateway)
- Devices with private ip addresses are mapped to ports in the router's NAT table
- Allows for Layer 4 load balancing
    - HAProxy NAT Mode
- Allows port forwarding:
    - If someone sends a request to e.g. port 80, forward it to e.g. port 8080 on a certain machine