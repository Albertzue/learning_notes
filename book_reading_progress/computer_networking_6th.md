## page：
2025/9/6   41

2025/9/7  113

2025/9/8  133

2025/9/9  158

2025/10/09 227 ps: physical layer is skipped currerntly 

2025/10/10 251

2025/10/13 plan/real   300/358

2025/10/13 plan/real   380/383

2025/10/17  450/425

2025/10/19 450/451

2025/10/20  480/505

2025/10/21 550/570

## Keypoint:

#### physical layer：
1. A device that converts between a stream of digital bits and an analog signal that represents the bits is called a **modem**

<img width="795" height="247" alt="image" src="https://github.com/user-attachments/assets/c2d70f73-58e1-41b7-b88c-67a9d0b2d9e6" />

#### datalink layer：
<img width="907" height="307" alt="image" src="https://github.com/user-attachments/assets/a89d0358-97fd-4b27-a184-180f0708c810" />

**Unacknowledged connectionless service** consists of having the source machine
send independent frames to the destination machine without having the destination
machine acknowledge them. **Ethernet** is a good example of a data link layer that
provides this class of service.

**Acknowledged connectionless service** there are still no logical connections used, but each frame sent is individually acknowledged. 802.11 (WiFi) is a good example of this type of link
layer service

**ESC** special escape byte

The data link layer on the receiving end removes the escape bytes before
giving the data to the network layer. This technique is called **byte stuffing**.

An n-bit unit containing data and check bits is referred to as an n-bit **codeword**

The number of bit positions in which two codewords differ is called the **Hamming distance**. Its significance is that
if two codewords are a Hamming distance d apart, it will require d single-bit errors to convert one into the other

The technique of temporarily delaying outgoing acknowledgements so that they can be hooked onto the next outgoing data frame is known as **piggybacking**

One option, called **go-back-n**, is for the receiver to just discard all subsequent frames, sending no acknowledgements for the discarded frames.

the **selective repeat protocol**, is to allow the receiver to accept and buffer correct frames received following a damaged or lost one.
<img width="853" height="697" alt="image" src="https://github.com/user-attachments/assets/4ec85211-5c79-430e-bb26-382b102b7001" />

**FDM** (Frequency Division Multiplexing)

#### network layer:
1. If connectionless service is offered, packets are injected into the network individually and routed independently
of each other. No advance setup is needed. In this context, the packets are frequently called **datagrams** (in analogy with telegrams) and the network is called a **datagram network**.

2. If connection-oriented service is used, a path from the source
router all the way to the destination router must be established before any data
packets can be sent. This connection is called a **VC** (Virtual Circuit), in analogy
with the physical circuits set up by the (old) telephone system, and the network is
called a **virtual-circuit network**.

3. Routing algorithms can be grouped into two major classes: **nonadaptive** and
**adaptive**.

4. **Nonadaptive algorithms** do not base their routing decisions on any
measurements or estimates of the current topology and traffic. Instead, the choice
of the route to use to get from I to J (for all I and J) is computed in advance,
offline, and downloaded to the routers when the network is booted. This procedure
is sometimes called **static routing**.

5. **Adaptive algorithms**, in contrast, change their routing decisions to reflect
changes in the topology, and sometimes changes in the traffic as well. These
**dynamic routing** algorithms differ in where they get their information (e.g.,
locally, from adjacent routers, or from all routers), when they change the routes
(e.g., when the topology changes, or every 6T seconds as the load changes), and
what metric is used for optimization (e.g., distance, number of hops, or estimated
transit time).

6. The distance vector routing algorithm is sometimes called by other names,
most commonly the distributed **Bellman-Ford routing algorithm**
<img width="932" height="410" alt="image" src="https://github.com/user-attachments/assets/807e9abf-ec9a-47b9-a62f-6f71e6f18ed0" />
<img width="1102" height="547" alt="image" src="https://github.com/user-attachments/assets/e12c55a3-9207-42f3-b5b7-219060c69f92" />
<img width="892" height="711" alt="image" src="https://github.com/user-attachments/assets/6d4da922-53c6-4c81-848a-154add61538b" />
<img width="972" height="407" alt="image" src="https://github.com/user-attachments/assets/837289d2-94d8-44cd-ba5e-128f7ca8aedf" />


### transport layer
<img width="1125" height="331" alt="image" src="https://github.com/user-attachments/assets/a3b34f08-df8a-4a35-b2d9-c3ba6d428c78" />
<img width="994" height="450" alt="image" src="https://github.com/user-attachments/assets/cafac8f7-360a-45b9-b732-476765d36db1" />


## new words: 
relay 

antenna

stereos

proliferation

foolproof

stake

plunder 

burglar

eavesdropper

homogeneous

morph

rhyme

astute

whippersnapper

appal

squabble

skepticism

vague

tender

rural

fledgling

spammer

critique

helical

attenuated

sheath

insulated

stiff

encase

cutaway

attenuate

distortion

amplitudes

toll

convergence

## terms：
**gateway** The device that makes a connection between two or more networks and provides the necessary translation, both in terms of hardware and software

**store-and-forward switching**

**cut-through switching**

**full-duplex links**

**half-duplex links**

**simplex links**

The width of the frequency range transmitted without being strongly attenuated is called the **bandwidth**
