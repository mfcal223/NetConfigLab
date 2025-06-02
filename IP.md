- [6. 🏷️ IP Addressing](#6-️-ip-addressing)
	- [🧮 What does the number mean?](#-what-does-the-number-mean)
	- [📉 What is IPv4 Address Depletion?](#-what-is-ipv4-address-depletion)
		- [📱 **Real-World Problem: Too Many Devices !**](#-real-world-problem-too-many-devices-)
	- [🏠 Private vs. Public IP Ranges](#-private-vs-public-ip-ranges)
	- [🌐 Classes of IP: Network and Host Portions](#-classes-of-ip-network-and-host-portions)
		- [🌐 Classful addressing](#-classful-addressing)
		- [🌐 Classless Inter Domain Routing (CIDR)](#-classless-inter-domain-routing-cidr)
	- [📐 IPV4 addressing rules focused on small-scale network configuration exercises:](#-ipv4-addressing-rules-focused-on-small-scale-network-configuration-exercises)


## 6. 🏷️ IP Addressing

*Imagine a network as a neighborhood with houses 🏠.Each house needs a unique address to receive mail or deliveries.* 
*In a network, devices (like computers, phones, etc.) also need unique addresses to communicate with each other. This unique numerical identifier assigned to each device connected to a network is the* ***IP address***.

💡 IPv4 is the most widely used system for identifying devices on a network. It uses a set of four number (32-bit integers), separated by periods (like 192.168.0.1), to give each device a unique address. 

📑 Purposes of IP address: 
- Identification: It uniquely identifies a device on a network.
- Location Addressing: It indicates where a device is located within a network, making data routing possible.

### 🧮 What does the number mean?
- An IPv4 address consists of series of four eight-bit binary numbers which are separated by decimal point.  
> 4 * 8-bit (octet) = 32 bits

> Each octet is converted to decimal and shown separated by dots (.)

![IPv4 Address Format](https://media.geeksforgeeks.org/wp-content/uploads/20241205124156693253/IPv4-address-format.webp)

- Since each octet has 8 bits, it can represent 256 numbers ranging from o to 255.  
- These four octets are represented as decimal numbers, separated by periods known as dotted decimal notation.

### 📉 What is IPv4 Address Depletion?

**We are running out of unique IPv4 addresses to assign to all the devices on the internet.**

IPv4 addresses are 32-bit numbers. That means the total possible unique addresses = 2³² = 4,294,967,296  
That seems like a lot… but:

| Subset of Addresses                                     | Reason They’re Reserved                             | Impact                               |
| ------------------------------------------------------- | --------------------------------------------------- | ------------------------------------ |
| **Private addresses** (e.g., `192.168.x.x`, `10.x.x.x`) | Used only in local networks (not globally routable) | Can’t be used on the public internet |
| **Multicast addresses**                                 | Reserved for one-to-many communication              | Not for devices                      |
| **Loopback addresses** (`127.0.0.1`)                    | For internal system testing                         | Not usable globally                  |
| **Broadcast** (`255.255.255.255`)                       | Used for sending messages to all devices            | Not assignable                       |
| **Reserved and experimental ranges**                    | Set aside for future or special use                 | Not assignable                       |

So the usable portion of those ~4.3 billion addresses is much smaller.  
  
#### 📱 **Real-World Problem: Too Many Devices !**  
The internet was originally built for computers, but now we have Phones, tablets, smart TVs, smart watches, routers, IoT devices (lightbulbs, fridges, etc.). All these devices need IP addresses, and many of them are online at once.
  
One of the strategies to delay the depletion is the implementation of ***IPv6***  
IPv6 uses 128 bits instead of 32. That means 2¹²⁸ ≈ 340 undecillion addresses 😲  
  
---
  
### 🏠 Private vs. Public IP Ranges

A **public IP** address is an IP address that can be accessed directly over the internet and is assigned to your network router by your *internet service provider (ISP)*. 
  
> A **public (or external) IP** address helps you connect to the internet from inside your network to outside your network( they are globally routable).

A **private IP** address is an address your *network router* assigns to your device. Each device within the same network is assigned a unique private IP address (sometimes called a private network address) — this is how devices on the same internal network talk to each other.

🚨 When a network is connected to the internet, it cannot use an IP address from the reserved private IP addresses.  

> The following ranges are reserved for private IP addresses (not routed over the internet):
> - 192.168.0.0 – 192.168.255.255
> - 10.0.0.0 – 10.255.255.255
> - 172.16.0.0 – 172.31.255.255

### 🌐 Classes of IP: Network and Host Portions 

For a TCP/IP wide area network (WAN) to work efficiently as a collection of networks, the routers that pass packets of data between networks don't know the exact location of a host for which a packet of information is destined.  
Routers only know what network the host is a member of and use information stored in their route table to determine how to get the packet to the destination host's network. After the packet is delivered to the destination's network, the packet is delivered to the appropriate host.

For this process to work, an IP address has two parts. The first part of an IP address is used as a network address, the last part as a host address. 
If you take the example:  
		192.168.123.132  
- 192.168.123.	or	 	192.168.123.0  >>>>>> network address  
- .132			or		0.0.0.132      >>>>>>>>>>>> host address  

#### 🌐 Classful addressing
  
In early networking, this division was not fixed. The temporal solution to help simplify complex subnetting schemes that require sophisticated network management tools was organised IP addresses in classes based on network size. This method faced limitations in flexibility and efficient use of address space.  

The IP addresses were organised in 5 classes:  
  
| Class		| IP address | 	Network ID | Host ID |
|-----------|------------|-------------|---------|
| Class	A	| a.b.c.d	 |		a	   |  b.c.d	 |
| Class	B	| a.b.c.d	 | 		a.b	   | 	c.d	 |
| Class	C	| a.b.c.d	 | 	  a.b.c	   | 	d	 |
| Class	D	| a.b.c.d	 | 	Multicast purpouses  |
| Class	E	| a.b.c.d	 | 	Experimental Use     |

![Classes of IP](https://www.tech-faq.com/wp-content/uploads/IP-Address-Classes.jpg)

> **The problem with this classful addressing method is that millions of class A addresses are wasted, many of the class B addresses are wasted, whereas, the number of addresses available in class C is so small that it cannot cater to the needs of organizations.**

Since there are these problems, Classful networking was replaced by **Classless Inter-Domain Routing (CIDR)** in 1993.

#### 🌐 Classless Inter Domain Routing (CIDR)

Classless Inter-Domain Routing (CIDR) is a method of IP address allocation and IP routing that allows for more efficient use of IP addresses. CIDR is based on the idea that IP addresses can be allocated and routed based on their network-prefix rather than their class, which was the traditional way of IP address allocation.

CIDR addresses are represented using a slash notation, which specifies the number of bits in the network-prefix. 

> This / notation goes after the IP address (after, like a suffix). In this particular case, the word "prefix" refers to the fact that the network part of the IP goes before the host portion of the

For example, an IP address of 192.168.1.0 with a prefix length of 24 would be represented as: 
**192.168.1.0/24**.  
This notation indicates that the first 24 bits of the IP address are the network prefix and the remaining 8 bits are the host identifier. 
You can assume then that:  
		-  The network ID is 24 bits long.  
		-  The host ID is 8 bits long.  
		-  2^21 = 2097152 network address.  
		-  2^8 - 2 = 254 host address.  

> CIDR allows any prefix length between /0 and /32.  
`/24` is just very common, especially in local networks.

> /25 = 128 IPs = 50% of total range (256 possibilities per byte)

🛜 **CIDR Block Reminders**
| CIDR  | Usable IPs | Use Case                |
| ----- | ---------- | ----------------------- |
| `/30` | 2          | Point-to-point link     |
| `/29` | 6          | Small subnet            |
| `/24` | 254        | Home / office LAN       |
| `/16` | 65,534     | Large corporate network |
 
🛜 **Other advantages of CIDR:**
- ✴️ Efficient use of IP addresses: CIDR allows for more efficient use of IP addresses by allowing the allocation of IP addresses based on their network prefix rather than their class.
- ✴️ Flexibility: CIDR allows for more flexible IP address allocation, as it allows for the allocation of arbitrary-sized blocks of IP addresses.
- ✴️ Better routing: CIDR allows for better routing of IP traffic, as it allows routers to aggregate IP addresses based on their network prefix, reducing the size of routing tables.
- ✴️ Reduced administrative overhead: CIDR reduces administrative overhead by allowing for the allocation and routing of IP addresses in a more efficient and flexible way.
  
🔇 **Disadvantages of CIDR:**
- ⚠️ Complexity: CIDR can be more complex to implement and manage than traditional class-based addressing, which can require additional training and expertise.
- ⚠️ Compatibility issues: Some older network devices may not be compatible with CIDR, which can make it difficult to transition to a CIDR-based network.
- ⚠️ Security concerns: CIDR can make it more difficult to implement security measures such as firewall rules and access control lists, which can increase security risks.
  
### 📐 IPV4 addressing rules focused on small-scale network configuration exercises:
  
| Rule                                                                               | Why It Matters in NetPractice                                                                 |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **1. Host ID all 0s is reserved**                                                  | Represents the **network address** itself (e.g., `192.168.1.0`) — not assignable to a device. |
| **2. Host ID all 1s is reserved**                                                  | Represents the **broadcast address** (e.g., `192.168.1.255`) — not assignable to a device. .`255` = all 8 host bits = 1.  That address is reserved and cannot be assigned to a device.   |
| **3. Each device must have a unique IP. Host ID must be unique to that network.**            | No two devices on the same network can share the same address (the last bits of their IP addresses). Otherwise, there will be an address conflict   |
| **4. All devices in the same subnet must use the same subnet mask**                | Otherwise, they may interpret network boundaries differently and fail to communicate.         |
| **5. All devices must be on the same network to talk directly (without a router)** | Important for validating if two IPs should reach each other directly.                         |
| **6. Use the correct default gateway**                                             | Devices need a gateway IP that is **within their subnet** and points to the right router.     |
| **7. You must not assign an IP outside of the subnet's range**                     | NetPractice will mark this incorrect, even if the syntax is okay.                             |
| **8. Private address ranges must be used**                                         | Since it’s a local simulation, use `10.x.x.x`, `172.16.x.x – 172.31.x.x`, or `192.168.x.x`.   |
| **9. Avoid using 127.0.0.1**                                                       | This is reserved for loopback and testing the local device.                                   |
| **10. Match prefix length to address plan**                                        | Don’t just use `/24` blindly — match the prefix length to the number of hosts you need.       |
| **11. Avoid using 0.0.0.0 to denote a specific host**                            | This refers to the historical 0.0.0.0 convention. It used to mean: "this specific host" (but without an IP yet) . ⚠️ Modern routers treat it specially — but in the exercises, you just avoid it altogether.    |

> 📣 Broadcast and Network Addresses

Example: `192.168.1.0/24`
- Network Address: `192.168.1.0`
- Broadcast Address: `192.168.1.255`
- Usable: `192.168.1.1` – `192.168.1.254`

---





