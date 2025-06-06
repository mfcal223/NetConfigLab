- [9. 🧯 Exercises tips and Troubleshooting checklist](#9--exercises-tips-and-troubleshooting-checklist)
  - [⚠️ Common Pitfalls in Networking Exercises](#️-common-pitfalls-in-networking-exercises)
  - [🧮 **Decimal to binary - "manual" conversion**](#-decimal-to-binary---manual-conversion)
    - [**Binary numbers you will use in subnet masks**](#binary-numbers-you-will-use-in-subnet-masks)
    - [✏️ **How to Convert Decimal to Binary**](#️-how-to-convert-decimal-to-binary)
    - [💻 **Using "bc" in the terminal window**](#-using-bc-in-the-terminal-window)
  - [🛠️ Diagnostic Tools](#️-diagnostic-tools)

## 9. 🧯 Exercises tips and Troubleshooting checklist

This is my approach when starting a new exercise:   

1. Which are the *devices* that need to connect with each other? Who is sending and who is receiving?
      1. sometimes the "receiving" device (maybe "something" on the internet will give the hint if the IP range the hosts must have)
      2. Is the sender/responder using a destination with **what range**? ---> this will help decide how to split ranges for multiple subnets if necessary.
      3. Is there a host PC that needs to comunicate with something in the internet? Does the internet have the IP range of THAT host PC as destination?
   
2. Are the devices in the *same network*? How many networks and subnets are there?  
      1. which are the networks that must NOT overlap?
      2. Does the IP range need to be adapt? does the subnet mask match that adaptation?
      3. Are all the subnets receiving inside the senders IP range?
   
3. Is the *subnet mask* correct for all devices in the same subnet? Does it match?  
   
4. What are the IPs that I cannot change? Are they next hop or destination IPs? Where should they match?
   
5. What is the network address for each subnet?  

6. Are the IPs in the devices in each subnet *inside IP real range*?  
   
7. Are all IPs *unique*?  
   
8. Is there any host using *network or broadcast address*?  
          - Has any host been assign the **network address** (host bits all 0)?  
           - Has any host been assign the **broadcast address** (host bits all 1)?  


--- 

### ⚠️ Common Pitfalls in Networking Exercises

❌ 1. **Assigning the network or broadcast address to a host** 
  
Network: 192.168.1.0/24  
Host assigned IP: 192.168.1.0 ❌ ← This is the network address  
OR  
Host assigned IP: 192.168.1.255 ❌ ← This is the broadcast address  

❌ 2. **IP doesn’t match the subnet mask**  
  
Device A: 192.168.1.10/24  
Device B: 192.168.2.10/24 ❌ ← They’re on different networks  
  
They won’t be able to reach each other without a router, even if connected physically.  

❌ 3. **Wrong default gateway (e.g., outside the subnet).**  
  
- Wrong IP:  
Device: 192.168.1.50/24  
Gateway assigned: 192.168.2.1 ❌ ← Not in the same subnet  
  
The device won’t know how to reach the gateway, and can’t go outside the local network.  

- Using default all the time: this might lead to a loop detection. Sometimes it is necessary to set the wider range to avoid loops.

❌ 4. **Using /24 for everything blindly**  
  
You only need 6 hosts → /29 would work fine   
Using /24 wastes 254 addresses unnecessarily    
NetPractice may test your ability to choose minimal blocks (CIDR-aware)  
  
❌ 5. **Duplicate IP addresses -> Trying to assign the same IP address to more than one host.**  
  
Device A: 192.168.1.10/24  
Device B: 192.168.1.10/24 ❌ ← Conflict  
  
This causes errors — only one device should use each unique IP.  

❌ 6. **Failling to recognize different subnets connecting to the same router.**  
A router separates subnets! So every interface (even if it's talking directly to a device) is considered part of a different network segment.

If you have one Router A:
| Interface		| Connected to		| IP Address	|	Subnet			|
|	A1			|	Device A		| 192.168.0.1	|	192.168.0.0/26	|
|	A2			|	Device B		| 192.168.0.193	|	192.168.0.192/26|
			
A1 talks to Device A → must be in the same subnet as A
A2 talks to Router B → must be in the same subnet as B's interface
If both interfaces had the same IP or were on the same subnet, routing would fail or loop — because the router wouldn't know where to forward the packet.

✔️ Each router interface must have its own IP address
✔️ Each IP must belong to the subnet it's connected to
❌ You cannot reuse IPs between interfaces
❌ You cannot have two interfaces on the same router in the same subnet

❌ 7. **Failling to divide a range of IP into multiple subnet while staying inside range.**  

Imagine you are receiving packets from the internet with Destination IP = `49.175.13.0/26` 
This means the packets will be send inside the range : `49.175.13.0 - 49.175.13.63`

They will need to go through 2 router (A and B) to arrive to 2 different host PC (C and D), connected to router B.  
Knowing this we can divide our devices into 3 subnets:
- router A <-> router B  
- router B <-> host C
- router B <-> host D
  
Therefore, we will need to divide this `/26` range into at least 3 different subnets that DO NOT overlap. The subnet mask for all those 3 subnets will need to be `/28 or .240`  
- 49.175.13.0 - 49.175.13.15  
- 49.175.13.16 - 49.175.13.31  
- 49.175.13.32 - 49.175.13.47  
- 49.175.13.48 - 49.175.13.63  

> The IP range stills goes from `.0 to .63` to stay within `/26` range.

---

### 🧮 **Decimal to binary - "manual" conversion**

#### **Binary numbers you will use in subnet masks**

|	Decimal	|	Binary	|
|-----------|-----------|
|	128		| 10000000	|
|	192		| 11000000	|
|	224		| 11100000	|
|	240		| 11110000	|
|	248		| 11111000	|
|	252		| 11111100	|
|	254		| 11111110	|
|	255		| 11111111	|

#### ✏️ **How to Convert Decimal to Binary**
To convert decimal numbers into binary, there are several methods, including formulas and division techniques. In this explanation, we'll use the remainder method. The steps to convert a decimal number to binary using this method are as follows:

Step 1: Divide the given decimal number by 2, and find the remainder (Ri).

Step 2: Now divide the quotient (Qi) that is obtained in the above step by 2, and find the remainder.

Step 3: Repeat the above steps 1 and 2 until 0 is obtained as a quotient.

Step 4: Write down the remainder in the following manner: the last remainder is written first, followed by the rest in reverse order (Rn, R(n - 1) .... R1). Thus binary conversion of the given decimal number will be obtained.

![Decimal to binary](https://media.geeksforgeeks.org/wp-content/uploads/20230905164644/17-in-Binary.png)

---

#### 💻 **Using "bc" in the terminal window**
✅ What bc Can Do  
🔢 Arithmetic operations (default = decimal)  
You can perform:  
- Addition: 1 + 2  
- Subtraction: 10 - 3  
- Multiplication: 5 * 4  
- Division: 8 / 2  
- Modulus: 10 % 3  
- Power: 2^8 (if using -l option)
  
> echo "10 + 5" | bc  
> 15  

🔁 Converting Between Number Bases   
Binary, Octal, Decimal, Hex — YES! But you must set the input/output base:  
- Example: Convert Decimal to Binary  
> $ echo "obase=2; 192" | bc  
> 11000000  
- Convert Binary to Decimal  
> $ echo "ibase=2; 11000000" | bc  
> 192  


🧠 ibase = input base  
🧠 obase = output base  

> ⚠️ Note: You must set obase before ibase, or bc will treat your inputs as base-2 immediately.(??????)


### 🛠️ Diagnostic Tools

- `ping`: test reachability
- `traceroute`: path to destination
- `ipconfig`/`ifconfig`: IP info
- `netstat`: current connections

---

Prev:  
[🚏 8. Basic Routing: Guiding Data Across Networks](routing.md#-basic-routing-guiding-data-across-networks)  

Back to : [README file](README.md)  