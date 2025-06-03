- [5. 📘 Transmission Control Protocol/Internet Protocol (TCP/IP) Protocol Suite](#5--transmission-control-protocolinternet-protocol-tcpip-protocol-suite)
	- [Layers of TCP/IP Model](#layers-of-tcpip-model)
	- [🟢 Advantages of TCP/IP Model](#-advantages-of-tcpip-model)
	- [🔴 Disadvantages of TCP/IP Model](#-disadvantages-of-tcpip-model)
	- [📦 Data Packets: The Units of Communication](#-data-packets-the-units-of-communication)

---

## 5. 📘 Transmission Control Protocol/Internet Protocol (TCP/IP) Protocol Suite

- Created by the U.S. Department of Defense (1970s).
- TCP/IP is the foundation of the internet and enables devices to communicate with each other using a common language.
- It is a set of conventions or rules and methods that enables devices to communicate over networks: this messages = packages sent across the internet.
- The main condition of combo of protocols is to make data reliable and accurate so that the receiver will receive the same information which is sent by the sender. To ensure that, each message reaches its final destination accurately, the TCP/IP model divides its data into packets and combines them at the other end, which helps in maintaining the accuracy of the data while transferring from one end to another end.

### Layers of TCP/IP Model

- Divided into **4 layers** (simpler than the 7-layer OSI model):

1️⃣ Application Layer → HTTP, FTP, SMTP, DNS  


- The closest to the end user and is where applications and user interfaces reside.
- Key responsibilities:
	- Supports application protocols like HTTP, FTP, SMTP, DNS, etc.
		- These are a number of application protocols used to provide services to end-users: HTTP (Hypertext Transfer Protocol) for web browsing, FTP (File Transfer Protocol) for file transfer, and SMTP (Simple Mail Transfer Protocol) for email.
	- Enables communication between software applications across networks.
	- Handles data formatting, encryption, and session management.


2️⃣ Transport Layer → TCP (reliable), UDP (fast but unreliable)  
- It is responsible for the reliability, flow control, segmentation/reassembly and correction of data that is being sent over the network.  
- This layer is comprise of 2 protocols: TCP and UDP. TCP is used for reliable data transmission, while UDP is used for fast transmission of data that can tolerate some packet loss (because it does not check or waits for confirmation of reception, if something gets lost...UDP does not care or knows).
- TCP guarantees the integrity of the data being communicated over a network. Before it transmits data, TCP establishes a connection between a source and its destination, which remains active until communication begins. It then breaks large amounts of data into smaller packets, while ensuring end-to-end delivery without loss of any data.

3️⃣ Internet Layer → IP (addressing, routing) and the Address Resolution Protocol (ARP).
- The main responsibility of this layer is to send the packets from any network, and they arrive at the goal irrespective of the route they take.
	- Determines the best path for data to travel across networks.
- Involves protocols like IP, ICMP (for diagnostics), and ARP (for address resolution).
	- IP is responsible for routing data packets between devices, while ARP is used to map IP addresses to physical addresses.
	- ARP sits between the Internet Layer and the physical/network hardware. It helps IP* find MAC addresses** on the local network, which is a Network Access Layer concern. So ARP isn’t a “transport protocol” and it isn’t directly part of the physical layer — it's a helper between layers.
> If IP is like writing the address on an envelope, and Ethernet is like handing the envelope to the courier, then: ARP is the address book that helps find the delivery person's actual location.

4️⃣ Network Access Layer → Ethernet, Wi-Fi, MAC addressing, (physical transmission)
- Its main responsibility is the transmission of information over the same network between two devices.
	- It is responsible for the physical connection between devices within the same network segment.

![TCP/IP Model](https://media.geeksforgeeks.org/wp-content/uploads/20250503155044094249/tcp_ip-1.webp)

---

### 🟢 Advantages of TCP/IP Model
- ✴️ Interoperability : this  model allows different types of computers and networks to communicate with each other, promoting compatibility and cooperation among diverse systems.
- ✴️ Scalability : TCP/IP is highly scalable, making it suitable for both small and large networks, from local area networks (LANs) to wide area networks (WANs) like the internet (in more modern complex networks, this can be more challenging)
- ✴️ Standardization : It is based on open standards; different devices and software can work together without compatibility issues.
- ✴️ Flexibility : The model supports various routing protocols, data types, and communication methods, making it adaptable to different networking needs.
- ✴️ Reliability : it includes error-checking and retransmission features that ensure reliable data transfer, even over long distances and through various network conditions.

### 🔴 Disadvantages of TCP/IP Model
- ⚠️ Security Concerns : TCP/IP was not originally designed with security in mind. While there are now many security protocols available (such as SSL/TLS), they have been added on top of the basic TCP/IP model, which can lead to vulnerabilities.
- ⚠️ Inefficiency for Small Networks : For very small networks, the overhead and complexity of the TCP/IP model may be unnecessary and inefficient compared to simpler networking protocols.
- ⚠️ Congestion: TCP/IP was not designed with congestion management in mind, which can lead to issues such as network congestion and packet loss. This can result in reduced network performance and reliability.
- ⚠️ Limited by Address Space : Although IPv6 addresses this issue, the older IPv4 system has a limited address space, which can lead to issues with address exhaustion in larger networks.
- ⚠️ Data Overhead : TCP the transport protocol, includes a significant amount of overhead to ensure reliable transmission. This can reduce efficiency, especially for small data packets or in networks where speed is crucial.

### 📦 Data Packets: The Units of Communication
When data is sent over a TCP/IP network, it is broken down into smaller, manageable units called packets.  
Each packet contains a portion of the actual data (the payload) along with control information in a header. The header includes crucial metadata like the source and destination IP addresses, sequence numbers (used by TCP), and information about the protocol being used. An optional footer might also be included for checking data integrity.  
These packets travel independently across the network and are reassembled in the correct order at the destination. Understanding packets helps in diagnosing network issues by examining the information they carry.

> Each packet contains:
> - **Header**: source/destination IPs, control info
> - **Payload**: the actual data
> - **Optional Footer**: for data integrity
> Packets are:
> - Split by **TCP**.
> - Routed by **IP**.
> - Assembled at the destination.
---

Next:
[6. 🏷️ IP Addressing](IP.md#6--ip-addressing)