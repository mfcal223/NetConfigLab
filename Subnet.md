- [7. 👺 Subnet Mask \& Subnetting: Defining Network Boundaries](#7--subnet-mask--subnetting-defining-network-boundaries)
  - [📊 Subnet Mask to CIDR Conversion Table](#-subnet-mask-to-cidr-conversion-table)
  - [🧮 Subnetting:](#-subnetting)

---

## 7. 👺 Subnet Mask & Subnetting: Defining Network Boundaries

**Subnet masks** are critical for defining the boundaries of networks and subnetworks as they are used by the TCP/IP protocol to determine whether a host is on the local subnet or on a remote network.

In TCP/IP, the parts of the IP address that are used as the network and host addresses aren't fixed. Unless you have more information, the network and host addresses above can't be determined. This information is supplied in another 32-bit number called a subnet mask.

By performing a logical `AND` operation between the IP address and the subnet mask, a device can identify the network address and thus determine if another device is on the same local network. 

Let's go through this concepts with an example:  
  
> IP address | 104.198.241.125
> Mask       | 255.255.255.128

✒️ Subnet masks are 32 bits long, just like IP addresses.  
✒️ Each `255` is 8 bits = 1 (11111111)  
✒️ `128` into binary = 10000000  

📌 255.255.255.128 = 11111111.11111111.11111111.10000000 ➡️ 25 bits set to 1  

✒️ *The same in CIDR notation is `/25`   
🔸25 network bits = 7 bits left for hosts  
🔸2^7 = 128 possible IPs (range), minus 2 for network and broadcast ➡️  126 usable addresses  

If we convert IP and mask into binary:  
  
|				|										|
|---------------|---------------------------------------|
| IP address	| 01101000.11000110.11110001.01111101	|
| Mask			| 11111111.11111111.11111111.10000000	|

To obtain the network address we need to perform a bitwise `AND` operation between IP and Mask. 

> Bitwise-AND (&): true if both bits = 1

|				|										|
|---------------|---------------------------------------|
| IP address	| 01101000.11000110.11110001.01111101	|
| Mask			| 11111111.11111111.11111111.10000000	|
|---------------|-------BITWISE-AND --------------------|
|Network address | 01101000.11000110.11110001.00000000	|

Back into decimal, the **network address** is `104.198.241.0/25`.  
  
Therefore:  
🔹 **IP Range**: 104.198.241.0 to 104.198.241.127  ➡️ 128 possibles IP
🔹 **Usable hosts ("real range")**: 104.198.241.1 to 104.198.241.126  ➡️ 126 usable addresses  
🔹 As the extremities of the range are reserved for specific uses and cannot be given to an interface:
        🔹 **Broadcast address**: 104.198.241.127  
        🔹 **Network address**: 104.198.241.0
.  

### 📊 Subnet Mask to CIDR Conversion Table
| CIDR  | Subnet Mask       | Host Bits | Usable IPs (Total IPs − 2 (network + broadcast)) | Block Size (Total IPs = 2^host bits) | Typical Use                                   |
| ----- | ----------------- | --------- | ---------- | ---------- | --------------------------------------------- |
| `/30` | `255.255.255.252` | 2         | 2          | 4          | Point-to-point links (e.g., router-to-router) |
| `/29` | `255.255.255.248` | 3         | 6          | 8          | Small subnets (few devices)                   |
| `/28` | `255.255.255.240` | 4         | 14         | 16         | Very small LANs                               |
| `/27` | `255.255.255.224` | 5         | 30         | 32         | Small LANs                                    |
| `/26` | `255.255.255.192` | 6         | 62         | 64         | Medium LANs                                   |
| `/25` | `255.255.255.128` | 7         | 126        | 128        | Larger LANs                                   |
| `/24` | `255.255.255.0`   | 8         | 254        | 256        | Standard local networks                       |
| `/23` | `255.255.254.0`   | 9         | 510        | 512        | Joining two `/24` ranges                      |
| `/22` | `255.255.252.0`   | 10        | 1022       | 1024       | Large subnet or supernet                      |
| `/16` | `255.255.0.0`     | 16        | 65,534     | 65,536     | Large organizations                           |


---

### 🧮 Subnetting:

**Subnetting is the process of taking a larger network and dividing it into smaller, more manageable sub-networks (called subnets) by adjusting the subnet mask.**

Subnetting helps to organize devices into smaller groups, improve network performance by reducing broadcast traffic within segments, enhance security, and make network management easier.  

In the previous example, the subnet mask `255.255.255.128` (which is /25) covers the range `104.198.241.0 → 104.198.241.127`.  

🔍 **What happenes to the range `104.198.241.128 → 104.198.241.255`?** 🔍
It will belong to a different subnet.

| Subnet               | Subnet Mask       | IP Range                   |
| -------------------- | ----------------- | -------------------------- |
| `104.198.241.0/25`   | `255.255.255.128` | `104.198.241.0` → `.127`   |
| `104.198.241.128/25` | `255.255.255.128` | `104.198.241.128` → `.255` |

✅ That division is subnetting.

> The subnet mask stays the same, but the network address is different. That’s what defines a new subnet.
> the have the same number of host bits (7), same mask, but different starting point.

|				 |	1st subnet							|
|----------------|---------------------------------------|
| IP address (.0)| 01101000.11000110.11110001.00000000	|
| Mask			 | 11111111.11111111.11111111.10000000	|
|----------------|-------BITWISE-AND --------------------|
|Network address | 01101000.11000110.11110001.00000000	| 
- 104.198.241.0/25 starts at .0 ❗❗

|				    |	2nd subnet							|
|-------------------|---------------------------------------|
| IP address (0128)	| 01101000.11000110.11110001.10000000	|
| Mask	    		| 11111111.11111111.11111111.10000000	|
|-------------------|-------BITWISE-AND --------------------|
|Network address    | 01101000.11000110.11110001.10000000	| 
- 104.198.241.128/25 starts at .128 ❗❗  
  

🎯 Why Do We Subnet?
- To save IPs (avoid wasting a whole /24 for a few devices)
- To organize networks (e.g., split by department, floor, etc.)
- For routing efficiency and security
---

