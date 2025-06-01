#Introduction

iptables operates at OSI Layer 3 (Network). For OSI Layer 2 (Link), there are other technologies such as ebtables (Ethernet Bridge Tables). 

#### An Example Command

Here is a sample iptables command:
```
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 80
  -j DNAT --to-destination 192.168.1.3:8080
```

![image](https://github.com/user-attachments/assets/65026412-ed83-4b97-ac68-55d1d120fb21)


#### Concepts
iptables defines five “hook points” in the kernel’s packet processing pathways: `PREROUTING`, `INPUT`, `FORWARD`, `POSTROUTING` and `OUTPUT`.
Built-in chains are attached to these hook points; you can add a sequence of rules for each hook point. Each rule represents an opportunity to affect or monitor packet flow.

![image](https://github.com/user-attachments/assets/167c62bd-4f8e-4678-884a-3e42938e5d14)


#### Tables
iptables comes with three built-in tables: `filter`, `mangle`, and `nat`. 
![image](https://github.com/user-attachments/assets/9a680fc1-72df-4444-acea-42460c309023)

**Tip
The default table is the filter table; if you do not specify an explicit table in an iptables command, filter is assumed.**

#### Chains
.Only the built-in targets (see Table 1-8) ACCEPT and DROP can be used as the policy for a built-in chain, and the default is ACCEPT. All user-defined chains have an implicit policy of RETURN that cannot be changed

#### Rules
An iptables rule consists of one or more match criteria that determine which network packets it affects (all match options must be satisfied for the rule to match a packet) and a target specification that determines how the network packets will be affected.

#### Targets
Targets are used to specify the action to take when a rule matches a packet and also to specify chain policies. Four targets are built into iptables, and extension modules provide others.
![image](https://github.com/user-attachments/assets/eca11c0a-3106-4ab2-98d1-bd971d1e1b8a)

# Configuring iptables
#### Persistent rules
On recent Red Hat systems, you can find the iptables rules stored in /etc/sysconfig/iptables.
#### Other configuration files
The kernel’s general networking and iptables behavior can be monitored and controlled by a number of pseudofiles in the /proc filesystem.

![image](https://github.com/user-attachments/assets/7f1c5338-df6f-4d49-be7b-5b8ee215e934)


# Network Address Translation (NAT)
NAT is the modification of the addresses and/or ports of network packets as they pass through a computer. The computer performing NAT on the packets could be the source or destination of the packets, or it could be one of the computers on the route between the source and destination.

The nat built-in table is intended specifically for use in NAT applications.

## Source NAT and Masquerading
Source NAT (SNAT) is used to share a single Internet connection among computers on a network. The computer attached to the Internet acts as a gateway and uses SNAT (along with connection tracking) to rewrite packets for connections between the Internet and the internal network. The source address of outbound packets is replaced with the static IP address of the gateway’s Internet connection. When outside computers respond, they will set the destination address to the IP address of the gateway’s Internet connection, and the gateway will intercept those packets, change their destination addresses to the correct inside computer, and forward them to the internal network.

Since SNAT entails modifying the source addresses and/or ports of packets just before they leave the kernel, it is performed through the POSTROUTING chain of the nat table.

You can set up SNAT on the eth1 interface by putting a simple rule on the POSTROUTING chain of the nat table:
```
iptables -t nat -A POSTROUTING -o eth1 -j SNAT
```

The corresponding command for masquerading is:
```
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
```

## Destination NAT
Since DNAT entails modifying the destination addresses and/or ports of packets just before they are either routed to local processes or forwarded to other computers, it is performed through the PREROUTING chain of the nat table.

For example, to forward inbound connections coming in on a gateway’s port 80 (HTTP) to an internal web server running on port 8080 of 192.168.1.3, you could use a rule like this:
```
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 80
  -j DNAT --to-destination 192.168.1.3:8080
```

## Transparent Proxying

If you have an HTTP proxy (such as Squid) configured to run as a transparent proxy on your firewall computer and listen on port 8888, you can add one rule to redirect outbound HTTP traffic to the HTTP proxy:
```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80
  -j REDIRECT --to-port 8888
```
