
## 🚏 Basic Routing: Guiding Data Across Networks
Routing is the function of directing data packets across networks from their source to their destination. The Internet Protocol (IP) is responsible for this.

### 🚪 Default Gateway: : Your Exit to Other Networks
- Used when a device needs to communicate **outside its subnet**.
- E.g., `Router IP: 192.168.1.1`

The default gateway is the IP address of the device, usually a router, that serves as the access point for devices on a local network to send data to destinations on other networks (like the internet).   
When a device wants to communicate with an IP address that is not on its local network (as determined by its IP address and subnet mask), it sends the data packet to its configured default gateway.

---
  
### ⛓ Switch
A switch connects multiple devices together in a single network. Unlike a router, the switch does not have any interfaces since it only distributes packets to its local network, and cannot talk directly to a network outside of its own.

---

### Routers 

**Routers** are network devices specifically designed to perform routing: they connect multiple networks together.
They examine the destination IP address of incoming packets and use routing tables to decide the most efficient path to forward the packet towards its final destination, potentially across multiple interconnected networks.  
Understanding how routing works at a basic level helps predict how data will travel and diagnose connectivity issues.
 
The router has an interface for each network it connects to.  
Since the router separates different networks, the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.

#### Routing Table 

A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations.  

In some exercises, the routing table consists of 2 elements:
- Destination: The destination specifies a network address on which a host is the end target of the packets. 
  - The route of default or 0.0.0.0/0, is the route that takes effect when no other route is available for an IP destination address. 
  - The default route will use the next-hop address to send the packets on their way without giving a specific destination. 
  - The default route will match any network.

- Next hop: = the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.

![Routing Table](https://www.baeldung.com/wp-content/uploads/sites/4/2022/10/Routing-Table.drawio.png)