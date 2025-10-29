### Info
https://www.certskills.com/ccna2024-07/
### schedule(plan/finish)
2025/10/28 100/100

2025/10/29 130/120

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

### new words
1. excerpt
2. As an aside
3. framer
4. small office/home office (SOHO) networks
5. a standard-first-code-second approach
6. Requests For Comments (RFC)
7. electromagnetic interference (EMI)
8. ranch
