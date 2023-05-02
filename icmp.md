# ICMP

- internet control message protocol
- layer 3
- designed for informational messages
- uses IP
- packets: source ip address, destination ip address
- used by:
    - ping
    - traceroute
- some firewalls block ICMP
- TTL is a mechanism to prevent packets from endlessly circulating in a network. It represents the maximum number of hops (router or network nodes) that a packet can traverse before being discarded or returned to the sender. Each time a packet passes through a router or a network node, the TTL value is decremented by 1. When the TTL value reaches 0, the packet is discarded, and an ICMP Time Exceeded message is sent back to the sender.
- Ping sends ICMP Echo Request messages with a specific TTL value