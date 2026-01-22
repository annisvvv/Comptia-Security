# MAC address

The **MAC (Media Access Control) address** is a **physical address** tied to the **network interface card (NIC)** of a device. It works at **Layer 2 (Data Link Layer)** of the OSI model and is primarily used **within a local network (LAN)**.

A MAC address is a 48-bit number (12 hexadecimal characters), often displayed in pairs separated by colons or hyphens, like 00:1A:2B:3C:4D:5E.  
The **first half** usually identifies the device manufacturer, while the **second half** is a unique identifier for the device.

Example:  
00-1A-2B-3C-4D-5E  
↳ 00-1A-2B → Manufacturer ID  
↳ 3C-4D-5E → Device-specific ID

These addresses are **pre-assigned by the manufacturer** and usually do not change. However, MAC spoofing tools can temporarily override the address in software.

MAC addresses are **only relevant inside a local network**. When a packet is sent outside the LAN (e.g., to the internet), its MAC address is **not retained**.
# IPv4 and IPv6
The **IP (Internet Protocol) address** is a **logical address** used to identify a device globally across networks. It operates at **Layer 3 (Network Layer)** of the OSI model.

There are two major versions:

- **IPv4**: 32-bit address written in dotted decimal, e.g., 192.168.1.10
- **IPv6**: 128-bit address written in hexadecimal, e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334 

An IP address can be assigned **manually (static IP)** or **automatically using DHCP (Dynamic Host Configuration Protocol)**.

Unlike MAC addresses, **IP addresses can change** depending on the network the device is connected to.
# How Do MAC and IP Work Together?

When a device sends data across networks, it uses **both addresses**:

1. The **IP address** helps identify the **destination network**.
2. Once the data reaches the destination network, the **MAC address** is used to deliver it to the **correct device** within the local segment.

This translation between IP and MAC is done using **ARP (Address Resolution Protocol)**, which maps IP addresses to their corresponding MAC addresses.
# Ports
A **port** is a logical communication endpoint that allows a device to distinguish between multiple services or applications running on the same system. Think of it as a numbered "door" through which data enters or leaves a computer. the port numbers go from `0–65535` 

Even though data may travel to a single IP address, **ports allow simultaneous services** to operate without conflict. For instance, you can download a file via FTP (port 21) while browsing a website (port 80) over the same network.

Ports operate at **Layer 4 – the Transport Layer**. They are used by transport protocols like **TCP** and **UDP** to direct packets to the correct service. Network layer protocols (e.g., IP) only deliver packets to the device, not to the specific service.

| **Port** | **Protocol** | **Use**                         |
| -------- | ------------ | ------------------------------- |
| 20, 21   | FTP          | File Transfer                   |
| 22       | SSH          | Secure remote access            |
| 25 / 587 | SMTP         | Email (unencrypted / encrypted) |
| 53       | DNS          | Domain name resolution          |
| 80       | HTTP         | Web browsing                    |
| 123      | NTP          | Time synchronization            |
| 443      | HTTPS        | Secure web browsing             |
| 3389     | RDP          | Remote desktop                  |

#### Port Ranges
- **0–1023:** Well-known ports (reserved for system services)  
- **1024–49151:** Registered ports (used by user applications)  
- **49152–65535:** Dynamic/private ports (temporary use)
### Note
netcat
# TCP and UDP
### TCP
**TCP** is a **connection-oriented** protocol. Before sending data, it establishes a connection using a process called the **three-way handshake**. TCP ensures that data is delivered **accurately and in order**.

![Pasted image 20251226140723](../zzfiles/Pasted%20image%2020251226140723.png)
#### Key Features of TCP:
- Reliable delivery with error checking and acknowledgment
- Sequence numbers to ensure correct order
- Flow control and congestion control
- Retransmits lost packets
- Slower due to overhead, but very reliable
#### TCP use cases
`tcp` is used where we dont want to lose packets like in **File Transfer Protocol (FTP)** , **Secure Shell (SSH)** , **World Wide Web (WWW**) ect
### UDP
**UDP** is a **connectionless** protocol. It sends data without establishing a prior connection, which makes it **faster but less reliable**. There’s no acknowledgment, sequencing, or retransmission.

![Pasted image 20251226140834](../zzfiles/Pasted%20image%2020251226140834.png)
#### Key Features of UDP:
- Lightweight and fast
- No guarantee of delivery or order
- Minimal error checking
- Supports broadcasting and multicasting
#### UDP use cases
`UDP` is used where reliability is not needed but speed is like in voice calls, video calls ect
## TCP vs. UDP: Side-by-Side Comparison

| **Feature**       | **TCP**                               | **UDP**                                   |
| ----------------- | ------------------------------------- | ----------------------------------------- |
| Connection        | Connection-oriented (3-way handshake) | Connectionless                            |
| Reliability       | Reliable, ensures delivery            | Unreliable, no guarantees                 |
| Ordering          | Guarantees packet order               | No ordering                               |
| Speed             | Slower due to overhead                | Faster, minimal delay                     |
| Acknowledgment    | Yes                                   | No                                        |
| Retransmission    | Yes (if packets are lost)             | No                                        |
| Error Checking    | Extensive                             | Basic (checksum only)                     |
| Header Size       | 20–60 bytes                           | 8 bytes                                   |
| Use Cases         | Web, email, file transfers            | Streaming, gaming, DNS, voice/video calls |
| Broadcast Support | No                                    | Yes                                       |
| Protocol Examples | HTTP, HTTPS, FTP, SMTP, SSH           | DNS, DHCP, TFTP, SNMP, VoIP, RIP          |
# NAT network address translation
Network Address Translation, or NAT, allows multiple devices within a private network to access the internet using a single public IP address. This technique helps conserve the limited pool of available IPv4 addresses.

The IPv4 addressing scheme provides a maximum of 2³² addresses (approximately 4.3 billion), which is insufficient considering the vast number of internet-connected devices. NAT addresses this limitation by allowing private IP addresses to be reused internally while relying on just one public IP address for external communication.

![Pasted image 20251226141700](../zzfiles/Pasted%20image%2020251226141700.png)
#### **How NAT Works**

NAT operates by translating private IP addresses into public ones (and vice versa). This process typically takes place on the network’s edge device, such as a router or firewall, which is connected to both the internal (private) and external (public) networks.

When a packet is sent from a device in the private network to the internet, NAT replaces the internal source IP with a public IP. It also modifies the source port number and logs this mapping in the NAT translation table. When the response arrives, NAT refers to this table to determine which internal device should receive the packet, restoring the original IP and port.

If the public IP pool is exhausted (in dynamic NAT configurations), NAT cannot assign a new public address and will drop the packet, often sending back an ICMP host unreachable message.

#### **Why Port Numbers Are Also Translated**

Imagine two internal hosts (A and B) sending traffic to the same external server using the same port number, say 1000. If NAT only translated the IP addresses and not the ports, both sets of packets would appear identical once they reach the destination — making it impossible for NAT to know which reply is for which device. To prevent this, NAT also changes the source port numbers and records these changes in its NAT table. This process ensures that return traffic is directed to the correct internal host.
#### **Types of NAT**

1. **Static NAT**  
    Maps a single private IP to a single public IP in a one-to-one relationship. This is often used for hosting internal services accessible from outside. However, it requires one public IP per device, which can be costly.  
      
    
2. **Dynamic NAT**  
    Maps private IPs to a pool of public IPs. If no public IP is available in the pool, the request is dropped. This method is more flexible than static NAT but still requires a sizable pool of public IPs.  
      
    
3. **Port Address Translation (PAT)** – Also known as NAT Overload  
    PAT How NAT Works
NAT operates by translating private IP addresses into public ones (and vice versa). This process typically takes place on the network’s edge device, such as a router or firewall, which is connected to both the internal (private) and external (public) networks.

When a packet is sent from a device in the private network to the internet, NAT replaces the internal source IP with a public IP. It also modifies the source port number and logs this mapping in the NAT translation table. When the response arrives, NAT refers to this table to determine which internal device should receive the packet, restoring the original IP and port.

If the public IP pool is exhausted (in dynamic NAT configurations), NAT cannot assign a new public address and will drop the packet, often sending back an ICMP host unreachable message.

Why Port Numbers Are Also Translated
Imagine two internal hosts (A and B) sending traffic to the same external server using the same port number, say 1000. If NAT only translated the IP addresses and not the ports, both sets of packets would appear identical once they reach the destination — making it impossible for NAT to know which reply is for which device. To prevent this, NAT also changes the source port numbers and records these changes in its NAT table. This process ensures that return traffic is directed to the correct internal host.allows multiple private IP addresses to share a single public IP by using different port numbers. This is the most widely used NAT type today, as it enables thousands of devices to access the internet through just one public IP.
# `ICMP` and `ARP`
### `ARP` address resolution protocol
Since network communication at the data link layer requires MAC addresses, but most routing decisions are based on IP addresses, a mechanism is needed to translate between the two. This is where the **ARP protocol (Address Resolution Protocol)** comes into play.

**ARP is responsible for mapping IP addresses to MAC addresses.** When a device wants to send data to another device on the same local network, it uses ARP to find the MAC address corresponding to the target IP address.

Here’s a simplified explanation of how ARP works:

1. **Check the ARP Cache**  
    The sending device first checks its ARP cache — a local memory storing recent IP-to-MAC address mappings.
    - If the MAC address for the target IP is already cached, it uses it immediately.
    - If not, the device sends an ARP Request to the entire network.  

2. **ARP Request Broadcast**  
    The ARP request is sent as a **broadcast**, meaning all devices on the subnet receive it. The message asks, "Who has this IP address?" Only the device with the matching IP will respond with its MAC address.  

3. **ARP Reply**  
    The destination device replies with its MAC address, and the sender updates its ARP cache and proceeds with data transmission.
### `ICMP` internet control message protocol
ICMP (Internet Control Message Protocol) is used for ping because it's designed for network diagnostics, allowing devices to send lightweight "echo requests" to check reachability, measure round-trip time (latency), and detect packet loss, acting as a simple, universal way to verify if a host is alive and how well it's responding on an IP network. It provides fundamental feedback for troubleshooting, making it ideal for the simple "is it there and how fast?" job of ping. 

Key Reasons for Using ICMP for Ping:
- **Connectivity Testing:** Ping sends an ICMP Echo Request to a target; if reachable, the target sends back an ICMP Echo Reply, confirming basic communication.
- **Latency Measurement:** By timing how long the Echo Reply takes to return (Round-Trip Time or RTT), you measure network delay, indicating connection speed.
- **Packet Loss Detection:** If replies don't cocontrolme back, it signals packet loss, pointing to network congestion or issues.
- **Simplicity & Efficiency:** ICMP is a lightweight protocol, requiring minimal resources, making it fast and efficient for quick checks.
- **Universal Compatibility:** Most network devices support ICMP, allowing you to test across different types of hardware.
- **Diagnostic Foundation:** It's a core diagnostic tool, forming the basis for other utilities like `traceroute`, which map the entire path by using ICMP Time Exceeded messages. 

In essence, ping leverages ICMP's error reporting and operational messaging capabilities to provide essential real-time insights into network health and performance.
# `DHCP` and `DNS`
### `DHCP` dynamic host configuration protocol
`DHCP` is used to automatically assign IP addresses and other essential network configuration settings—such as the subnet mask, default gateway, and DNS server—to devices on a network. It simplifies network management and eliminates the need for manual configuration on each device.

When a device, such as a smartphone or computer, connects to a network, it initiates a process to obtain an IP address from a **DHCP server**. This process involves a four-step message exchange between the client and the server also called "DORA" :

1. **DHCP Discover** – The client broadcasts a request to locate any available DHCP server.
2. **DHCP Offer** – A DHCP server responds with an offer containing an available IP address and configuration information.
3. **DHCP Request** – The client sends a request to the server to accept the offered IP address.
4. **DHCP Acknowledgment (ACK)** – The server confirms that the IP address has been assigned to the client.

This process allows a device to join the network with the necessary configuration, without user intervention.
### `DNS` domain name system
`DNS` translates human-readable domain names (like www.example.com) into machine-readable IP addresses (like 210.38.33.7).

Here’s how the DNS resolution process works:

1. The browser contacts the **Local DNS Server (LDNS)** and asks for the IP address of the domain.  
2. If the LDNS doesn’t have the information cached, it forwards the request to a **root DNS server**, which points it to the appropriate **Top-Level Domain (TLD) server** (e.g., .com).  
3. The TLD server responds with a **Name Server (NS) record** for the requested domain.  
4. The LDNS then contacts the authoritative DNS server and requests an **A record**, which contains the actual IP address.  
5. Once received, the LDNS returns the IP address to the browser and caches the response for future queries.
