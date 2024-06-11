---
title: CITS3002 Notes
description: Uni Notes
layout: default.hbs
---

<a class="link" href="./notes.html">cd -</a>

>Written by Jeremy Butson 2024 based on UWA CITS3002 Lecture Notes


# Introduction
## Definitions:
- Computer Network: an interconnected collection of autonomous computers
	- interconnected if they are capable of exchanging information
- Computers are autonomous if there is not a permanent master/slave relationship between them. 

## Internet Protocols:
- Consists of an agreed format for messages, expressed by a packet header, an optional message component, and a set of rules for the exchange of messages between computers.
- Must - 
	- happen in an agreed order
	- travel from the sender to the correct receiver(s)
	- contain the correct unambiguous data

## ISO/OSI Reference Model:
- We require protocols to "meet" new computers, ask for information, agree to share data, etc.
- Open Systems Interconnection/International Standards Organization
- The 7 layer model:
1. **THE PHYSICAL LAYER**: is responsible for transmitting a (raw) bit stream over the physical communication medium. 
2. **THE DATA-LINK LAYER**: takes the bit stream from the physical layer and constructs logical chunks of data termed *frames*.
3. **THE NETWORK LAYER**: is responsible for providing the connection between "end systems" across a network. Network layer functions include:
	1. Routing: deciding how to transmit frames between source and destination using addresses
	2. Relaying: enables data transfer across intermediate networks
	3. Flow control: matches traffic flow with physical capacity of a transmission path
	4. Sequencing: control ordering of frames across a network
4. **THE TRANSPORT LAYER**: provides a reliable end-to-end service independent of the network topology. This is achieved by splitting messages into network sized packets and joining them back together again at the other end.
5. **THE SESSION LAYER**: is the upper layer crucial to internetworking and manages the dialogue between end systems. Typically provides:
	1. establishment and closing of connections
	2. synchronization to allow checking and recovery of data
	3. negotiation of full and half duplex communication
6. **THE PRESENTATION LAYER**: provides a standard format for transferred information by overcoming compatibility problems between systems using dissimilar data encoding rules and possibly different display technologies. 
7. **THE APPLICATION LAYER**: provides the interface between the application processes. In particular, functions such as file transfer, remote job execution and application dependent virtual terminal support are provided.

# The Physical Layer
## Physical Layer Responsibilities:
- Provides topology of network
- Provides transfer medium
- \[TX] Encodes data into a transmission signal supported by medium
- \[RX] Decodes data into a transmission signal supported by medium
- \[TX+RX] Generates or amplifies re-transmitted signals along the medium
- \[RX] Monitors transmission errors
- \[RX] Detects arriving signal levels to synchronize speed and timing

## Data Link Layer Responsibilities:
- \[TX] Constructs data frames using the format of the physical layer
- \[TX] Calculates Cyclic Redundancy Codes (CRC) information
- \[RX] Checks arriving error using CRC information 
- \[RX] Initiates and arbitrates the link to reduce interruption and contention
- \[RX] Examines arriving and passing device addresses in data
- \[RX+TX] Acknowledges receipt of a frame
- \[RX+TX] Retransmits data if there is an error

## Metrics of Network Measurement:
- We want high bandwidth and low latency
- **Latency/Propagation Delay**: amount of time it takes for the first bit to reach its destination. Round-trip time (RTT) is twice the latency. 
- **Bandwidth**: the number of bits that can be fit through a network connection, per unit time.
- **Throughput**: usually the measured number of bits per second, while bandwidth is the nominal bits per second possible. 
$$
T_{latency} = T_{propagation} + T_{transmit} + T_{queue}
$$
$$
T_{propagation} = distance/speedOfPropInMedium
$$
$$
T_{transmit} = messageSize/bandwidth
$$
$$
T_{queue} = timeSpentInLocalAndRemoteOSAndSwitchQueues
$$

## Transmission Errors:
- Usually occur in bursts and are caused by:
	- thermal background noise
	- impulse noise, electrical arcing
	- distorted frequency
	- crosstalk between adjacent wires

## How Data Is Placed In Frames:
- Simple timing gaps between frames cannot be used as all hardware devices run at slightly different speeds; resulting in skewing if time is relied upon
- To overcome synchronization problems, special byte sequences are often used to prefix and suffix the data, so byte stuffing using DLE, STX and ETX

## Phase Encoding Of Signals:
- A digital signal is a sequence of discrete, discontinuous pulses or signal elements
- If all signal elements have the same sign, they are unipolar
- The modulation rate of a LAN is the number of signal elements a second (baud rate)
- Data may be modified so that errors can either be:
	- detected
	- corrected
- Correction is required where communication must be simplex (only possible in one direction), but it is expensive. A good example of its need is between Earth and inter-planetary spacecraft. 
- Error correction by receiver is *forward error correction*, re-transmission schemes are referred to as *reverse error correction*.
- The **HAMMING DISTANCE** between two codewords consists of the number of bit positions in which they differ. The difference is performed via XOR.
	- The Hamming distance of a code is the minimum Hamming distance between any two words in that code. 
- To detect δ errors, a distance of δ + 1 is required
- To correct δ errors a distance of 2δ + 1 is required so that even with δ errors, the damaged codeword is the closest to one valid codeword

## Hamming's Correction of Single-Bit Errors:
- m bits for the message, and r bits of seemingly redundant information, therefore we transmit $$ n=m+r $$ when transmitting a message.
- Each of the 2$^m$ possible message words has n illegal code words which are a distance 1 from it. Therefore, each message word requires n+1 distinct bit patterns. 

## How Does Checksum Error Detection Work?
1. Break original message into k blocks of n bits
2. Sum all k blocks
3. Add the carry to the sum and take the 1's complement
4. If when the receiver sums the k blocks and the check sum block and it adds to all 1s, then it accepts the data, otherwise it is wrong

## How Does CRC (Cyclic Redundancy Check) Work?
1. Find the length of divisor ('L' in this example)
2. Append L-1 bits to the original message
3. Perform binary division operation
4. Remainder is the CRC
	1. The CRC hence is L-1 bits

# Data Link Layer
### What is the Data Link Layer?
- The Data Link Layer provides the following services between the physical and network layers:
	- bundling and unbundling groups of bits into *frames* for the physical layer
	- *throttling* the flow of frames between sender and receiver
	- detecting and correcting "higher-level" transmission errors, such as the sequencing of packets from the network layer

### 3 Levels of Data Link Layer Complexity:
- **Simplex connectionless** - the sender simply sends its frames without waiting for the receiver to acknowledge them. No attempt is made to detect or re-transmit lost frames. Most modern LAN technologies (such as ethernet) use this method and leave error resolution to higher layers. A.K.A. unacknowledged connectionless service.
- **Half-duplex connectionless** - each frame sent is individually acknowledged. Frames which are lost or garbled are retransmitted if the receiver requests them (again) or after a suitable timeout. A.K.A. acknowledged connectionless service.
- **Full-duplex connection-oriented** - each frame is individually numbered and is guaranteed by the data link layer to be received once and only once and in the right order. The result is that the data link layer presents a reliable frame *stream* to the network layer. A.K.A. acknowledged connected service. 

### Some Declarations for Introductory Protocols:
- As our protocols "evolve" we'll need to distinguish different types of data link frames from each other
```
#define MAX_DATA_SIZE 1000

typedef struct {
	int len; //length of the payload
	char data[MAX_DATA_SIZE];
} FRAME;

#define FRAME_HEADER_SIZE (sizeof(FRAME) - sizeof(FRAME.data))
#define FRAME_SIZE(f) (FRAME_HEADER_SIZE + f.len)
```

### The Unrestricted Simplex Protocol:
- Assuming:
	- a (unidirectional) error free channel
	- that the sender's network layer has unlimited data to send (being "pushed down" from above)
	- that the receiver's network layer has an infinite buffer to receive the data (being "pushed up" from below)
	- that the functions READ_xxx_LAYER() and WRITE_xxx_LAYER() block until their actions are complete - they execute synchronously
- **In the Sender:**
```c
FRAME frame;
int   len, link = 1;

while( true ) {
    READ_NETWORK_LAYER(frame.data, &len);
    frame.len = len;
    WRITE_PHYSICAL_LAYER(link, &frame, FRAME_SIZE(frame));
}
```
- **In the Receiver:**
```c
FRAME frame;
int   len, link;

while( true ) {
    READ_PHYSICAL_LAYER(&link, &frame, &len);
    WRITE_NETWORK_LAYER(frame.data, frame.len);           
}
```

### Software Simulations:
- **Benefits**:
	- Many different aspects can be controlled and examined on very dynamic "networks":
		- network topology
		- message arrival rate
		- message size and destination
		- transmission speeds and delays
		- frame corruption and loss
		- extent of node and link failures
		- signal strength and propagation models
		- node mobility
	- Real network infrastructure is *static and too reliable* - error rates on local area networks are too infrequent
	- Centralized control of a network permits the accurate management and collection of statistics and their analysis
- **Pitfalls:**
	- The choice of a simulation environment can constrain the types of practical exercises and discourage creativity 
	- The *wrong* choice of network simulator can seriously impede a student's learning and dissuade experimentation
	- Purpose written simulators have constrained domains - transport-layer protocol testbeds do not actually "transmit" the data frames
	- Very few students are enthused by simulations whose role is to verify or develop statistical models
	- Students can perceive a simulation as something that will never happen
	- Too much control/variation can overwhelm

### Frame Pipelining:
- If the distance (in time) between sender and receiver is long or expensive, bandwidth should be maximised
- The solution is to permit *multiple* outstanding frames
- This happens by the sender transmitting *many* frames until the medium is 'full', and then wait for acknowledgements indicating that frames have been received correctly before proceeding
- When frames or acknowledgements are lost:
	- the go-back-to-N protocol
	- the selective repeat protocol

# LANs & WLANs
## Simplified Satellite Broadcasting
- Many users share a *single* channel
- Propagation at the speed of light, 300,000km/sec
- However, the *distance* travelled is large, resulting in round trip times of ~270-700msec
- Bandwidth, typically 500Mbps, is currently about 5x higher than typical LAN-based networks as it less limited by speed of local infrastructure
- Cost is the same whatever the distance between sender and receiver
- Satellite acts as a repeater of incoming signals, amplifying and re-broadcasting these signals
- If 2 stations broadcast simultaneously, the satellite will receive and re-broadcast the *sum* of these 2 signals, resulting in garbage. This is a **collision**
- A sender can listen to a re-broadcast of their own packets and determine whether a collision has occurred, however there are **no acknowledgements**
- Users are uncoordinated and can only communicate via the channel
	- Therefore, the satellite must control its own allocation
- Advantages of this approach (shared medium):
	- No data link layer acknowledgements needed, as users can verify themselves
	- No routing problems in the Network Layer (no subnet!!)
	- No congestion problems or topology optimization
	- Mobile users may be supported
- Disadvantages:
	- Long propagation delay of at least 270ms
	- All users receive all messages

## Channel Allocation
- 2 common schemes:
	- ### **Polling**
		- satellite or ground offers the channel to an individual user for a specified amount of time
		- Delays, making this impractical 
	- ### **Frequency and Time Division Multiplexing**
		- 2 Forms:
			- FDMA (frequency division multiplexing), channel is divided into N frequency bands for a maximum of N users, guard bands are placed between these limits
			- TDMA (time division multiplexing), channel is divided into slots based on time intervals, each user using a channel for that certain amount of time
		- Both are inefficient as the number of users is in "bursts"

## Local Area Networks
> "A LAN is a routerless network, using the same protocol stack for each device, and using only uniform, local, networking media."
- LANs are between about 10 - 0.1km in separation with a bit rate of 100 - 10,000Mbps
- Machines connect to a single cable within a 1km radius (often same building or campus)
- Total data rate >10Mbps (due to short round trip time and simple data bit layer)
- Single organization ownership
- Usually use broadcasting (no routing problems, but everyone sees all frames)

## Carrier Sense Networks
- All stations can *sense* the electrical carrier before sending
	- This is possible because of the use of high speed cables over short distances
- Factors affecting CSMA (carrier-sense multiple access) LANs:
	1. All frames are of constant length
	2. There are no transmission errors
	3. No capture effect
	4. Random delay after collision is uniformly distributed and large compared to the frame's transmission time
	5. Frame generation attempts form a Poisson process with mean G frames per time
	6. A station may **not** transmit and receive simultaneously
	7. Each station can sense the transmission of other stations
	8. Sensing of the channel state can be performed at the same time as transmitting
	9. The propagation delay is small compared to the frames' transmission time, and identical for all stations
- ***Persistent CSMA Protocols:***
	- Each station first senses activity on the channel
	- If stations A and B are waiting for C to finish, they pause until they sense it is free, transmit with a probability of 1
	- The longer the propagation delay = the more collisions, worse performance

## IEEE-802.x LAN Standards - The Ethernet System
- Uses a 1-persistent CSMA with collision detection (CD) method
- Each packet must be at least 64bytes to provide reasonable chance to have collisions be detected over long propagation times
- Due to power losses in Ethernet cables, each segment cannot exceed 500m, so repeaters used to connect up to 5 into a single LAN, this and other physical properties of ethernet are specified in IEEE-802.3

### Ethernet Contention Algorithm
- Each station wanting to transmit, listens to the ether and on finding it silent, begins transmission
- On detecting a collision: (called *binary exponential back off*)
	- Backs off for random period
	- After first collision backs off for 0 or 1 times slots before trying again, second, 0, 1, 2, or 3 times
	- In general a station will back off from 0 to 2<sup>i-1</sup> times after the i<sup>th</sup> collision
	- After 16, it considers it "severed"

## Packet Transport Mechanisms
- Each station connects to the ether with a transceiver, failures of this transceiver must not pollute the ether, power failure must not cloud it, and disconnection must not be noticed by the other stations
- ### 5 Significant Mechanisms to Reduce Probability and Cost of Losing a Packet
	1. Carrier detection (phase encoding which guarantees at least one phase transition)
	2. Packet error detection
	3. Interference detection (each transceiver has an interference detector)
	4. Truncated packet filtering (hardware is able to filter them out)
	5. Collision consensus enforcement (deliberately jamming the ether to ensure the other colliding stations hear the collision as quickly as possible)

## Hubs, Switches and Collision Domains
- A collision now occurs when a device or LAN-segment receives two or more signals simultaneously.
- A hub will retransmit the frame to *ALL* of its outgoing ports, whereas a switch will more 'intelligently' retransmit the signal to the ports known to be wanting the frame. 
- A collision domain is the set of devices (potentially) receiving a frame collision. 

## IEEE-802.11 Wireless LAN Protocol
- Of interest is not just the maximum possible transmission rate, but the distance over which WiFi may operate
- The unit **dBm** is defined as the power ratio in decibel referenced to one milliwatt. It represents absolute power, a WiFi access point (AP) will typically transmit up to 100mW, and a receiving device will typically be able to discern signal from noise until -90dBm

## Hidden Node
- The method of simply waiting until the airways are clear, such as wired, in wireless networks does not work, because not all nodes are within range of each other

## Collision Avoidance (802.11)
- Most wireless cards are unable to both transmit and receive at the same time on the same frequency - they employ *half-duplex* transmissions
- This means collisions cannot be detected while transmitting
- It employs collision *avoidance* to reduce the likelihood of collisions occurring. The algorithm is termed Multiple Access with Collision Avoidance (MACA), where both *physical channel* sensing and *virtual channel* sensing are employed
	- Basically; before transmitting data frames, the sender and receiver must first exchange additional control frames before the 'true' data frames. The success or failure of this initial exchange either reserves the medium for communication or directs how the sender, receiver and all other nodes should act

# Network Layer
- The data link layer had the responsibility of reliably transmitting frames across along a single wire (or wireless) link
- Network layer's responsibility is to get packets from an actual source machine to a destination machine
- The lowest OSI layer that has to deal with end-to-end transmission
- It must be aware of the immediate topology of its subnet to make routing choices

## Network Layer Design Objectives
- The design objectives of an effective Network Layer are:
	- to be independent of processor and communication technology
	- to be independent of the number, type and topology of the subnets
	- to provide a uniform addressing scheme for all hosts in the network

## Responsibilities of the Network Layer
- The network layer includes nearly all of the functions we consider important in multi-node networks
- Each node can be responsible for everything from handling its own links to managing the network topology
- Three types of requirements:
	- **Source and destination functions:** end-to-end protocols, network layer software interface, fragmentation and reassembly of messages, management of network layer sequence numbers, and creation, manipulation and deletion of headers.
	- **Store and forward functions:** choice of the best route for packets, local flow control and local error control
	- **Network-wide management functions:** network flow control, topological awareness and modification, and network performance measurement and monitoring.
- *Further explanation of packet fragmentation and reassembly*:
	- Messages divided into smaller data units (packets) before transmission, they travers the network independently and then the destination stitches them back together, using each packet's header to see where they go
	- This has benefits of a fixed buffer size, prevents congestion at destination and they require simpler memory allocation schemes

## Network Layer Header Management
- The NL header is created in the source node, examined in intermediate nodes and removed at the destination node

## Path of Frames and Packets
- Whereas the data link layer must acknowledge each frame once it successfully transverses a link, the NL acknowledges each packet as it arrives at its destination

## Network Layer Routing Algorithms
- The routing algorithms are the part of the Network Layer software that decides on which outgoing line an incoming packet should go
	- for virtual circuits: route is chosen each session
	- for datagrams: route is chosen for each packet
- Desirable properties for the routing systems are similar to those for the whole network layer:
	- correctness, simplicity, robustness, stability, fairness and optimality
- Robustness is significant for 2 reasons:
	- Once a large network is off and running it is difficult to change the routing algorithm software
	- Network topologies often change - hosts, IMPs and lines frequently fail
- The better a routing algorithm can cope with changes in topology, the more it is

## Two Classes of Routing Algorithm
- Non-adaptive
	- the choice of routes between two hosts are computed in advance and loaded into each host in the whole network
	- often called static routing
	- Example: Flooding, where initially every incoming packet is retransmitted on every link, which gives it the shortest package delay and is robust to machine failures. However, it *does* flood the network. Some possible improvements include not retransmitting it on the link they came from, acknowledgements are sent through *only* this link
- Adaptive
	- attempts to adjust their route choices based on their current knowledge of the network topology
	- Three types:
		- global use information periodically collected from whole network
		- local algorithms use only the information that each router knows about itself
		- combined use both
	- often called dynamic routing
	- Example: Distance Vector Routing, where it maintains a table in each router of the best known distance to each destination and the preferred link to that destination. However, if the reliability is uncertain, we may encounter the count-to-infinity problem, where if a router goes down, that distance/time is infinite. If router A crashes, B may want to send via C, then C does the same to B and so on to infinity. 

## Congestion and Flow-Control in the Network Layer
- If too many packets are dumped into some part of the subnet, network performance will decrease sharply
	- This can increase the frequency of timeouts and re-transmissions
- **Congestion Control** is concerned with ensuring that the subnet can carry the offered traffic - a global issue concerning all hosts and routers working together
- **Flow Control** is concerned with end-to-end control
	- Sender requests the allocation of buffer space and time in the intermediate nodes and the receiver
- Both of these work together to reduce the offered traffic entering the network when the load is already high, detected through:
	- percentage of packets discarded for lack of buffer space
	- average router queue lengths
	- number of packets timing out
	- average packet delay
- **Open Loop Control** attempts to prevent congestion in the first place. Pre-allocating buffer space for each virtual circuit
- **Closed Loop Control** maintains a feedback loop of 3 stages:
	- monitoring of local subnet to detect where congestion occurs
	- passing information to where corrective action may be taken
	- adjustment of local operation to correct problem

## Load Shedding
- If not all demand can be met, some section is deliberately disadvantaged
- The Network Layer now introduces an **UNRELIABLE SERVICE!**
- Constraints:
	- Must balance reasonable delay and user freedom
	- Maintain fair access to all users
	- Respect rights of priority users

# TCP/IP Protocols
#### TCP/IP Protocol Layers & Common Protocols
- Application | Telnet, FTP, SMTP, DNS, RIP, SNMP
- Transport | TCP, UDP
- Internet/Network | ARP, IP, IGMP, ICMP
- Link (can also be referred to as the data link and physical layers) | Ethernet, ATM

#### Requirements of Internetworking
- Networks come in different topologies and speeds, so no single network configuration suits everyone
- Internetworking draws the multitudes of networking technologies into a common framework, combining networks into internets
- In general, an internetwork must: 
	- Provide a link between networks
	- Provide routing and delivery of data
	- Provide an accounting service, keeping track of the status of networks and gateways
	- Accommodate the differences between sub-networks

#### Initial Internet Concepts
**Ground Rules**:
- Each distinct networks would have to stand on its own
- Communications would be on a best effort basis (if a packet doesn't make it to a final destination, it would shortly be retransmitted)
- Black boxes would be used to connect the networks, later called gateways, that hold no information from packets passing through
- No global control at the operations level
**Key Issues**:
- Algorithms to prevent lost packets from permanently disabling communications
- Providing for host to host pipelining
- Gateway functions to allow it to forward packets appropriately
- Need for end-end checksums, reassembly of packets and detection of duplicates
- Need for global addressing
- Test for host-to-host flow control
- Interfacing with various OSs
**Emergent Basic Approaches**:
- Communications consist of a very long streams of bytes (octets)
- Flow control done by sliding windows and acknowledgements
- 32 bit IP address used (8 bits signified network, 24 bits designated the host)

#### Address Resolution Protocol (ARP)
- Low level protocol that hides the underlying physical addressing, permitting one or more internet addresses to be assigned to each machine
- Its design permits it to indicate how big its own fields will be

#### Configuration of Network Devices
- To configure its own network connection, a client host requires:
	- One unique IP address for each network interface
	- The client's hostname
	- Address of default router
	- Each interface's subnet mask (determines how many bits of the IP address provide the network and host ids)
	- IP address of an initial DNS (domain name server)
	- The time, or at least the time zone

#### Problems with Static Configuration
- Sys admins may have to oversee hundreds of machines on a network
- Single network domain may service many more computers than it has registered IP addresses
- Mobile computers may wish to frequently connect to different networks
- Some previously trusted computers may become untrusted

#### Bootstrap Protocol (BOOTP)
- UDP/IP based protocol that allows a booting host to configure itself dynamically
- A server's BOOTP response includes several configuration items and fits in a single (Ethernet) packet
- Immediately boot up and asks through their MAC address what they should be (addresses, IPs, etc.)

#### Dynamic Host Configuration Protocol (DHCP)
- Enables individual computers on an IP network to extract their configurations from a server
- Responses to each client will be generated dynamically
- Overall purpose being to reduce the work necessary to administer a large IP-based network
- Based on BOOTP, however DHCP allows for dynamic allocation of network addresses and configurations to newly attached hosts

#### Internet Protocol (IP) Datagrams
- Provides an unreliable, best-effort, connectionless, packet delivery system
- We will primarily use IP v4
- Internet datagrams resemble standard physical layer frames, but are designed to be encapsulated within the normal network framing schema

#### Internet Control Message Protocol (ICMP)
- Allows gateways and hosts to exchange bootstrap and error information
- Gateways send ICMP datagrams when they cannot deliver a datagram, or to direct hosts to use another gateway

# Transport Layer
#### Port Numbers
- IP addresses only address hosts and not individual OS processes on those hosts
- From the perspective of any transport protocol, such as TCP, each frame is identified by a 16bit positive port number that identifies the software end point
- TCP demultiplexes each arriving segment to its corresponding end point, using a port as an index
- Port numbers under 1024 are *reserved ports*, can be shown on Linux by `/etc/services`

#### Transmission Control Protocol (TCP)
- Transforms raw IP into full duplex reliable character stream
- Uses sliding window with selective-repeat protocol and conveys a number of important fields in its TCP frame header
- **6 Major Features**:
	1. Connection Orientation (one program must first request a connection)
	2. Reliable Connection Start-up (when two apps create a connection, they must both agree)
	3. Point to Point Communication (each communication session has exactly two end points)
	4. Full-Duplex Communication (single connection may be used for messages in both directions)
	5. Stream Interface (from applications view, data is sent and received as a continuous sequence of bytes)
	6. Graceful Connection Shutdown (TCP/IP guarantees to reliable deliver all pending data once a connection is closed by an endpoint)

#### TCP/IP Transmissions
- Due to massively variable distances
- Sliding window protocol and timeouts are employed to force re-transmissions, however as the distance can vary these must vary as well
- Therefore we use the equation:
  $SRTT = (\alpha * SRTT) + ((1 - \alpha) * RTT)$
	  RTT = estimate of current round trip time for each connection
	  SRTT = smoothed round trip time, minimising effects
	  $\alpha$ = the smoothing factor (1 when the new value of RTT is ignored)'
- SRTT estimates the average round trip time

#### TCP/IP Congestion Control
- TCP attempts to avoid congestion collapse by using end to end packet loss as a measure of congestion
	- TCP receiver *fills* the Window field of an ACK header to report how much additional buffer space is available for further data
	- When a message is lost, the TCP sender could naively retransmit, instead it commences by sending a single packet, if ACK, then it transmits two, then four, etc... 
	- TCP/IP responds to congestion by backing off quickly and avoids further congestion by slowly increasing offered traffic

#### Network Application Program Interfaces (APIs)
- Calls to Unix `open()` which can then be `read()` and `write()`
- It is preferable if the API to network I/O exhibit the same semantics as file or stream, however this is difficult:
	- client-server asymmetry
	- network connections may be connection oriented or connectionless
	- Identification is more important to network than for file operations
	- Many I/O models presume continuous data stream

#### Berkeley Sockets (a network API)
- Consists of 3 parts:
	- Socket layer provides the interface between user programs and networking
	- Protocol layer supports different protocols in use (TCP/IP, etc.)
	- The device driver supports physical devices (ethernet controllers, etc.)


# Client-Server 
#### Client/Server Software Architectures
- Client/server computing takes this a step farther by recognizing that those modules need not all be executed within the same memory space
- The calling module becomes the client (that which requests a service) and the called module becomes the server

#### Partitioning Client/Server Responsibilities
- We must address a number of issues:
	- Is there a functional partition at all?
	- Is there a data-driven partition?
	- Is there an extensive use of global variables?
	- Are there any hidden intra-application communication mechanisms (vars, excepts, or signals)?

#### Two Tier and Three Tier Architecture
- Two tier is one where a client talks directly to a server, typically used in small environments (<50)
- Three tier introduces another server (agent) between the clients and the traditional service, providing various services (vertical scaling)

#### Concurrency in Servers
- Concurrency is derived from using a non-queuing model of execution, either by using a copy of the server to support each client, or to provide faster response to each client
- Clients leave their concurrency to the OS
- Concurrent servers are multiple simultaneous requests, iterative is one at a time

#### The Internet Supervisor Daemon - `inetd`
- One problem with having many internetworking services supported, each OS host requires many daemons just waiting for incoming connections on their reserved port, consuming memory and a process slot
- Solution is a 'super daemon' listening for incoming connections on many ports

# Architecture Independent Applications
#### Automated Development of Distributed Applications
The complications of layering in the OSI model come to a head in the Session Layer and a number of recent developments have 'bypassed' many of the OSI layers
These have been motivated by:
- Speed
- Distributed and replicated file systems
- Remote process invocation and control
- Network aware programming languages such as Java
- Increased need for distributed security

#### Remote Procedure Call (RPC) Paradigm
Based on the observation that procedure calls are a well understood mechanism for control transfer. The proposal is that procedure calls may be consistently extended to access remote environments (other machines).
When a remote procedure call is invoked:
- The calling environment is suspended
- Any parameters are passed across the network to the remote environment
- Results are marshalled back to the caller and its execution resumes

#### RPC Execution Order
1. The client calls a local procedure (*client stub*), which appears to the client that the stub is an actual procedure, the purpose is to package arguments to the remote procedure
2. The network messages are sent to the local kernel using a sys call
3. The network messages are then sent to a remote kernel 
4. The *server stub* has been waiting on any client's request, unmarshalling the arguments from the network messages and converts them to its format
5. The SS then executes a local procedure call 
6. When the procedure finishes, it returns to the SS
7. The SS then converts the return values if necessary and builds one or more network messages
8. Messages traverse network
9. The CS reads the replies from the local kernel
10. The CS returns to the calling procedure, control flow is again in the clients code

#### SUN Microsystem's RPC Compiler `rpcgen`
- Many OS's provide RPC within their kernels and as a standard library of routines
- SUN's RPC package consists of `rpcgen` a compiler for creating remote procedure call server and client stubs, the XDR for encoding data into a portable manner

#### Naming and Interface Binding
- Most OSs now supporting RPCs use a replicated database used to store server addresses
- When a server restarts (boots) it informs the database that it is alive and passes the programs number, version and port number

# Security of TCP/IP
The 4 layers of the TCP/IP suite, has multiple potential vulnerabilities:
- **Application Layer**: such as FTP, HTTP and SMTP run on machines to which attackers may not otherwise have physical access. Each application service may need to authenticate its remote client, and may use local OS authentication to perform this. Individual applications offering the networked services are themselves also vulnerable
- **Transport Layer**: primarily provided by the reliable, streaming transport control protocol (TCP) and user datagram protocol (UDP) meet the data delivery requirements of most internet applications, however, apps and OSs expect the protocol to perform in certain ways, so incorrect interpretation of protocol, or attacks makes them not work as expected or at all. 
- **Internet Layer**: consists of the Internet Protocol (IP) and Internet Control Message Protocol (ICMP) provide the actual routed delivery of messages between source and destination. IPv4 is particularly vulnerable to attack and may be exploited to not deliver messages, or deliver to the wrong destination, etc. 
- **Physical Layer**: are not strictly part of the TCP/IP suite, but define how packets or frames are received via hardware and provided to the IP layer above. By its nature, interface hardware must see all packets destined for the interface. 

### Packet Sniffing
- Most computer networks consist of many personal computers or workstations connected via a shared LAN or WLAN segments. To capture the information traversing the network is termed sniffing. LAN topology, specifically Ethernet, works by transmitting addressed packets via shared cable. 
- Two main problems with Ethernet's approach:
	- Most Ethernet NICs (network interface card) can be placed in promiscuous mode, which results in all observed packets being sent to the OS
	- Most Ethernet NICs permit their NIC address to be modified, so one Ethernet NIC could be given the MAC address of another
- A variety of hardware and software tools are termed packet sniffers:
	- Packet sniffer denotes any hardware or software tool that can capture packets from a network
	- Network analysers are tools that monitor network traffic and devices with the goal of alerting the network manager of problems
	- Protocol analysers are tools that capture network packets, providing some level of formatting for those packets, allowing the user to analyse/visualise packets post-hoc
- Typical uses of such programs:
	- Automatic sifting of clear-text passwords and usernames
	- Conversion of data to human readable format so that people can read the traffic
	- Fault analysis to discover problems in the network
	- Network intrusion detection
	- Network traffic logging

### TCP/IP Port Scanning
- An attacker tries to identify which services are supported from a potential target host. 
- Can connect to an open port.

### Stealth Port Scanning
- Involves searching for open ports, but without actually creating a connection, nothing is logged by half-open scanning. 

### IP Spoofing
- Allows an intruder on the internet to effectively impersonate a local system's IP address. 
- Create and send malformed IP packets.

### UDP Packet Spoofing
- UDP is a lightweight protocol built on IP. An attacker may attack a UDP service because of these properties - the attacker is unconcerned about reply packets. 

### DoS Attacks
- Using source address spoofing to send thousands of packets to a target system, characterised by attackers' explicit attempt to prevent or delay legitimate users from using a service
#### Smurf DDoS Attack
- The attacker provides a spoofed source address, when sending an ICMP echo, or ping, to an IP broadcast address as the destination.

### Security at Network Boundaries
- The greatest opportunity is provided to an attacker who connects to the LAN from the wider internet.
- Attacks from the internet can attempt to bypass the user or system-level security of a single machine, or possibly undertake a DoS attack on the LAN itself. 
- Specifically we should:
	- Control network traffic based on both senders' and receivers' network IP address
	- Control network traffic based on requested services (IP Ports)
	- Not expose our LAN topology to the wider-internet, hiding hostnames, addresses and available services
	- Constrain some network traffic based on its content
	- Only permit internal access from remote users and services, based on their verified identities and possibly location
	- Log all internet connections, attempts and traffic

### Packet Filtering at Network Boundaries
- *Firewall* describes any network device, appliance or specially configured computer which protects the boundary of an internal network. 
- A firewall may be:
	- part of a traditional single workstation protecting itself
	- a computer or device protecting several other workstations
	- a dedicated device doing nothing else but protecting other hosts

#### Possible Packet Filtering Criteria
- By examining the headers of TCP/IP traffic, we can detect obviously falsified traffic:
	- filter on each IP packet's source address
		- i.e. a packet arriving outside out internal network and announce their source address as being internal, has probably spoofed source addresses
	- filter on each IP packet's destination address
	- filter based in specific low level routing or transport protocols
	- filter based on application protocols
		- i.e. letting HTTP and FTP requests leave, but not NFS to enter
	- filter based on recent activity

### Developing a Firewall Policy
- Simplifies and provides a consistent and consistently applied practice deciding what traffic to permit and what to filter

### `iptables`
- State-of-the-art in programmable firewall software, provides stateful control over network traffic
- Consists of two software components:
	- `iptables` application program, controlling the set of rules and policies to be enforced
	- `netfilter` software configured as part of an OS kernel to control IP traffic on several network interfaces
- Lifetime of a packet as it enters and traverses a firewall:
	- the packet could have originated on the firewall host and be destined for another host, `iptables` filters these packets before they are retransmitted
	- the packet could have originated from outside the firewall host and be destined for processes on the firewall host
	- the packet could have been originated from outside the firewall host and be destined for another host, `iptables` filters these packets as soon as the packet arrives via an incoming interface

### IP Masquerading or Network Address Translation (NAT)
- A technique employed within a firewall or border gateway to translate one set of IP address to another
- Primary motivations for NAT are:
	- your network provider may only provide you with a single IP address to use
	- it simplifies the later growth and redesign of a network
	- external attackers cannot learn the topology of your internal network unless they penetrate your firewall

### Connection Tracking
- The ability for a firewall to maintain state information about connections - source and destination IP address and port number pairs, protocol types, connection state and timeouts
- Firewalls able to do this are termed stateful

# Cryptography
### ISO/OSI Security Architecture
- Includes the requirements:
	- **Data Confidentiality** - protects data as it traverses the network from being disclosed to incorrect parties.
	- **Data Integrity** - protects the data from the modification or removal while in the network
	- **Data Origin Auth** - validates the sender of the data
	- **Data Receiver Auth** - validates the receiver of the data
	- **Peer-entity Auth** - validates all network components through which a data stream must travel
	- **Non-repudiation** - creates and verifies evidence that the claimed sender sent the data and likewise with the receiver

### Where should encryption be performed?
- Users encrypting individual files stored in a standard file-system
- File-systems encrypting all data before writing it to disk
- Datalink and network layers in switches and routers (VPNs, etc.)
- Session layer with end-to-end data conversion (SSL, etc.)
- Application layer in programs like email agents (PGP, etc.)

### Terminology
- Plain Text -> Cipher Text
- The intended receiver should be able to quickly and correctly reverse
- Following attacks are common with the goal of determining cryptographic keys:
	- known plaintext attack
	- chosen plaintext attack
	- differential analysis