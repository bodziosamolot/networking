*tcpdump -i en0*

-i interface - Use *ifconfig -l* to list all network interfaces. Network devices with assigned IP addresses are the ones being used:

    en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=6463<RXCSUM,TXCSUM,TSO4,TSO6,CHANNEL_IO,PARTIAL_CSUM,ZEROINVERT_CSUM>
	ether bc:d0:74:5f:7c:82
	inet6 fe80::10a7:5b19:551b:fc7%en0 prefixlen 64 secured scopeid 0xf
	inet 192.168.1.105 netmask 0xffffff00 broadcast 192.168.1.255
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect
	status: active

*tcpdump -i en0 arp*

- see all arp announcements on interface *en0*


*tcpdump -i en0 arp*

- same as above but without hostnames, only IP addresses


*tcpdump -i en0 src [put source ip address here] or dst [destination ip address]*

- filters traffic by source ip address, comming from the specified ip address or destination address