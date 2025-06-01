a firewall—a type of router that restricts the types of traffic it forwards

With NAT, Internet addresses need not be globally unique, and as a consequence they can be reused in different parts of the Internet, called address realms. Allowing the same addresses to be reused in multiple realms greatly eased the problem of address exhaustion.

# Firewalls
The two major types of firewalls commonly used include `proxy firewalls` and` packet-filtering firewalls`.

The packet-filtering firewall is an Internet router that drops datagrams that (fail to) meet specific criteria. The proxy firewall operates as a multihomed server host from the viewpoint of an Internet client. That is, it is the endpoint of TCP and UDP transport associations; it does not typically route IP datagrams at the IP protocol layer.

###  Packet-Filtering Firewalls
A typical packet-filtering firewall is shown in Figure 7-1.
Here, the firewall is an Internet router with three network interfaces: an “inside,” an “outside,” and a third “DMZ” interface. 
The DMZ subnet provides access to an extranet or DMZ where servers are deployed for Internet users to access. 
Network administrators install filters or access control lists (ACLs, basically policy lists indicating what types of packets to discard or forward) in the firewall. 
Typically, these filters conservatively block traffic from the outside that may be harmful and liberally allow traffic to travel from inside to outside.
![image](https://github.com/user-attachments/assets/7975000a-811b-486d-9186-51a16dfc2ec5)


### Proxy Firewalls
Figure 7-2 illustrates a proxy firewall. For this type of firewall,
clients on the inside of the firewall are usually configured in a special way to associate (or connect) with the proxy instead of the actual end host providing the desired service. 
(Applications capable of operating with proxy firewalls this way include configuration options for it.) 
These firewalls act as multihomed hosts, and their IP forwarding capability, if present, is typically disabled. As with packet-filtering firewalls, 
a common configuration is to have an “outside” interface assigned a globally routable IP address and for its “inner” interface to be configured with a private IP address.
Thus, proxy firewalls support the use of private address realms.

![image](https://github.com/user-attachments/assets/8f46c400-6d62-4317-adc3-95996e4afa1a)

# Network Address Translation (NAT)
NAT is essentially a mechanism for allowing the same sets of IP addresses to be reused in different parts of the Internet. 
The primary motivation for the creation of NAT was the limited and diminishing availability of IP address space. 

Despite its popularity, NAT has several drawbacks. 
The most obvious is that offering Internet-accessible services from the private side of a NAT requires special configuration because privately addressed systems are not directly reachable from the Internet. 
n addition, for a NAT to work properly, every packet in both directions of a connection or association must pass through the same NAT. 
This is because the NAT must actively rewrite the addressing information in each packet in order for communication between a privately addressed system and a conventionally addressed Internet host to work. In many ways, NATs run counter to a fundamental tenet of the Internet protocols: the “smart edge” and “dumb middle.” To do their job, NATs require connection state on a per-association (or per-connection) basis and must operate across multiple protocol layers, unlike conventional routers. 
Modifying an address at the IP layer also requires modifying checksums at the transport layer 

![image](https://github.com/user-attachments/assets/7616b4a3-8413-4b18-9b68-42d86d97eb73)

### Traditional NAT: Basic NAT and NAPT
The precise behavior of a NAT remained unspecified for many years. Nonetheless, a taxonomy of NAT types has emerged,
based largely on observing how different implementations of the NAT idea behave. 
The so-called traditional NAT includes both basic NAT and Network Address Port Translation (NAPT) 

Basic NAT performs rewriting of IP addresses only. In essence, a private address is rewritten to be a public address,
often from a pool or range of public addresses supplied by an ISP. 
This type of NAT is not the most popular because it does not help to dramatically reduce the need for IP addresses—the number of globally routable addresses must equal or exceed the number of internal hosts that wish to access the Internet simultaneously.
A much more popular approach, NAPT involves using the transport-layer identifiers (i.e., ports for TCP and UDP, query identifiers for ICMP) to differentiate which host on the private side of the NAT is associated with a particular packet (see Figure 7-4).
This allows a large number of internal hosts (i.e., multiple thousands) to access the Internet simultaneously using a limited number of public addresses, 
often only a single one.

![image](https://github.com/user-attachments/assets/b4df84e6-2345-4af0-8c8f-51923aad22d6)

We shall ordinarily use the term NAT to include both traditional NAT and NAPT unless the distinction is important in a particular context.

###  Address and Port Translation Behavior
Some NATs implement a special feature called port parity. Such NATs attempt to preserve the “parity” (evenness or oddness) of port numbers. Thus, if x is even, x1´ is even and vice versa.Although not as strong as port preservation, such behavior is sometimes useful for specific application protocols that use special port numberings

###  Hairpinning and NAT Loopback
An interesting issue arises when a client wishes to reach a server and both reside on the same, private side of the same NAT. NATs that support this scenario implement so-called hairpinning or NAT loopback
![image](https://github.com/user-attachments/assets/c95ec62e-8e51-4bf6-ad9b-fb80b1d3cc70)
