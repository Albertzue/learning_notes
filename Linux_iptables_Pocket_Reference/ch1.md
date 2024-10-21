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
