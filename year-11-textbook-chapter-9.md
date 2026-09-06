# Unit 1 — Chapter 9: Network Foundations & Diagrams

This chapter introduces the fundamental concepts of network communication, physical hardware, media options, and logical network topology design. You will explore how data is packaged and sent using the Department of Defence (DoD) TCP/IP model, learn to select and justify networking hardware, examine IP addressing and subnetting, and construct professional logical diagrams using standard SCSA-compliant CISCO symbols.

These concepts represent a major theoretical and practical component of the **SCSA Computer Science ATAR syllabus** and are directly assessed in written examinations and **Assessment Task 3 (Network Topology & Theory Test)**.

---

## Lesson 9.1: DoD TCP/IP Model and Protocols

### Your Goal
Map network communications and explain how data is encapsulated and transmitted through the four layers of the DoD TCP/IP model.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.1: Characters as Binary Numbers](./year-11-textbook-chapter-1.md#lesson-11-characters-as-binary-numbers) (understanding how data is ultimately represented as bitstreams).
*   [Lesson 8.2: Good Programming Practices](./year-11-textbook-chapter-8.md#lesson-82-good-programming-practices) (understanding structural coordination).

### The Idea
When you send a message over the internet, it doesn't travel as one giant, continuous file. Instead, it is broken down, packaged, addressed, and sent across physical cables or wireless waves. To manage this complex process, computer scientists use a layered model.

**The Analogy:**
Imagine you want to send a physical letter from Perth to a friend in Albany:
1.  **Application Layer:** You write the letter (the raw message) in a language your friend understands.
2.  **Transport Layer:** You put the letter in an envelope, sealing it to ensure it arrives intact, and write sequence numbers if it spans multiple pages.
3.  **Internet Layer:** You write the sender and receiver mailing addresses clearly on the outside of the envelope.
4.  **Network Access Layer:** The envelope is put onto a physical mail truck or plane and transported over roads and tracks as physical signals.

The internet uses the **Department of Defence (DoD) TCP/IP model**, which consists of four distinct layers working from top to bottom:

```
[ Application Layer ]  <-- HTTP, HTTPS, FTP, SMTP, DNS
         │
         ▼
[ Transport Layer ]    <-- TCP (reliable, ordered) vs. UDP (fast, connectionless)
         │
         ▼
[  Internet Layer ]    <-- IP (IPv4, IPv6), routing packets
         │
         ▼
[ Network Access  ]    <-- Physical wires, fibre, Wi-Fi, Ethernet frames
```

#### **Encapsulation and Decapsulation**
As data travels *down* the sending computer's stack, each layer adds its own control information (called a **header**). This process of wrapping data is called **Encapsulation**. When the packets arrive at the destination computer, they travel *up* the stack, and each layer strips away its corresponding header to reconstruct the original message. This is called **Decapsulation**.

#### **SCSA Key Terms**
*   **DoD TCP/IP Model:** A four-layer conceptual framework for network protocols and communication.
*   **Application Layer:** The top layer that provides network services directly to user applications (e.g., web browsers, email clients).
*   **Transport Layer:** Responsible for establishing end-to-end connections, flow control, and reliable packet delivery.
*   **Internet Layer:** Handles the addressing, packaging, and routing of packets across networks.
*   **Network Access Layer:** The bottom layer that manages the physical transmission of bits over physical media.
*   **Protocol:** A set of formal rules governing how devices exchange data over a network.
*   **Encapsulation:** The process of appending headers (and footers) to data as it moves down the network stack.

#### **Layer Protocols and Units**
Each layer has specific protocols and handles data in different units:

| Layer Number | DoD Layer Name | Core Protocols | Data Unit | Role / Description |
| :--- | :--- | :--- | :--- | :--- |
| **4** | **Application** | HTTP, HTTPS, FTP, SMTP, DNS | Data / Payload | Interacts with software (e.g. loads webpage content). |
| **3** | **Transport** | TCP, UDP | Segment | Manages ports, reliable delivery, and divides data. |
| **2** | **Internet** | IP (IPv4, IPv6) | Packet | Attaches source/destination IP addresses for routing. |
| **1** | **Network Access**| Ethernet, Wi-Fi (802.11) | Frame (Bits) | Converts logical data into physical copper, light, or radio signals. |

#### **TCP vs. UDP: The Transport Layer Duel**
The Transport layer relies on two competing protocols depending on the communication needs:
*   **Transmission Control Protocol (TCP):** Connection-oriented. It establishes a "handshake" before sending data, guarantees delivery by requesting acknowledgements, and reorders packets if they arrive out of sequence. Used for web browsing (HTTPS) and file transfers (FTP).
*   **User Datagram Protocol (UDP):** Connectionless. It sends packets ("datagrams") immediately without checking if the receiver is ready or if the packets arrive safely. It has lower overhead and is much faster. Used for video streaming and live gaming.

---

### See It Worked
#### **The Scenario**
At the **WA Junior Sports Carnival**, the timing desk official submits a 100m sprint race record of `11.45` seconds to the central web server. We need to trace how this data payload descends through the DoD TCP/IP stack on the official's laptop.

#### **The Step-by-Step Encapsulation Trace**

```
[Step 1: Application Layer] 
Payload: "Time: 11.45"
Protocol: HTTPS (Hypertext Transfer Protocol Secure)
Action: Formats the data into a secure web request.
Result: Raw Payload

          │
          ▼
[Step 2: Transport Layer]
Segment Header: Source Port: 53120, Destination Port: 443 (HTTPS), Sequence: 1
Protocol: TCP (ensures the race result is reliably delivered)
Action: Encapsulates payload with TCP port metadata.
Result: [TCP Header] + ["Time: 11.45"] (TCP Segment)

          │
          ▼
[Step 3: Internet Layer]
Packet Header: Source IP: 192.168.1.15, Destination IP: 192.168.1.100
Protocol: IP (Internet Protocol)
Action: Encapsulates the segment with logical network addresses.
Result: [IP Header] + [TCP Header] + ["Time: 11.45"] (IP Packet)

          │
          ▼
[Step 4: Network Access Layer]
Frame Header: Source MAC: 00:1A:2B:3C:4D:5E, Destination MAC: 00:1A:2B:3C:4D:9F
Protocol: Ethernet (IEEE 802.3)
Action: Wraps packet in physical MAC addresses and converts it into physical binary voltages.
Result: [Ethernet Header] + [IP Header] + [TCP Header] + ["Time: 11.45"] + [Footer] (Ethernet Frame)
```

---

### Try It with Help
#### **The Problem**
An organizer at the carnival is streaming live, real-time video commentary of the 4x100m relay back to the main display screen in the clubroom. 
1.  State which Transport layer protocol (TCP or UDP) should be selected for this task.
2.  Using the four-layer DoD TCP/IP model, describe the journey of a single video frame packet from the camera's wireless transmitter down to the physical Wi-Fi signal.

#### **Structural Hints**
*   Consider whether real-time video streaming requires error retransmission (TCP) or low latency speed (UDP). If a video frame drops, does the system wait to resend it, or just display the next live frame?
*   Trace the data packaging from Layer 4 down to Layer 1.

#### **Scaffolded Outline**
*   **Protocol Choice:** ________ (because low latency is more critical than retransmitting lost frames).
*   **Layer 4 (Application):** Encodes the raw camera stream using a protocol like RTP/HTTPS, creating the raw video data.
*   **Layer 3 (Transport):** Wraps the video data with a ________ header, appending port numbers to identify the video stream.
*   **Layer 2 (Internet):** Wraps the segment with an ________ header containing the camera's source ________ address and the clubroom screen's destination address.
*   **Layer 1 (Network Access):** Encapsulates the packet into a wireless ________ (802.11) and broadcasts it as radio frequency signals.

---

### Try It Yourself
#### **The Problem**
A student downloads a large, compressed archive file (`results.zip`) containing all historical carnival times from the school intranet. 
1.  Explain why **TCP** must be used for this file download instead of **UDP**.
2.  Describe what would happen at the destination computer's Transport layer if data packet number 3 of 10 was lost or corrupted during transmission over a noisy Wi-Fi connection.

---

### Check Your Reasoning
#### **The Answer**
1.  **Why TCP is mandatory:** Downloading a compressed ZIP archive requires 100% data integrity. A single missing bit in a compressed file will corrupt the entire archive, rendering it unreadable. TCP ensures absolute reliability through mandatory error-checking and packet retransmission. UDP is connectionless and does not guarantee delivery, making it unsuitable for file transfers.
2.  **Handling a dropped packet under TCP:**
    *   The sending computer transmits packets with sequence numbers (e.g. 1 to 10).
    *   The destination computer receives packets 1, 2, 4, and 5, identifying that packet 3 is missing.
    *   The destination's Transport layer holds the out-of-order packets (4 and 5) in a buffer and does *not* pass them to the Application layer.
    *   It sends a negative acknowledgement (or does not acknowledge packet 3), causing the sender's timer to expire.
    *   The sender retransmits packet 3.
    *   Once packet 3 arrives safely, the destination's Transport layer reassembles them in correct sequence (1, 2, 3, 4, 5...) and passes the complete data stream up to the Application layer.

#### **Common SCSA Student Errors**
*   **Confusing TCP/IP layers with the OSI model:** Writing OSI-specific layers (like Session or Presentation) instead of the four DoD TCP/IP layers. SCSA syllabus specifically specifies the **DoD TCP/IP model** for Year 11.
*   **Incorrect packet unit terminology:** Using the generic term "packet" for all layers. Remember the precise hierarchy: **Data/Payload** (Application) $ightarrow$ **Segment** (Transport) $ightarrow$ **Packet** (Internet) $ightarrow$ **Frame** (Network Access).
*   **Vague descriptions of UDP:** Describing UDP as "unreliable" in a casual way. In computer science, "unreliable" does not mean bad; it is a technical term meaning *delivery is not guaranteed*.

---

### Review and Connect
In this lesson, you explored how the DoD TCP/IP model coordinates network communication through encapsulation and protocols. On the next page, we will examine the physical hardware devices and copper/fibre cabling that operate at the Network Access layer to move these frames physically.

---

## Lesson 9.2: Physical Media & Hardware

### Your Goal
Select, compare, and justify physical transmission media and hardware components to meet specific speed, distance, and security requirements in a network layout.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 9.1: DoD TCP/IP Model and Protocols](#lesson-91-dod-tcpip-model-and-protocols) (specifically knowing that hardware operates at different layers of the model).

### The Idea
Every network requires physical components to connect devices. However, you cannot use the same wires and devices for every situation. Connecting computers within a small timing booth requires different components than connecting ovals separated by hundreds of meters.

**The Analogy:**
Think of network hardware as a city's road infrastructure:
*   **Transmission Media (Cables):** The physical roads. A local suburban road (copper UTP cable) is cheap but slow; a multi-lane highway (fibre optic) is expensive but moves massive volumes over long distances.
*   **Switch:** A local traffic roundabout that directs cars within a suburb to their specific street address.
*   **Router:** A highway exit intersection that connects different cities, guiding long-distance traffic between completely separate road networks.

#### **Physical Transmission Media**
SCSA expects you to compare three primary physical media options:

1.  **Unshielded Twisted Pair (UTP) Copper Cable:**
    *   *How it works:* Transmits electrical pulses along pairs of twisted copper wires (Ethernet).
    *   *Sizing/Limits:* Maximum length of **100 metres** before signal degradation (attenuation).
    *   *Pros/Cons:* Very cheap and easy to install, but highly vulnerable to electromagnetic interference (EMI) from power lines and lightning.
2.  **Fibre Optic Cable:**
    *   *How it works:* Transmits pulses of light through thin strands of glass.
    *   *Sizing/Limits:* Can span **kilometres** without signal loss.
    *   *Pros/Cons:* Extremely high bandwidth, completely immune to electromagnetic interference, and highly secure (cannot be easily tapped). However, it is expensive and requires specialized installation.
3.  **Wireless (Wi-Fi / 802.11):**
    *   *How it works:* Transmits data using radio frequency waves.
    *   *Sizing/Limits:* Subject to structural obstacles, weather, and physical range limits (~50m indoors).
    *   *Pros/Cons:* High convenience and mobility for user devices, but prone to signal interference, data collisions, and security risks (signals broadcast in all directions).

#### **Network Hardware Components**
To route Ethernet frames and IP packets safely, we use specialized devices:

```
                  ┌──────────────┐
                  │   Internet   │
                  └──────┬───────┘
                         │ (WAN)
                  ┌──────▼───────┐
                  │   Firewall   │ <-- Filters unauthorized external traffic
                  └──────┬───────┘
                         │
                  ┌──────▼───────┐
                  │    Router    │ <-- Connects separate IP networks (Local vs External)
                  └──────┬───────┘
                         │ (LAN)
                  ┌──────▼───────┐
                  │    Switch    │ <-- Filters and forwards frames to specific MAC addresses
                  └──┬────────┬──┘
                     │        │
           ┌─────────▼─┐    ┌─▼─────────┐
           │ Laptop A  │    │  Wireless │ <-- Broadcasts Wi-Fi to wireless clients
           └───────────┘    │  Access   │
                            │   Point   │
                            └───────────┘
```

*   **Switch (Layer 1/2):** Connects devices within a single Local Area Network (LAN). It reads incoming Ethernet frames, identifies the destination physical **MAC address**, and forwards the frame *only* to the specific port holding that device. This prevents unnecessary data collisions.
*   **Router (Layer 3):** Connects two or more separate networks (e.g., connecting a school LAN to the wide-area Internet). It reads logical **IP addresses** to determine the best path to route packets across network boundaries.
*   **Wireless Access Point (WAP):** Translates physical wired network signals into wireless radio waves, allowing mobile devices to connect to the local wired LAN.
*   **Modem:** Modulates and demodulates signals. It translates digital computer signals into analog carrier signals used by telephone lines or cable systems, bridging the home/school to the Internet Service Provider (ISP).
*   **Firewall:** A security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It establishes a barrier between a trusted internal network and untrusted external networks.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival committee needs to set up a local network. They have a timing desk laptop on the main oval, a public results display screen mounted on a scoreboard 250 metres away across an open field, and a central administration office. 

Identify the best transmission media to connect the scoreboard to the office, and justify your choice.

#### **The Solution & Justification**
*   **Selected Medium:** **Fibre Optic Cable**
*   **Justification:**
    1.  **Distance Constraint:** The distance of 250m exceeds the physical limit of Unshielded Twisted Pair (UTP) copper cable, which is strictly 100m. Using UTP would result in severe attenuation and data loss.
    2.  **Environmental Factors:** Cabling run across an open outdoor field is exposed to lightning strikes and electrical interference. Fibre optic cables transmit light rather than electrical currents, making them completely immune to electromagnetic interference (EMI).
    3.  **Performance:** Uploading real-time high-resolution scoreboard updates requires high, stable bandwidth over a dedicated line, which wireless cannot guarantee due to outdoor wind, rain, or user signal congestion.

---

### Try It with Help
#### **The Problem**
The WA Junior Sports Carnival administration tent contains three registration computers, a local results database server, and a wireless printer. All of these devices must connect together within a single Local Area Network (LAN). The tent also needs to safely connect to the external internet to upload final state qualification times.

Identify the networking hardware devices required to set up this network, and outline their specific roles.

#### **Structural Hints**
*   Which device connects local wired computers and the server together in a LAN?
*   Which device is needed to bridge the LAN to the external internet?
*   How do we secure the local database server from external internet hackers?

#### **Scaffolded Response Template**
1.  **________ (Hardware Device):** Connects the local registration computers, server, and printer within the LAN, directing data frames directly to their target MAC addresses.
2.  **________ (Hardware Device):** Connects the local LAN to the external Internet WAN, routing logical packets across the boundary.
3.  **________ (Hardware Device):** Placed between the router and the external internet to inspect incoming packets and block unauthorized access to the database server.

---

### Try It Yourself
#### **The Problem**
A school IT department is upgrading its computer science lab. The lab has 32 desktop computers, a network printer, and several student iPads. The IT technician suggests connecting all 32 desktops using high-speed Wi-Fi access points to avoid running cables. 

Critique the technician's suggestion. Discuss the trade-offs of using Wireless (Wi-Fi) versus physical UTP cabling for a classroom lab containing 32 active computers.

---

### Check Your Reasoning
#### **The Answer**
The technician's suggestion of using a purely wireless network for 32 active desktop computers is suboptimal for a high-density computer lab.

**Trade-offs Analysis:**
*   **Bandwidth & Performance (Cabling Wins):** Physical UTP cabling provides dedicated, full-duplex bandwidth (typically 1 Gbps) to every single computer. In contrast, Wi-Fi is a shared medium. With 32 active computers transmitting simultaneously, data collisions will spike, reducing throughput.
*   **Reliability & Interference (Cabling Wins):** Classrooms contain physical obstructions, and wireless signals are prone to interference from neighboring networks, fluorescent lights, and student mobile devices. Physical UTP copper cables are insulated and provide a stable, interference-free connection.
*   **Mobility & Cost (Wireless Wins):** Wi-Fi avoids the material and installation cost of running 32 physical cables and allows students to move around with iPads.
*   **Recommendation:** Use physical **UTP Copper Cabling** to connect the 32 stationary desktop computers to a central **Switch** to ensure stable, high-speed performance, while installing a single **Wireless Access Point (WAP)** solely to accommodate mobile student iPads.

#### **Common SCSA Student Errors**
*   **Confusing a Hub with a Switch:** Stating that a switch broadcasts data to all ports. *Hubs* broadcast to all ports (obsolete, highly inefficient); *Switches* read MAC addresses and send data *only* to the intended device.
*   **Vague Distance Limitations:** Stating that UTP has a "short" range. Students must state the exact SCSA standard limit: **100 metres**.
*   **Assuming Fibre is always better:** Recommending fibre optic cable to connect desktop computers inside a single classroom. While fast, fibre is expensive, delicate, and completely unnecessary for short-distance desk connections.

---

### Review and Connect
In this lesson, you analyzed how physical media and hardware components establish Local Area Networks. On the next page, we will learn how logical **IP addresses** are allocated across these networks and how **subnet masks** are used to partition devices.

---

## Lesson 9.3: IP Addressing, Subnetting & Performance

### Your Goal
Analyze IP address structures, differentiate between IPv4 and IPv6, calculate subnet ranges, and diagnose factors that degrade network performance.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 1.2: Hexadecimal and Decimal Conversions](./year-11-textbook-chapter-1.md#lesson-12-hexadecimal-and-decimal-conversions) (since IPv6 relies heavily on hexadecimal notation).
*   [Lesson 5.1: Arithmetic Operators and MOD](./year-11-textbook-chapter-5.md#lesson-51-arithmetic-operators-and-mod).

### The Idea
Every device on a network must have a unique identifier so that data packets can be sent to the correct destination. This is the role of the **Internet Protocol (IP) Address**. 

**The Analogy:**
Think of a large school campus like *Westlake College*:
*   The street address is *100 Westlake Road*. Every classroom shares this parent address.
*   Each specific classroom has a room number: *Room 12, Room 13, Room 14*.
*   If we send mail, we use the school address to get it to the front gate, and then a "subnet mask" (the classroom number) to find the exact room.

#### **IP Version Comparison (IPv4 vs. IPv6)**
As the number of internet-connected devices has exploded globally, the original addressing system ran out of unique combinations, leading to a modern replacement standard:

| Feature | IPv4 (Internet Protocol Version 4) | IPv6 (Internet Protocol Version 6) |
| :--- | :--- | :--- |
| **Address Size** | 32-bit | 128-bit |
| **Notation Format** | Dotted Decimal (e.g. `192.168.1.15`) | Hexadecimal Colons (e.g. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`) |
| **Number of Addresses**| ~4.3 Billion ($2^{32}$) | ~340 Undecillion ($2^{128}$) |
| **Address Example** | 4 octets separated by dots | 8 groups of 4 hex digits separated by colons |

#### **The Role of Subnet Masks**
An IP address is split into two logical parts: the **Network ID** (the neighborhood) and the **Host ID** (the specific house). A **Subnet Mask** is a 32-bit binary number that tells the router exactly where the Network ID ends and the Host ID begins.

In a standard small local network, we use a subnet mask of `255.255.255.0` (also written as `/24` in CIDR notation). 
*   If a computer has the IP `192.168.1.15` and a subnet mask of `255.255.255.0`, the network portion is `192.168.1.x`, and the host portion is `.15`.
*   Any device with an IP starting with `192.168.1.x` can communicate directly without going through a router, because they share the same subnet.

#### **Factors Degrading Network Performance**
When designing networks, developers must minimize performance bottlenecks. SCSA highlights four key factors:
1.  **Bandwidth Limits:** The maximum rate at which data can be transferred over a link (measured in bps, Mbps, Gbps). A 100 Mbps copper link will choke if trying to move 1 Gbps of concurrent traffic.
2.  **Poor Network Design (Collision Domains):** If too many devices are connected to a single broadcast segment (e.g., using old hubs instead of switches), packets will collide in transit and must be retransmitted, slowing down the entire network.
3.  **Excessive Broadcast Traffic:** Some network services broadcast packets to *every* device on the network (e.g., discovery requests). If a single subnet contains thousands of devices, "broadcast storms" will consume all available bandwidth.
4.  **Data Collisions:** Occur when two wireless devices transmit on the same frequency channel at the exact same instant, corrupting both signals.

---

### See It Worked
#### **The Scenario**
At the **WA Junior Sports Carnival**, the IT coordinator configures three laptops on the ovals with the following IP credentials:
*   **Laptop A:** IP `192.168.1.10`, Subnet Mask `255.255.255.0`
*   **Laptop B:** IP `192.168.1.25`, Subnet Mask `255.255.255.0`
*   **Laptop C:** IP `192.168.2.50`, Subnet Mask `255.255.255.0`

Identify which laptops can communicate directly without a router, and calculate the maximum number of unique host addresses available on Subnet 1.

#### **The Solution & Calculation**
1.  **Direct Communication Check:**
    *   Laptop A and Laptop B can communicate directly. Under the `255.255.255.0` mask, the first three octets represent the network. Both laptops have the Network ID `192.168.1.x`.
    *   Laptop C has the Network ID `192.168.2.x`. Because its network ID is different, Laptop C *cannot* communicate with A or B directly. Packets must be sent through a Layer 3 Router to cross the network boundary.
2.  **Host Address Range Calculation:**
    *   A class-based `/24` subnet mask leaves the final octet (8 bits) for host addresses.
    *   $2^8 = 256$ total binary combinations.
    *   However, we must subtract **two special reserved addresses** in every subnet:
        *   The **Network Address** (used to identify the network itself): `.0` (`192.168.1.0`)
        *   The **Broadcast Address** (used to send packets to all hosts on the subnet): `.255` (`192.168.1.255`)
    *   **Maximum Available Hosts:** $256 - 2 = 254$ assignable host IPs (ranging from `.1` to `.254`).

---

### Try It with Help
#### **The Problem**
The timing coordinator at the track wants to set up a small local network for the stopwatch timers. They assign IP addresses to the ovals. 
*   **Stopwatch Laptop 1:** IP `10.0.0.5`, Subnet Mask `255.0.0.0`
*   **Stopwatch Laptop 2:** IP `10.0.10.20`, Subnet Mask `255.0.0.0`
*   **Display Screen:** IP `10.1.5.80`, Subnet Mask `255.0.0.0`

Determine if all three devices can communicate directly on the same subnet, and explain how the `255.0.0.0` subnet mask dictates this evaluation.

#### **Structural Hints**
*   Look at the subnet mask `255.0.0.0`. It only has `255` in the *first* octet.
*   This means only the first number of the IP address (e.g. `10.x.x.x`) represents the network ID.
*   Compare the first octets of all three devices.

#### **Scaffolded Response Template**
*   The subnet mask `255.0.0.0` indicates that only the ________ (first / second / third) octet represents the network ID.
*   Therefore, the network address for all three devices is **`10.0.0.0`**.
*   Comparing the first octets:
    *   Stopwatch Laptop 1 begins with `10`.
    *   Stopwatch Laptop 2 begins with `10`.
    *   Display Screen begins with `10`.
*   Because all three devices share the same network ID octet, they ________ (can / cannot) communicate directly without a router.

---

### Try It Yourself
#### **The Problem**
A local business network with 500 computers is suffering from severe network slowdowns. The network is configured as a single massive subnet with an IP range of `172.16.0.1` to `172.16.3.254` and a subnet mask of `255.255.252.0` (which groups all 500 computers into one broadcast domain). 

1.  Identify the performance degradation factor responsible for this slowdown.
2.  Propose a structural network design change to resolve this issue and restore network performance.

---

### Check Your Reasoning
#### **The Answer**
1.  **Performance Degradation Factor:** The issue is caused by **excessive broadcast traffic** within a single, large broadcast domain. Devices on a local network frequently broadcast packets (such as ARP requests and NetBIOS announcements) to all other hosts. With 500 active computers in one broadcast domain, the volume of broadcast traffic becomes overwhelming, consuming CPU cycles on every single device and saturating the physical bandwidth.
2.  **Proposed Solution:** Implement **Subnetting (Segmentation)**. Split the single large network into smaller, isolated logical subnets (e.g., four subnets of 125 computers each, using subnet masks of `255.255.255.128` or `/25`). Install a **Layer 3 Router** or a Layer 3 Switch to route traffic between these subnets. This design confines broadcast traffic within each small subnet, preventing broadcast storms from flooding the entire physical infrastructure.

#### **Common SCSA Student Errors**
*   **Forgetting to Subtract Reserved Addresses:** Calculating available hosts as $2^n$ rather than $2^n - 2$. SCSA marking keys always subtract 2 for the Network and Broadcast addresses.
*   **Vague Subnet Descriptions:** Stating that a subnet "makes the internet faster." Subnets do not change the speed of external internet connections; they optimize local network traffic flow.
*   **Confusing IPv4 and IPv6 Bit sizes:** Reversing the bit allocations (e.g., stating IPv4 is 64-bit and IPv6 is 128-bit). Memorize the exact sizes: **IPv4 is 32-bit; IPv6 is 128-bit**.

---

### Review and Connect
In this lesson, you calculated logical subnet boundaries and diagnosed network congestion bottlenecks. On the next page, we will learn how to visually document these physical and logical connections using standardized **CISCO network diagram conventions**—a highly assessed skill in ATAR written exams.

---

## Lesson 9.4: CISCO Network Diagrams

### Your Goal
Create and interpret logical network diagrams representing LAN, WLAN, and WAN configurations using SCSA-compliant CISCO network diagrammatic conventions.

### Before You Start
Ensure you are comfortable with:
*   [Lesson 9.2: Physical Media & Hardware](#lesson-92-physical-media--hardware) (knowing the roles of routers, switches, WAPs, and firewalls).

### The Idea
Before an IT technician can wire a school network, they must have a logical blueprint. In computer science, we use a standardized language of symbols established by CISCO. These symbols allow any engineer or student in Western Australia to understand a network layout at a glance.

#### **SCSA-Compliant CISCO Symbols**
You must memorize and draw these specific symbols in your exams:

```
┌────────────────────────────────────────────────────────┐
│               SCSA CISCO DIAGRAM SYMBOLS               │
├───────────────────┬────────────────────────────────────┤
│ Device Type       │ Written Diagram Representation     │
├───────────────────┼────────────────────────────────────┤
│ Router            │ Circle with two horizontal arrows  │
│                   │ crossing inside: ( ──► )           │
│                   │                  ( ◄── )           │
├───────────────────┼────────────────────────────────────┤
│ Switch            │ Square or 3D block with flat,      │
│                   │ parallel arrows on the front: [ ⇄ ]│
├───────────────────┼────────────────────────────────────┤
│ Firewall          │ A brick wall or rectangle with     │
│                   │ brick patterns: [🧱🧱]              │
├───────────────────┼────────────────────────────────────┤
│ Wireless Access   │ Circle or box with two antenna      │
│ Point (WAP)       │ radiating waves outwards: (( 📡 )) │
├───────────────────┼────────────────────────────────────┤
│ Host / Workstation│ Standard desktop computer/monitor  │
│                   │ or laptop symbol: [🖥️]              │
├───────────────────┼────────────────────────────────────┤
│ WAN / Internet    │ A cloud symbol: ( Cloud )          │
└───────────────────┴────────────────────────────────────┘
```

#### **Line Representation Conventions**
*   **Wired Connections (UTP/Fibre):** Represented by **solid, continuous black lines**.
*   **Wireless Connections (Wi-Fi):** Represented by **dashed or dotted lines** linking hosts to the Wireless Access Point.

#### **Key Diagram Design Rules**
1.  **Never connect hosts directly to a Router:** In a Local Area Network, all local workstations and servers must connect to a central **Switch** first. The Switch is then linked to the Router.
2.  **Firewall Placement:** The Firewall must sit directly on the boundary line between the trusted local router and the untrusted external WAN (Internet) cloud.
3.  **Label Everything:** Every device, interface, and subnet boundary must be clearly labeled (e.g., Subnet 1: `192.168.1.0/24`) to show logical divisions.

---

### See It Worked
#### **The Scenario**
The WA Junior Sports Carnival timing committee wants a logical network diagram. 
The specifications are:
1.  A central server room containing the **Results Server** and a local **Wired Admin Desktop**.
2.  Both of these devices connect to a central **Wired Switch**.
3.  A **Wireless Access Point (WAP)** connected to the Switch to allow mobile timing laptops on the field to submit times.
4.  The Switch connects to a **Router** to allow communication outside the field.
5.  An external **Firewall** sits between the Router and the **Internet WAN Cloud**.

#### **The SCSA-Standard Logical Layout**

```
               ( WAN / Internet Cloud )
                          │
                  [🧱 Firewall 🧱]
                          │
                  ( ◄── Router ──► )
                          │
                      [ Switch ]
                     /    │                         /     │             [ Server ]──┘      │       └──[(( WAP ))]
                          │             :  : (Wireless link)
                   [🖥️ Admin PC]         :  :
                                         :  └ - - [🖥️ Timing Laptop 1]
                                         :
                                         └ - - - [🖥️ Timing Laptop 2]
```

#### **Why this design is correct:**
*   The **Firewall** is correctly positioned on the perimeter line protecting the local router and internal network from the external WAN cloud.
*   All local hosts (Server, Admin PC, and WAP) connect directly to the central **Switch** via solid lines, rather than directly to the router, establishing a single LAN.
*   The **Timing Laptops** connect to the WAP using dashed lines, representing physical wireless boundaries.

---

### Try It with Help
#### **The Problem**
Draw a logical CISCO network diagram based on the following school library specification:
1.  The library contains three public student research computers (PC1, PC2, PC3).
2.  The library has a local network storage server (Library Server).
3.  These local devices connect to a central local Switch.
4.  The Switch is connected to a local Wireless Access Point, allowing student mobile phones to access library resources.
5.  The Switch connects to the school's central Router.

#### **Structural Hints**
*   Draft the central Switch first.
*   Draw lines from PC1, PC2, PC3, the Library Server, and the WAP to that central Switch.
*   Draw a dashed line from a student mobile phone host to the WAP.
*   Draw a line from the Switch to the Router. 
*   *Note:* There is no external internet connection or firewall specified in this local intranet request.

#### **Visual Assembly Guidance**
*   Place the **Router** at the top.
*   Place the **Switch** in the middle.
*   Connect the **Router** to the **Switch** with a solid line.
*   Branch PC1, PC2, PC3, and the **Library Server** off the **Switch** using solid lines.
*   Connect the **WAP** to the **Switch** using a solid line.
*   Draw a dashed line from a **Phone [🖥️]** to the **WAP**.

---

### Try It Yourself
#### **The Problem**
A local athletics club is building a permanent administration office. They require a network layout that meets these constraints:
1.  An internal office subnet containing 4 wired computers connected to an office switch.
2.  An external timing booth subnet containing 2 wired timing laptops connected to a timing booth switch located 90 meters away.
3.  Both switches must link to a central dual-port router.
4.  The router must connect to the internet through a dedicated physical firewall.

Draw a complete, logical SCSA-standard CISCO network diagram representing this dual-subnet topology. Ensure you label each subnet boundary clearly.

---

### Check Your Reasoning
#### **The Answer**

```
                     ( WAN / Internet Cloud )
                                │
                        [🧱 Firewall 🧱]
                                │
                   ┌────( ◄── Router ──► )────┐
                   │ (Port 1)                 │ (Port 2)
                   │                          │
            [ Office Switch ]           [ Timing Switch ]
             /   │     │   \                 /                     /    │     │    \               /                    [🖥️]  [🖥️]  [🖥️]  [🖥️]           [🖥️]         [🖥️]
         PC1   PC2   PC3   PC4          Laptop 1    Laptop 2

   └───────── Subnet 1 ─────────┘     └───────── Subnet 2 ─────────┘
        (e.g., 192.168.1.0/24)             (e.g., 192.168.2.0/24)
```

#### **Design Scorecard (SCSA Marking Standards)**
*   **Dual-Port Router (1 Mark):** The router correctly splits the system into two distinct logical subnets.
*   **Wired Switch Layout (1 Mark):** All workstations connect to switches, *never* directly to router interfaces.
*   **Firewall Perimeter (1 Mark):** The firewall is correctly placed outside the router, filtering the WAN boundary line.
*   **SCSA Labeling (1 Mark):** Subnet boundaries (Subnet 1 and Subnet 2) are explicitly outlined and labeled.
*   **Cable Solid Lines (1 Mark):** All connections are drawn as solid lines since all devices are wired.

#### **Common SCSA Student Errors**
*   **Forgetting the Switch:** Directly connecting host PCs to the ports of a Router. Routers have limited physical ports and operate at Layer 3; they are designed to route *between* subnets, not connect individual local workstations.
*   **Misplacing the Firewall:** Putting the firewall between a Switch and local hosts. Firewalls should protect the entire local network, which means placing them at the outermost border between the Router and the Internet WAN.
*   **Incorrect Symbols:** Using standard generic squares for routers. SCSA examinations explicitly state that students must use standard CISCO symbols (circles with arrows for routers, switches with overlapping flat arrows).

---

## Teacher Support Module

### **SCSA Syllabus Mapping**
*   **Unit 1.2 (Networking)**: DoD TCP/IP model, layers, protocols (HTTP, HTTPS, FTP, SMTP, TCP, UDP, IP).
*   **Unit 1.2 (Hardware/Media)**: Function of hardware (router, switch, WAP, modem, firewall); Media (UTP, fibre, wireless).
*   **Unit 1.2 (Addressing/Performance)**: IP addressing, subnet masks, IPv4 vs IPv6; performance factors (bandwidth, collisions, excess broadcasts).
*   **Unit 1.2 (Diagrams)**: Creating logical network diagrams using SCSA CISCO diagram conventions.

### **Diagnostic Prerequisite Check**
Before starting this chapter, ensure students have completed:
*   **Lesson 1.1 (Characters as Binary Numbers):** Students must understand that computer networking ultimately converts high-level application data into physical copper voltages or fiber light pulses.

### **Misconception Busters**
1.  **"IP Addresses and MAC Addresses are the same thing"**
    *   *The Reality:* A MAC Address is a physical, 48-bit address burned permanently into a network card (NIC) at the factory; it never changes and is used for local delivery (Layer 2). An IP Address is a logical, 32-bit (IPv4) or 128-bit (IPv6) address assigned by a network administrator to route packets between different networks (Layer 3).
2.  **"A Switch and a Router do the same job"**
    *   *The Reality:* A Switch connects devices *within* the same network (LAN) using MAC addresses. A Router connects *completely different* networks together using IP addresses.
3.  **"Fibre optic cables are fast because they use glass"**
    *   *The Reality:* Fibre is fast because it transmits pulses of light (photons) which travel at the speed of light through glass, experiencing zero electromagnetic interference and allowing extremely high-frequency data modulation over massive distances.

### **SCSA Exam Practice Task (Classroom Assessment)**
**Task Type:** Theory Test Question (8 Marks)
*Scenario:* A regional sports park requires a local wireless network for the public scoreboard and registration. The registration desks (3 desktops) are located inside an office. The scoreboard is mounted on a metal pole 120m away outdoors. The internet connection enters the office via a modem.
1.  Select and justify the physical transmission media to connect the scoreboard to the office switch. (3 Marks)
2.  Sketch a logical CISCO network diagram containing the registration desktops, switch, WAP, router, firewall, and WAN cloud. (5 Marks)

---
