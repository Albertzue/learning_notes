### backlog
1. practice chapter 6 key topics  done
2. practice chapter 10 key topics
3. practice chapter 18 key topics
### Info
https://www.certskills.com/ccna2024-07/
### schedule(plan/finish)
2025/10/28 100/100

2025/10/29 130/120

2025/10/31  150/146

2025/11/01  167/168

2025/11/02  188/191

2025/11/03  214/217

2025/11/04  243/248

2025/11/07  278/280

2025/11/08  312/302

2025/11/09  312/312

2025/11/10  356/330  356-381(chapter 11)  1074-1087 (appendix M)

2025/11/11  395/416

2025/11/14 464

2025/11/17  complete chapter 10  and 482 /510

2025/11/18  543/544

2025/11/21 568

2025/11/22  597

2025/11/24 620

2025/11/24 640

2025/11/26 694

2025/11/27 724

2025/11/28 761

2025/12/08 780

2025/12/10  finished

2025/12/11  practice exam chapter 1,2,3,4,5,6,11,12

2025/12/12  recall chapter 6 done  

2025/12/13 recall chapter 7 done   practice exam chapter 7

### keynotes

#### Chapter 1
1. To make all that work, the network hardware in your computer—an integrated network interface card (NIC)— implements some physical layer standards to support physical communications. That NIC also supports the related data-link standards. The OS on the computer implements protocols from the network and transport layers. Finally, that web browser implements some application layer protocols (for instance, HTTP or HTTPS.)

--- 
2. <img width="554" height="161" alt="image" src="https://github.com/user-attachments/assets/4ebbfa97-f503-444b-bd4c-0714ae210016" />

#### Chapter 2 
1. The term **Ethernet** refers to a family of LAN standards that together define the physical and data-link layers of the world’s most popular wired LAN technology
2. Devices using **unshielded twisted-pair (UTP)** cabling transmit data over electrical circuits via the copper
wires inside the cable.
3. The IEEE also uses more meaningful shortcut names that identify the speed, as well as a clue about whether
the cabling is UTP (with a suffix that includes T) or fiber (with a suffix that includes X).
<img width="1084" height="358" alt="image" src="https://github.com/user-attachments/assets/33912c8b-6919-4254-a127-fd23356e6f03" />
---
4. what is an Ethernet LAN? It is a combination of user devices, LAN switches, and different kinds of cabling. Each link can use different types of cables, at different speeds. However, they all work together to deliver Ethernet frames from the one device on the LAN to some other device.
5. <img width="997" height="318" alt="image" src="https://github.com/user-attachments/assets/954011ab-5c61-4bc2-97ae-062a1fbc38e7" />
---
6. When electrical current passes over any wire, it creates electromagnetic interference (EMI) that interferes with the electrical signals in nearby wires, including the wires in the same cable. (EMI between wire pairs in the same cable is called crosstalk.) Twisting the wire pairs together helps cancel out most of the EMI, so most networking physical links that use copper wires use twisted pairs.
7. Each wire has a color-coded plastic coating, with the wires in a pair having a color scheme. For example, for the blue wire pair, one wire’s coating is all blue, while the other wire’s coating is blue-and-white striped.
8. Many Ethernet UTP cables use an RJ-45 connector on both ends. The RJ-45 connector has eight physical locations into which the eight wires in the cable can be inserted, called pin positions, or simply pins. These pins create a place where the ends of the copper wires can touch the electronics inside the nodes at the end of the physical link so that electricity can flow.
<img width="216" height="197" alt="image" src="https://github.com/user-attachments/assets/d83fca76-ef94-4965-9152-5182355954c4" />
<img width="310" height="133" alt="image" src="https://github.com/user-attachments/assets/b62f8fe7-ba71-40f7-bd28-4f2fab54e629" />
<img width="855" height="547" alt="image" src="https://github.com/user-attachments/assets/8ce7e550-bf21-46f6-907b-b14402df7ce0" />
<img width="758" height="396" alt="image" src="https://github.com/user-attachments/assets/506474a2-6e9b-4df0-9426-bf551721bb45" />
<img width="753" height="285" alt="image" src="https://github.com/user-attachments/assets/9d671b0a-41c9-41b2-9bd5-7afab8c16232" />
<img width="750" height="250" alt="image" src="https://github.com/user-attachments/assets/cafa8cb3-30a4-49e4-bb79-7ba9ea61c5f8" />

9. For the exam, you should be well prepared to choose which type of cable (straight-through or crossover) is needed in each part of the network. The key is to know whether a device acts like a PC NIC, transmitting at pins 1 and 2, or like a switch, transmitting at pins 3 and 6. Then, just apply the following logic:
        Crossover cable: If the endpoints transmit on the same pin pair
        Straight-through cable: If the endpoints transmit on different pin pairs

<img width="821" height="251" alt="image" src="https://github.com/user-attachments/assets/10d6d7d8-6ac1-4f62-930d-84fad8654e1a" />

---
10. if the link needs a crossover cable, but the installer connected a straight-through cable, this feature can sense the incorrect pinout, and then redirect the electrical signals to the correct pairs to compensate so
that the link works. The Ethernet standard calls this feature automatic medium-dependent interface crossover **(auto-MDIX)**
11. To transmit between two devices, you need two cables, one for each direction, as shown in Figure 2-17. The concept works much like having two electrical circuits with the original UTP Ethernet standards. 
<img width="662" height="152" alt="image" src="https://github.com/user-attachments/assets/5b47968c-1ef8-4eb6-a875-f47fe1bfbab0" />

12. <img width="666" height="134" alt="image" src="https://github.com/user-attachments/assets/339086ae-de2b-40a8-ab43-ab55621a593a" />
<img width="811" height="231" alt="image" src="https://github.com/user-attachments/assets/0ab6abd5-80e4-42ea-9328-a540b63968d1" />
<img width="806" height="246" alt="image" src="https://github.com/user-attachments/assets/0a542445-e834-4668-9945-a12917f9871f" />

13. **Ethernet addresses**, also called Media Access Control (MAC) addresses, are 6-bytelong (48-bit-long) binary numbers. For convenience, most computers list MAC addresses
as 12-digit hexadecimal numbers. Cisco devices typically add some periods to the number for easier readability as well; for example, a Cisco switch might list a MAC address as  0000.0C12.3456.
<img width="627" height="242" alt="image" src="https://github.com/user-attachments/assets/6506a6f1-b1c2-4cb4-9496-6e3304c77711" />

14. **Broadcast address**: Frames sent to this address should be delivered to all devices on the Ethernet LAN. It has a value of FFFF.FFFF.FFFF. \
    **Multicast addresses**: Frames sent to a multicast Ethernet address will be copied and forwarded to a subset of the devices on the LAN that volunteers to receive frames sent to a specific multicast address.

15. The Ethernet **Frame Check Sequence (FCS)** field in the Ethernet trailer—the only field in the Ethernet trailer—gives the receiving node a way to compare results with the sender, to discover whether errors occurred in the frame.

16. 
   **Half duplex**: The device must wait to send if it is currently receiving a frame; in other words, it cannot send and receive at the same time.
    
   **Full duplex**: The device does not have to wait before sending; it can send and receive at the same time.

17. <img width="794" height="429" alt="image" src="https://github.com/user-attachments/assets/13a5b9f9-bdae-42c7-a4d9-4cecdfbf067a" />

#### chapter 3
1. WAN technologies define the physical (Layer 1) standards and data-link (Layer 2) protocols used to communicate over long distances.
2. <img width="790" height="160" alt="image" src="https://github.com/user-attachments/assets/0d3cef41-b96b-4406-8162-a8e243f7154f" />

3. The **leased line** service, a physical layer service, delivers bits in both directions, at a predetermined speed, using full-duplex logic. In fact, conceptually it acts as if you had a fullduplex crossover Ethernet link between two routers, as shown in Figure 3-2. The leased line uses two pairs of wires, one pair for each direction of sending data, which allows full-duplex operation.
<img width="784" height="221" alt="image" src="https://github.com/user-attachments/assets/7aa5d456-fdbc-4f62-adb1-83728e2ca6fb" />
4. <img width="856" height="523" alt="image" src="https://github.com/user-attachments/assets/e053c788-bc08-47f7-985d-b03ad9804bad" />
5.<img width="838" height="547" alt="image" src="https://github.com/user-attachments/assets/334931bc-9281-4c6f-b84f-ede32db5467a" />
6. <img width="993" height="213" alt="image" src="https://github.com/user-attachments/assets/098e265e-056e-4ae5-8f5f-a3207d7b9835" />


7. The default router is also referred to as the default gateway.
8. Two IP addresses, not separated from each other by a router, must be in the same group (subnet).Two IP addresses, separated from each other by at least one router, must be in different groups (subnets).
9. <img width="905" height="329" alt="image" src="https://github.com/user-attachments/assets/2e3034ea-6cd1-45a4-b889-4fac610d2517" />

10. TCP/IP defines the Address Resolution Protocol (ARP) as the method by which any host or router on a LAN can dynamically learn the MAC address of another IP host or router on the same LAN. ARP defines a protocol that includes the ARP Request, which is a message that makes the simple request “if this is your IP address, please reply with your MAC address.” ARP also defines the ARP Reply message, which indeed lists both the original IP address and the matching MAC address.

11. You can see the contents of the ARP cache on most PC operating systems by using the arp -a command from a command prompt.
12. **Ping** uses the Internet Control Message Protocol (ICMP), sending a message called an ICMP echo request to another IP address. The computer with that IP address should reply with an ICMP echo reply. If that works, you successfully have tested the IP network. In other words, you know that the network can deliver a packet from one host to the other and back. ICMP does not rely on any application, so it really just tests basic IP connectivity—Layers 1, 2, and 3 of the OSI model.
<img width="788" height="315" alt="image" src="https://github.com/user-attachments/assets/dc43fc08-21f1-438f-8c44-bc3cf2c65fbc" />

#### chapter 4
1. User EXEC mode, sometimes also called user mode, allows the user to look around but not break anything. The “EXEC mode” part of the name refers to the fact that in this mode, when you enter a command, the switch executes the command and then displays messages that describe the command’s results.
2. Cisco IOS supports a more powerful EXEC mode called privileged mode (also known as enable mode). The formal name, privileged mode, refers to the fact that IOS allows powerful (or privileged) commands from that mode.
<img width="974" height="583" alt="image" src="https://github.com/user-attachments/assets/eccdee38-f131-4180-90a4-60c3cbf4c1fd" />

3.  by default, a switch allows console access only. By default, the console requires no password at all, and no password to reach enable mode for users that happened to connect from the console.
4.  <img width="991" height="401" alt="image" src="https://github.com/user-attachments/assets/3f2ab082-b895-4e76-b8d0-a025de6b99b2" />

5. configuration mode, which is the mode used to configure the switch.
6. <img width="1005" height="325" alt="image" src="https://github.com/user-attachments/assets/37e1b88f-aef5-4d31-9f50-bc9f09a27ce1" />
The text inside parentheses in the command prompt identifies the configuration mode. For example, the first command prompt after you enter configuration mode lists (config), meaning global configuration mode. After the line console 0 command, the text expands to (config-line), meaning line configuration mode. Each time the command prompt changes within config mode, you have moved to another configuration mode.
<img width="994" height="295" alt="image" src="https://github.com/user-attachments/assets/2635a88d-f644-42ef-9d32-72b935ae3978" />
7.<img width="871" height="523" alt="image" src="https://github.com/user-attachments/assets/d3e6bf21-8554-40c9-8e14-6a39812c5951" />

8. If you want to keep that configuration, you have to copy the running-config file into NVRAM, overwriting the old startup-config file.
9. Note that Cisco IOS does not have a command that erases the contents of the runningconfig file. To clear out the running-config file, simply erase the startup-config file, and then reload the switch, and the running-config will be empty at the end of the process.

#### chapter 5
1. <img width="869" height="563" alt="image" src="https://github.com/user-attachments/assets/6d3f70c6-6266-46e7-b42f-6cf73fca97c2" />
2. <img width="905" height="630" alt="image" src="https://github.com/user-attachments/assets/d2696143-023e-46bd-80bf-1aaf7ebb47a1" />
3. <img width="926" height="404" alt="image" src="https://github.com/user-attachments/assets/2425e52c-9e5b-442b-adeb-b98d0625e36c" />
4. <img width="924" height="355" alt="image" src="https://github.com/user-attachments/assets/1ef6f576-ca14-4884-8377-734ab6264526" />

#### chapter 6
1. <img width="920" height="490" alt="image" src="https://github.com/user-attachments/assets/4370effd-e6c5-4db0-b72d-def18e73c6ea" />
2. <img width="955" height="763" alt="image" src="https://github.com/user-attachments/assets/c6d2abe4-dcf3-40fb-a8c7-262e9bee44c1" />
3. <img width="862" height="433" alt="image" src="https://github.com/user-attachments/assets/6abdc86d-f6d5-4318-b265-ea28dc094ba1" />
4. authentication, authorization, and accounting (AAA) server
5. <img width="776" height="479" alt="image" src="https://github.com/user-attachments/assets/02e59511-da39-4ef2-a8d5-864286d1b2d5" />
6.  The transport input command identifies the protocols allowed in the vty ports, with the all keyword including SSH and Telnet.
```
        transport input all or transport input telnet ssh: Support both Telnet and SSH
        transport input none: Support neither
        transport input telnet: Support only Telnet
        transport input ssh: Support only SSH
```
7.
   - Use the **no ip http server** global command to disable the HTTP server (port 80) (traditionally enabled by default).
   - Use the **ip http secure-server** global command to enable the HTTPS server (port 443, uses TLS) (traditionally enabled by default).
   - Use the **ip http authentication** local global command to define the authentication method to use locally defined usernames (traditionally defaults to use the enable password).
   - Use the **username name privilege 15 password** pass-value global command to define one or more usernames with privilege level 15.

8.  by default creating two levels, 0 and 15. IOS assigns user mode to level 0 and privileged mode (enable mode) to level 15.
9.   the switch then uses a NIC-like concept called a switch virtual interface (SVI), or more commonly, a **VLAN interface**. By using interface VLAN 1 for the IP configuration, the switch can then send and receive frames on any of the ports in VLAN 1. In a Cisco switch, by default, all ports are assigned to VLAN 1.
10.   <img width="1032" height="432" alt="image" src="https://github.com/user-attachments/assets/fe6fa310-63ff-4bb8-9593-f04574789cf3" />
11. <img width="1123" height="451" alt="image" src="https://github.com/user-attachments/assets/618b25bf-ffec-4e5d-9bea-ad6d19ce7619" />
12. <img width="1202" height="435" alt="image" src="https://github.com/user-attachments/assets/7ecc6879-43b6-4e6d-81fb-d08abef5fe0e" />
13. the [no] shutdown command. To administratively enable an interface on a switch, use the no shutdown interface subcommand; to disable an interface, use the shutdown interface subcommand.
14. <img width="1192" height="418" alt="image" src="https://github.com/user-attachments/assets/9c201ea5-1afc-466b-8861-a3e63b9916ee" />
15. if using DHCP, use the show dhcp lease command to see the (temporarily) leased IP address and other parameters. (Note that the switch does not store the DHCP-learned IP configuration in the running-config file.)
16. <img width="1189" height="368" alt="image" src="https://github.com/user-attachments/assets/bef1f977-2caf-4077-b296-d455e04d7b6d" />

#### chapter 7
1. Autonegotiation gives the devices on each link the means to agree to use the best speed without manually configuring the speed on each switch port.
2. **Fast Link Pulses(FLPs)** use outof-band electrical signaling, independent of the various physical layer standards for Ethernet frame transmission. Any device that supports autonegotiation supports using these out-ofband FLP messages. The FLPs solve the problem of how the devices can send information to each other even before the link is up and working for normal data transmission.
3. The IEEE refers to the logic used by autonegotiation when the other device has disabled autonegotiation as parallel detection, summarized as follows:
 - **Speed**: Detect the neighboring device’s physical layer standard by analyzing the neighbor’s incoming frames. Use that speed.
 - **Duplex**: Make a default choice based on speed—half duplex if the speed is 10 or 100 Mbps, and full duplex if faster.
 - Ethernet interfaces using speeds more than 1 Gbps always use full duplex.

4. <img width="1190" height="379" alt="image" src="https://github.com/user-attachments/assets/fcb9f0b5-20aa-4049-b253-ee309ff035a3" />
5. Autonegotiation can work only if the physical link works. 
6. <img width="1185" height="842" alt="image" src="https://github.com/user-attachments/assets/009bff7e-bab9-438f-a812-2b027129d9e1" />
7. Auto-MDIX works if either one or both endpoints on the link enable auto-MDIX
8. <img width="1224" height="666" alt="image" src="https://github.com/user-attachments/assets/112bbc13-5f55-4bf8-ac10-6b65f2a3f09f" />


9. - If you configured speed 1000 on an interface, the no speed command on that same interface reverts to the default speed setting (which happens to be speed auto).
   - Similarly, if you configured an earlier duplex half or duplex full command, the no duplex command in interface mode for the same interface reverts the configuration to the default duplex auto.
   - If you configured a description command with some text, to go back to the default state of having no description command for that interface, you can use the no description command when in interface configuration mode for that same interface.

10. <img width="1200" height="735" alt="image" src="https://github.com/user-attachments/assets/1f8621dc-0cbd-4ee6-98de-8e236a190005" />

11. if the duplex settings do not match on the ends of an Ethernet segment, the switch interface will still be in a connected state

#### chapter 8
1. A **LAN** includes all devices in the same broadcast domain.A broadcast domain includes the set of all LAN-connected devices, so that when any of the devices sends a broadcast frame, all the other devices get a copy of the frame. So, from one perspective, you can think of a LAN and a broadcast domain as being basically the same thing.
<img width="1216" height="419" alt="image" src="https://github.com/user-attachments/assets/98bb8a67-2160-49de-9e79-09cbaeee55a1" />
<img width="1054" height="212" alt="image" src="https://github.com/user-attachments/assets/4d6068bf-3282-4c47-a086-2d988e7c26a2" />

2. The following list summarizes the most common reasons for choosing to create smaller broadcast domains (VLANs):
 - To reduce CPU overhead on each device, improving host performance, by reducing the number of devices that receive each broadcast frame
 - To reduce security risks by reducing the number of hosts that receive copies of frames that the switches flood (broadcasts, multicasts, and unknown unicasts)
 - To improve security for hosts through the application of different security policies per VLAN
 - To create more flexible designs that group users by department, or by groups that work together, instead of by physical location
 - To solve problems more quickly, because the failure domain for many problems is the same set of devices as those in the same broadcast domain
 - To reduce the workload for the Spanning Tree Protocol (STP) by limiting a VLAN to a single access switch

3. <img width="1026" height="610" alt="image" src="https://github.com/user-attachments/assets/8a4cd2ab-528a-4bb6-a096-fa3f582c3b6a" />
4. <img width="978" height="550" alt="image" src="https://github.com/user-attachments/assets/d764c7f9-b738-4056-aae3-836ac7df37a1" />

5. This 12-bit fieldsupports a theoretical maximum of 212 (4096) VLANs, but in practice it supports a maximum of 4094. (Both 802.1Q and ISL use 12 bits to tag the VLAN ID, with two reserved values [0 and 4095]).
6. Cisco switches break the range of VLAN IDs (1–4094) into two ranges: the normal range and the extended range. All switches can use normal-range VLANs with values from 1 to 1005. Only some switches can use extended-range VLANs with VLAN IDs from 1006 to 4094. The rules for which switches can use extended-range VLANs depend on the configuration of the VLAN Trunking Protocol (VTP)
7. <img width="802" height="288" alt="image" src="https://github.com/user-attachments/assets/4fe4e40d-f116-4233-9a5e-52555ce38d1d" />

8. 802.1Q also defines one special VLAN ID on each trunk as the native VLAN (defaulting to use VLAN 1). In a normally working 802.1Q trunk, both endpoints use trunking, and both use the same native VLAN. Neither end, when sending a frame assigned to this native VLAN, adds the 802.1Q header. Both switches, knowing that untagged frames mean that the frame is part of the native VLAN, treat untagged frames as being part of the native VLAN.
9. To forward packets between VLANs, the network must use a device that acts as a router. You can use an actual router or use a switch that can perform some functions like a router. These switches that also perform Layer 3 routing functions go by the name multilayer switch or Layer 3 switch.
 <img width="920" height="385" alt="image" src="https://github.com/user-attachments/assets/7c7bf4fb-aa8b-4f8f-b055-8b388c7f1065" />

10. <img width="831" height="336" alt="image" src="https://github.com/user-attachments/assets/2c4b1d22-9027-4cfb-9fd1-9ecff88e1326" />
<img width="1016" height="519" alt="image" src="https://github.com/user-attachments/assets/bb36ff4c-e412-4b9d-b2c1-d20be93bb583" />
<img width="1002" height="850" alt="image" src="https://github.com/user-attachments/assets/e4e33103-5517-40a0-a68b-9a698462dcb4" />

11. <img width="939" height="307" alt="image" src="https://github.com/user-attachments/assets/55dca5e0-a5c6-49ce-afdd-2d000efec04b" />
<img width="869" height="484" alt="image" src="https://github.com/user-attachments/assets/58d385ac-4096-4b2e-9b95-87ea42d709ba" />

12. <img width="1000" height="362" alt="image" src="https://github.com/user-attachments/assets/7a6fd720-045f-41d4-b256-ca91e9a7276c" />
13. <img width="1010" height="484" alt="image" src="https://github.com/user-attachments/assets/cb30ee2a-7dda-42d4-87ba-bc6709f18956" />
14. <img width="988" height="392" alt="image" src="https://github.com/user-attachments/assets/839dcb5e-bcd4-4210-bdd8-56c99160f57a" />

#### chapter 9
1. The storm also causes a much more subtle problem called MAC table instability. MAC table instability means that the switches’ MAC address tables keep changing because frames with the same source MAC arrive on different ports.
2. <img width="1003" height="306" alt="image" src="https://github.com/user-attachments/assets/5ed1c2bd-7cd9-4596-8206-53804d064f24" />

3. - STP/RSTP elects a root switch. STP puts all working interfaces on the root switch in a forwarding state.
   - Each nonroot switch calculates the least-cost path between itself and the root switch based on STP/RSTP interface costs. The switch port that begins that least-cost path is its root port (RP), and the cost is the switch’s root cost.
   - In a modern Ethernet that uses switches, each physical link connects two devices only. With two switches on a link, the switch with the lowest root cost becomes the designated switch, and its port connected to that link is the designated port (DP) on the link.
   - <img width="866" height="393" alt="image" src="https://github.com/user-attachments/assets/6eab2b35-d74b-41fc-819b-bab87894f6ea" />

4. <img width="869" height="375" alt="image" src="https://github.com/user-attachments/assets/6cd03ae2-379e-4587-bcb7-ebe78d4a6177" />
5. <img width="806" height="289" alt="image" src="https://github.com/user-attachments/assets/a7d11102-eca3-4ff7-9bbe-47f8e2a5e356" />

#### chapter 10
1. Cisco uses the term access switch to refer to switches used to connect to endpoint devices. The term distribution switch refers to switches that do not connect to endpoints but rather connect to each access switch, providing a means to distribute frames throughout the LAN. 

2. The term uplink refers to the switch-to-switch links, usually trunks, between access and distribution switches.

3. <img width="969" height="380" alt="image" src="https://github.com/user-attachments/assets/8845a556-331a-459b-ad44-5945035e48fb" />
<img width="959" height="221" alt="image" src="https://github.com/user-attachments/assets/94116b8d-c49c-438f-a183-09fcd2225f51" />
<img width="904" height="352" alt="image" src="https://github.com/user-attachments/assets/a0741e58-fee6-4cdf-b955-8d02b08702d5" />
4. <img width="971" height="611" alt="image" src="https://github.com/user-attachments/assets/3fa0b6ab-dca2-44fd-b93f-9ec12532956c" />
5. <img width="902" height="258" alt="image" src="https://github.com/user-attachments/assets/4a28ad2d-abc4-4e5c-9992-eeb7b0ab0f99" />

6. standard RSTP behaves as if VLANs do not exist, while Cisco’s RPVST+ integrates VLAN information into the entire process.

7. You should not use PortFast on trunk ports connected to other switches, but you can use it on trunk ports connected to endpoints, as seen in the center of Figure 10-8
    <img width="756" height="491" alt="image" src="https://github.com/user-attachments/assets/03f4c401-2030-4f08-baa5-2a0a629f2f37" />

8.<img width="1017" height="428" alt="image" src="https://github.com/user-attachments/assets/6f0d3952-a726-4103-8d16-e3b42973f3c5" />

#### chapter 11
1. <img width="919" height="241" alt="image" src="https://github.com/user-attachments/assets/71cdf68c-9c49-4467-b4ed-00948ec1e240" />

2.  - Addresses in the same subnet are not separated by a router.
    - Addresses in different subnets are separated by at least one router.

3. <img width="498" height="218" alt="image" src="https://github.com/user-attachments/assets/69e690eb-a3b6-49ac-b9a7-cae9415258cb" />

4. <img width="491" height="99" alt="image" src="https://github.com/user-attachments/assets/67a36998-acd0-4a25-867e-5a7bf951f470" />

5. <img width="611" height="264" alt="image" src="https://github.com/user-attachments/assets/38e777b3-8057-4a5f-99cd-62094b24ba99" />

#### chapter 12 
1. <img width="961" height="405" alt="image" src="https://github.com/user-attachments/assets/880d83c6-c970-449a-8aa2-4647722e3270" />

2. - The addresses in the same network have the same values in the network part.
   - The addresses in the same network have different values in the host part.
#### chapter appendix M
1. <img width="918" height="431" alt="image" src="https://github.com/user-attachments/assets/9555422d-304f-4a2c-8a5b-4f38c9911e56" />

2. If overlapping subnets are implemented, routing problems occur and some hosts simply cannot communicate outside their subnets.

3. Each classful network has four key numbers that describe the network. You can derive these four numbers if you start with just one IP address in the network. The numbers are as follows:
 - Network number
 - First (numerically lowest) usable address
 - Last (numerically highest) usable address
 -  Network broadcast address

4. the lowest number in the network is the network ID. Then, the first (numerically lowest) host IP address is one larger than the network number.
5.  The TCP/IP RFCs define a network broadcast address as a special address in each network. This broadcast address could be used as the destination address in a packet, and the routers would forward a copy of that one packet to all hosts in that classful network.

6.  <img width="941" height="371" alt="image" src="https://github.com/user-attachments/assets/1fc7f4cb-e38c-4d26-9243-8da7fd3bb489" />

#### chapter 13
1. The subnet mask subdivides the IP addresses in a subnet into two parts: the prefix, or subnet part, and the host part.
2. - Classless addressing: The concept that an IPv4 address has two parts—the prefix part plus the host part—as defined by the mask, with no consideration of the class(A, B, or C).
   - Classful addressing: The concept that an IPv4 address has three parts—network, subnet, and host—as defined by the mask and Class A, B, and C rules.
  
#### chapter 14

#### chapter 15

#### chapter 16
1. IOS XE devices can support upgrading the OS while continuing to forward frames and packets, while IOS cannot
2. <img width="865" height="253" alt="image" src="https://github.com/user-attachments/assets/640ad89b-96ee-4b56-a4d7-80725580a89a" />
<img width="905" height="285" alt="image" src="https://github.com/user-attachments/assets/7e1f9c52-aafd-4e5a-9b01-abe2973cab98" />
3. <img width="958" height="238" alt="image" src="https://github.com/user-attachments/assets/463597d0-7704-4d9e-8aba-059da100b092" />
4. The Aux port works like the console port, except that the Aux port is typically connected through a cable to an external analog modem, which in turn connects to a phone line. Then, the engineer uses a PC, terminal emulator, and modem to call the remote router. After being connected, the engineer can use the terminal emulator to access the router CLI, starting in user mode as usual.
5. <img width="879" height="84" alt="image" src="https://github.com/user-attachments/assets/82a06a5a-1fe3-4e77-b4da-31511407a710" />

6. Floating static routes exist in the configuration of a router, but the router floats the route into the routing table and out of the routing table based on certain conditions
   <img width="885" height="400" alt="image" src="https://github.com/user-attachments/assets/464506a1-604c-4f5f-b725-8702afc2cf9b" />

#### chapter 17

#### chapter 18
1. the devices in one VLAN typically use IP addresses in one subnet. By the same reasoning, devices in two different VLANs are normally in two different subnets. For two devices in different VLANs to communicate with each other, routers must connect to the subnets that exist on each VLAN, and then the routers forward IP packets between the devices in those subnets.

2. <img width="1093" height="532" alt="image" src="https://github.com/user-attachments/assets/0bec24a9-0a43-4304-818f-45350b5e5790" />

3. The router needs to have an IP address/mask associated with each VLAN on the trunk. However, the router has only one physical interface for the link connected to the trunk. Cisco solves this problem by creating multiple virtual router interfaces, one for each supported VLAN on that trunk. Cisco calls these virtual interfaces **subinterfaces**, and the router configuration includes an ip address command for each subinterface.

4. <img width="762" height="314" alt="image" src="https://github.com/user-attachments/assets/69c2a46c-edc1-4043-9f3d-c53262db886f" />

5. note that most Cisco routers do not attempt to negotiate trunking, so both the router and switch need to manually configure trunking.
<img width="898" height="625" alt="image" src="https://github.com/user-attachments/assets/27a5d0a1-e5c4-4c06-b8f4-53edda933684" />

6. The two options to define a router interface for the native VLAN are:
   - Configure the ip address command on the physical interface, but without an encapsulation command; the router considers this physical interface to be using the native VLAN.
   - Configure the ip address command on a subinterface and use the encapsulation dot1q vlan-id native subcommand to tell the router both the VLAN ID and the fact that it is the native VLAN.
<img width="871" height="704" alt="image" src="https://github.com/user-attachments/assets/3774f30e-56aa-400a-9a29-b440f5e46e03" />

7. the subinterface state can also be enabled and disabled independently from the physical interface, using the no shutdown and shutdown commands in subinterface configuration mode. For instance, the physical interface and subinterface .10 can remain up/up, while subinterface .20 can be independently shut down.

#### chapter 19 
1. <img width="912" height="318" alt="image" src="https://github.com/user-attachments/assets/5d1cb4dd-64c3-4a4c-98b0-3be7cf6d78f2" />
2. When the DHCP process fails, the DHCP client self-assigns an APIPA IP address from within a subset of the 169.254.0.0 Class B network, along with default mask 255.255.0.0.
<img width="905" height="277" alt="image" src="https://github.com/user-attachments/assets/f0c6a7fc-bf2e-4b17-b7e3-91c1a7b77296" />

3. <img width="920" height="378" alt="image" src="https://github.com/user-attachments/assets/36b4841f-edbf-41b7-a029-6c323c90726b" />

#### chapter 21
1. <img width="929" height="322" alt="image" src="https://github.com/user-attachments/assets/f5d36a98-eea7-462f-b2af-5b4de3a7238b" />
2. <img width="749" height="186" alt="image" src="https://github.com/user-attachments/assets/43637f4a-2b7c-4a1f-bcee-233e9ef7e635" />
3. Today, Border Gateway Protocol (BGP) is the only EGP.
4. The bandwidth interface subcommand does not change the actual physical speed of the interface. It just tells IOS what speed to assume the interface is using.

#### chapter 22
1. <img width="800" height="641" alt="image" src="https://github.com/user-attachments/assets/b3149c5c-5cad-49a9-b712-1ba3d60952c9" />
2. <img width="946" height="236" alt="image" src="https://github.com/user-attachments/assets/cc3785c8-467a-4585-8085-03edb36bd60d" />
3. <img width="1150" height="319" alt="image" src="https://github.com/user-attachments/assets/31a2c248-5bc6-4bac-86cb-6dfcefc1418e" />

#### chapter 24
1. <img width="1205" height="365" alt="image" src="https://github.com/user-attachments/assets/9e2137e9-a7b9-42b4-a098-e11a82ba75ab" />

#### chapter 26
1. **Global Unicast Addresses (GUAs)**: These addresses work like public IPv4 addresses. The organization that needs IPv6 addresses asks for a registered IPv6 address block, which is assigned as a global routing prefix. After that, only that
organization uses the addresses inside that block of addresses—that is, the addresses that begin with the assigned prefix.

2. **Unique Local Addresses (ULAs)**: These addresses work somewhat like private IPv4 addresses, with the possibility that multiple organizations use the exact same addresses, and with no requirement for registering with any numbering authority.

### new words
1. excerpt
2. As an aside
3. framer
4. small office/home office (SOHO) networks
5. a standard-first-code-second approach
6. Requests For Comments (RFC)
7. electromagnetic interference (EMI)
8. ranch
9. High-Level Data Link Control (HDLC)
10. Point-to-Point Protocol (PPP)
11. Spanning Tree Protocol (STP)
12. Open Shortest Path First (OSPF) 
13. Boardcast Storm  Broadcast storms happen when any kind of Ethernet frames—broadcast frames, multicast frames, or unknowndestination unicast frames—loop around a LAN indefinitely.
14.  common spanning tree (CST)
15. RPVST+ (one tree per vlan)
16. variable-length subnet masks (VLSM)
17. octet
18. dotted-decimal notation (DDN)
19. router-on-a-stick (ROAS)
20. Layer 3 switch/multilayer switch
21. switched virtual interfaces (SVIs)
22. Automatic Private IP Addressing (APIPA)
23. Organizationally Unique Identifier (OUI)
24. AS number (ASN)
25. link-state advertisements (LSAs
26. acronym
