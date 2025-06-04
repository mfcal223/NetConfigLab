- [9. 🧯 Exercises tips and Troubleshooting checklist](#9--exercises-tips-and-troubleshooting-checklist)
	- [⚠️ Common Pitfalls in Networking Exercises](#️-common-pitfalls-in-networking-exercises)
	- [🧮 Decimal to binary - "manual" conversion](#-decimal-to-binary---manual-conversion)
		- [✏️ How to Convert Decimal to Binary](#️-how-to-convert-decimal-to-binary)
		- [💻 Using "bc" in the terminal window](#-using-bc-in-the-terminal-window)
	- [🛠️ Diagnostic Tools](#️-diagnostic-tools)

## 9. 🧯 Exercises tips and Troubleshooting checklist

This is my approach when starting a new exercise:   

1. Which are the *devices* that need to connect with each other?  
   
2. Are the devices in the *same network*? How many networks and subnets are there?  
   
3. Is the *subnet mask* correct for all devices in the same subnet? Does it match?  
   
4. Are the IPs in the devices in each subnet *inside IP real range*?  
   
5. Are all IPs *unique*?  
   
6. Is there any host using *network or broadcast address*?  
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
  
Device: 192.168.1.50/24  
Gateway assigned: 192.168.2.1 ❌ ← Not in the same subnet  
  
The device won’t know how to reach the gateway, and can’t go outside the local network.  

❌ 4. **Using /24 for everything blindly**  
  
You only need 6 hosts → /29 would work fine   
Using /24 wastes 254 addresses unnecessarily    
NetPractice may test your ability to choose minimal blocks (CIDR-aware)  
  
❌ 5. **Duplicate IP addresses -> Trying to assign the same IP address to more than one host.**  
  
Device A: 192.168.1.10/24  
Device B: 192.168.1.10/24 ❌ ← Conflict  
  
This causes errors — only one device should use each unique IP.  

---

### 🧮 Decimal to binary - "manual" conversion

#### ✏️ How to Convert Decimal to Binary
To convert decimal numbers into binary, there are several methods, including formulas and division techniques. In this explanation, we'll use the remainder method. The steps to convert a decimal number to binary using this method are as follows:

Step 1: Divide the given decimal number by 2, and find the remainder (Ri).

Step 2: Now divide the quotient (Qi) that is obtained in the above step by 2, and find the remainder.

Step 3: Repeat the above steps 1 and 2 until 0 is obtained as a quotient.

Step 4: Write down the remainder in the following manner: the last remainder is written first, followed by the rest in reverse order (Rn, R(n - 1) .... R1). Thus binary conversion of the given decimal number will be obtained.

![Decimal to binary](https://media.geeksforgeeks.org/wp-content/uploads/20230905164644/17-in-Binary.png)

---

#### 💻 Using "bc" in the terminal window
✅ What bc Can Do  
🔢 Arithmetic operations (default = decimal)  
You can perform:  
- Addition: 1 + 2  
- Subtraction: 10 - 3  
- Multiplication: 5 * 4  
- Division: 8 / 2  
- Modulus: 10 % 3  
- Power: 2^8 (if using -l option)
  
$ echo "10 + 5" | bc  
15  

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