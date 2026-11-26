# Day 3 - TCP/IP Network Model

- Protocol - Set of rules defining how data should be communicated between devices in a network.
- OSI - Open Systems Interconnection
- TCP/IP - Transmission Control Protocol/Internet Protocol

## OSI model

![[OSI layers.png]]

Please don’t teach students pointless acronyms.

- Application Layer
- Presentation Layer
- Session Layer
- Transport Layer
- Data Link Later
- Physical Layer

![[OSI and TCP-IP models.png]]

## TCP/IP Model

![[TCP-IP layers.png]]

- Physical Layer - Are the equipment that is used to form a network.
- Data Link Layer - Does hop to hop delivery by the use of Media Access Control (Mac Address)

![[Figure 4.2 Data Link hops.png]]

- Network Layer - Ensures end to end delivery of the message.

![[Figure 4.3 Network layer.png]]

- Transport Layer - The Application's Ports that the data is addressed to (not the physical Ports).
- Application Layer - Requests and receives or prepares the data.

## TCP/IP Encapsulation Summary

### Encapsulation (Sender)

```
Data
+ TCP Header
= Segment
+ IP Header
= Packet
+ Ethernet Header
+ Ethernet Trailer (FCS)
= Frame
```

Converted to Bits, then sent across cable/Wi-Fi.

### Decapsulation (Receiver)

```
Bits
→ Frame   → Remove Ethernet Header/Trailer
→ Packet  → Remove IP Header
→ Segment → Remove TCP Header
→ Data
```

### Protocol Data Unit (PDU) Names

```
Application = Data
Transport   = Segment
Network     = Packet
Data Link   = Frame
Physical    = Bits
```

### Key Header Information

| Header | Fields |
| --- | --- |
| TCP Header (Transport Layer) | Source Port, Destination Port, Sequence Number, Acknowledgment Number, Flags (SYN, ACK, FIN), Checksum |
| IP Header (Network Layer) | Source IP, Destination IP, TTL, Protocol (TCP/UDP) |
| Ethernet Header (Data Link Layer) | Source MAC, Destination MAC, EtherType |
| Trailer (Ethernet FCS) | Error detection mechanism |

- Receiver recalculates FCS
	- Match = Frame accepted
	- No match = Frame discarded
- FCS = Frame Check Sequence

### Encapsulation Structure

```
[Ethernet Header]
    [IP Header]
        [TCP Header]
            [Data]
[Ethernet Trailer/FCS]
```

### CCNA Exam Memorization

```
Data → Segment → Packet → Frame → Bits
Bits → Frame → Packet → Segment → Data
```

Layer 2 = MAC Address Layer 3 = IP Address Layer 4 = Port Number

## Adjacent-Layer Interaction vs Same-Layer Interaction

This is a common networking concept.

### 1. Adjacent-Layer Interaction (Vertical Communication)

Layers on the same device communicate with the layer directly above or below them.

Example on the sender:

```
Application
Transport
Network
Data Link
Physical
```

Flow: Application → Transport → Network → Data Link → Physical

- Application gives data to Transport.
- Transport adds TCP header and passes segment to Network.
- Network adds IP header and passes packet to Data Link.

This is called adjacent-layer interaction because communication happens between neighboring layers.

### 2. Same-Layer Interaction (Horizontal / Peer-to-Peer Communication)

A layer on the sender appears to communicate with the same layer on the receiver.

Example:

```
Sender                           Receiver

Application  <------------->  Application
Transport    <------------->  Transport
Network      <------------->  Network
Data Link    <------------->  Data Link
Physical     <------------->  Physical
```

In reality, the data travels down and up the stack, but each layer's header contains information intended for its peer layer.

- Sender TCP adds a TCP header.
- Receiver TCP reads and processes that TCP header.

So we say:

```
TCP ↔ TCP
IP ↔ IP
Ethernet ↔ Ethernet
```

This is called same-layer (peer-layer) interaction.

### Quick CCNA Note

```
Adjacent-Layer Interaction
Vertical communication
Within the same device

Application → Transport
Transport → Network
Network → Data Link
Data Link → Physical

Same-Layer Interaction
Horizontal (peer-to-peer)
Between sender and receiver

Application ↔ Application
Transport ↔ Transport
Network ↔ Network
Data Link ↔ Data Link
Physical ↔ Physical
```

### Easy Memory Trick

```
Adjacent Layer = Up and Down
Same Layer     = Across
```

Diagram:

```
Host A                          Host B

Application  <------------->  Application
Transport   <------------->   Transport
Network     <------------->   Network
Data Link   <------------->   Data Link
Physical    <------------->   Physical
```

Vertical arrows = Adjacent-layer interaction
Horizontal arrows = Same-layer (peer) interaction