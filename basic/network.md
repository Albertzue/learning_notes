# Network bridge
A network bridge is a computer networking device that creates a single, aggregate network from multiple communication networks or network segments.Bridging is distinct from routing. Routing allows multiple networks to communicate independently and yet remain separate, whereas bridging connects two separate networks as if they were a single network.

# DNAT 
DNAT(Destination Network Address Translation). DNAT refers to the technique of translating the Destination IP address of a packet, or to change it simply put. This is used together with SNAT to allow several hosts to share a single Internet routable IP address, and to still provide Server Services. This is normally done by assigning different ports with an Internet routable IP address, and then tell the Linux router where to send the traffic.

# SNAT
SNAT - Source Network Address Translation. This refers to the techniques used to translate one source address to another in a packet. This is used to make it possible for several hosts to share a single Internet routable IP address, since there is currently a shortage of available IP addresses in IPv4 (IPv6 will solve this).

# ICMP
ICMP messages are used for a basic kind of error reporting between host to host, or host to gateway. Between gateway to gateway, a protocol called Gateway to Gateway protocol (GGP) should normally be used for error reporting. As we have already discussed, the IP protocol is not designed for perfect error handling, but ICMP messages solves some parts of these problems.

# TCP/IP destination driven routing
TCP/IP has grown in complexity quite a lot when it comes to the routing part. In the beginning, most people thought it would be enough with destination driven routing. The last few years, this has become more and more complex however. Today, Linux can route on basically every single field or bit in the IP header, and even based on TCP, UDP or ICMP headers as well. This is called policy based routing, or advanced routing.

This is simply a brief discussion on how the destination driven routing is performed. When we send a packet from a sending host, the packet is created. After this, the computer looks at the packet destination address and compares it to the routing table that it has. If the destination address is local, the packet is sent directly to that address via its hardware MAC address. If the packet is on the other side of a gateway, the packet is sent to the MAC address of the gateway. The gateway will then look at the IP headers and see the destination address of the packet. The destination address is looked up in the routing table again, and the packet is sent to the next gateway, et cetera, until the packet finally reaches the local network of the destination.

As you can see, this routing is very basic and simple. With the advanced routing and policy based routing, this gets quite a bit more complex. We can route packets differently based on their source address for example, or their TOS value, et cetera.

# What is an IP filter
An IP filter operates mainly in layer 2, of the TCP/IP reference stack. Iptables however has the ability to also work in layer 3, which actually most IP filters of today have. But per definition an IP filter works in the second layer.

If the IP filter implementation is strictly following the definition, it would in other words only be able to filter packets based on their IP headers (Source and Destionation address, TOS/DSCP/ECN, TTL, Protocol, etcetera. Things that are actually in the IP header. However, since the Iptables implementation is not perfectly strict around this definition, it is also able to filter packets based on other headers that lie deeper into the packet (TCP, UDP, etc), and shallower (MAC source address).
