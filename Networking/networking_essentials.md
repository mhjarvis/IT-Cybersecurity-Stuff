# Networking Essentials

## DHCP - Network Settings

In order to access a network, you need an IP address with a subnet mask, a router (or gateway), and a DNS server. The Dynamic Host Configuration Protocol (DHCP) is an application level protocol that relies on UDP, listens on UDP port 67, and sends from UDP port 68. It follows 4 steps:

1. `DHCP Discover` - the client broadcasts a DHCPDISCOVER message seeking the local DHCP server if one exists.
2. `DHCP Offer` - the server responds with a DHCPOFFER message with an IP address available for the client to accept.
3. `DHCP Request` - the client responds with a DHCPREQUEST message to indicate that it has accepted the offered IP.
4. `DHCP Acknowledge` - the server responds with a DHCPACK message to confirm that the offered IP address is now assigned to this client.

The client will send a DHCP Discover packet on 255.255.255.255 and will use the IP address 0.0.0.0 to receive the network configuration.

## ARP - Bridging Layer 3 to Layer 2

ARP makes it possible to find the MAC address of another device on the Ethernet.

## ICMP - Troubleshooting Networks

Internet Control Message Protocol (ICMP) is mainly used for network diagnostics and error reporting. Two commands relly on ICMP:

- `pint` - tests connectivity and rount-trip time (RTT).
- `traceroute` - uses ICMP to discover the route from your host to target (`tracert` on Windows).

## Routing

OSPF (Open Shortest Path First): OSPF is a routing protocol that allows routers to share information about the network topology and calculate the most efficient paths for data transmission. It does this by having routers exchange updates about the state of their connected links and networks. This way, each router has a complete map of the network and can determine the best routes to reach any destination.
EIGRP (Enhanced Interior Gateway Routing Protocol): EIGRP is a Cisco proprietary routing protocol that combines aspects of different routing algorithms. It allows routers to share information about the networks they can reach and the cost (like bandwidth or delay) associated with those routes. Routers then use this information to choose the most efficient paths for data transmission.
BGP (Border Gateway Protocol): BGP is the primary routing protocol used on the Internet. It allows different networks (like those of Internet Service Providers) to exchange routing information and establish paths for data to travel between these networks. BGP helps ensure data can be routed efficiently across the Internet, even when traversing multiple networks.
RIP (Routing Information Protocol): RIP is a simple routing protocol often used in small networks. Routers running RIP share information about the networks they can reach and the number of hops (routers) required to get there. As a result, each router builds a routing table based on this information, choosing the routes with the fewest hops to reach each destination.

## NAT
