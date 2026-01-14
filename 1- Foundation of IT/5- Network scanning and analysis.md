## `ipconfig`, `ping` and `ARP`
Network scanning and discovery is a very important in identifying and mapping the attack surface of a system. These techniques are commonly used by threat actors but are equally valuable for `cybersecurity` professionals conducting security assessments and continuous monitoring.

These tools help retrieve IP configuration details and verify connectivity within a local `subnet`:
- **ipconfig** **(Windows)**: Displays network interface settings, including the MAC address, IPv4/IPv6 addresses, default gateway, and whether the IP is static or assigned via DHCP. If DHCP is used, it also shows the address of the DHCP server.
- **ifconfig** **(Linux)**: Provides similar functionality on Linux systems, displaying network interface configurations.
- **ping**: Sends ICMP Echo Request messages to test if a host is reachable. It can also be scripted to scan an entire subnet.  
    Example (Windows):  
`    for /l %i in (1,1,255) do @ping -n 1 -w 100 10.1.0.%i | find /i "reply"`
- **arp**: Displays the local ARP (Address Resolution Protocol) cache, which maps IP addresses to MAC addresses for recently contacted hosts. This is useful in identifying spoofing or man-in-the-middle (MITM) attacks. For instance, if the MAC address associated with your default gateway differs from the expected router's MAC, it could indicate a MITM attack.
## `route` and `traceroute`
The following tools are used to verify routing configurations and assess connectivity with remote hosts and networks.

- **route**: Displays and manages the local routing table of a host. On most endpoint devices, the routing table is relatively simple, typically consisting of:  
      
    - A **default route** (0.0.0.0/0) directing traffic for external networks through a designated gateway (e.g., 10.1.0.254).  
          
    - A **local subnet route** (e.g., 10.1.0.0/24) for internal traffic, often marked with a gateway of 0.0.0.0 to indicate direct connection via a specific interface (e.g., eth0).

If the host is not functioning as a router, the presence of unexpected entries in the routing table could suggest suspicious activity or misconfiguration.  
  

- **tracert** _(Windows)_ and **traceroute** _(Linux)_: Both tools perform path discovery between a local host and a remote destination. They reveal the sequence of network hops and the **Round Trip Time (RTT)** for each.  
      
    - tracert uses ICMP Echo Requests.
    - traceroute typically uses UDP packets by default.  
          
- **pathping** _(Windows)_: Combines the functionality of ping and `tracert`, providing extended statistics on **latency** and **packet loss** over time.
    - On Linux, a similar tool is `mtr` (My `Traceroute`), which offers real-time analysis.

In security monitoring, **unexpected delays at the default gateway** compared to baseline RTTs may point to a man-in-the-middle (`MITM`) attack. Similarly, unusual latency spikes at other hops could indicate a denial-of-service (`DoS`) attack or simply reflect **network congestion**.
## IP scanners and `nmap`
Using basic tools like ping for network scanning is slow, noisy, and limited in the information it returns. For efficient and detailed topology discovery, `cybersecurity` professionals typically rely on dedicated IP scanner tools.

An **IP scanner** is designed to identify active hosts on a network and determine how they are interconnected. In enterprise environments, tools like **Microsoft System Center** can perform authenticated scans using protocols such as `SNMP` (Simple Network Management Protocol), offering detailed insights into each host.

One of the most `powerfull` and widely used open source scanner is `nmap`. [[1- nmap]]
## `netstat` and `nslookup`
Basic service discovery can also be conducted using built-in tools available on both Windows and Linux systems. These tools help administrators detect unauthorized services, identify potential malware activity, and verify `DNS` configurations.
### `netstat` - network statistic
The `netstat` command displays the current status of `TCP` and `UDP` connections on the local system. It is available on both Windows and Linux (though with different option formats).

- `netstat` can be used to:  
      
    - Detect unauthorized or `misconfigured` services (e.g., a user-installed web or FTP server).
    - Identify suspicious inbound or outbound connections to or from the host.  
    - Reveal which processes are listening on which ports—particularly useful when investigating potential malware activity.  

Example: Filtering `netstat` output on Windows with `findstr` to isolate connections from local `IPv4` addresses. `netstat -ano | findstr "192.168"`

_Note_: On Linux systems, netstat is deprecated and has been replaced by the more modern ss command, which is part of the iproute2 toolset.
### `nslookup` and `dig` - `DNS query tools`
These tools are used to query DNS records for a given domain using a specified DNS resolver:

- **nslookup** (Windows): Allows users to interactively query DNS servers for name resolution data.  
      
- **dig** (Linux): Provides detailed DNS query results and is widely used for troubleshooting and testing.

These tools can help uncover DNS misconfigurations. For example, if a DNS server is improperly configured to allow **zone transfers**, an attacker could retrieve a complete list of hostnames and IP addresses in the domain—revealing critical information about the network structure.

Example: Testing for zone transfer vulnerability on a domain:

dig AXFR @ns1.example.com example.com