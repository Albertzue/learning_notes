## page：
2025/9/6   41

2025/9/7  113

2025/9/8  133

2025/9/9  158

2025/10/09 227 ps: physical layer is skipped currerntly 

2025/10/10 251

2025/10/13 plan/real   300/358

2025/10/13 plan/real   380/383

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

## terms：
**gateway** The device that makes a connection between two or more networks and provides the necessary translation, both in terms of hardware and software

**store-and-forward switching**

**cut-through switching**

**full-duplex links**

**half-duplex links**

**simplex links**

The width of the frequency range transmitted without being strongly attenuated is called the **bandwidth**
