Network are the back bone of every device connections in other term the internet. it is constituted of  set of protocols and connections between devices.
# Types of network
- `PAN` personal area network like connecting with Bluetooth NFC ect
- `LAN` local area network that covers small spaces like a home or an office and constitute a set of devices connected to a router or a switch, the connection is with the WiFi (802.11) protocol or Ethernet.
- `MAN` metropolitan area network (50-60 km) is a set of connected routers forming multiple `LANs` this with fiber optics connections
- `WAN` wide area network covers a very big area (cities, countries)and is constituted of a lot of interconnected `LANs and MANs`
### Comparison

| **Parameter**        | **LAN**                 | **MAN**                     | **WAN**                             |
| -------------------- | ----------------------- | --------------------------- | ----------------------------------- |
| Network Ownership    | Private                 | Public or Private           | Public or Private                   |
| Coverage Area        | Small (1–5 km)          | Medium (up to 60 km)        | Large (hundreds to thousands of km) |
| Design & Maintenance | Simple                  | Moderate complexity         | Complex                             |
| Bandwidth            | High                    | Moderate                    | Low to High                         |
| Data Throughput      | High                    | Medium                      | Low to Medium                       |
| Congestion           | Low                     | Medium                      | High                                |
| Typical Use          | Homes, schools, offices | Cities, university campuses | Multinational companies, ISPs       |

![[Pasted image 20251226072527.png]]
# The `OSI` model
The **OSI (Open Systems Interconnection)** model is a conceptual framework used to understand and troubleshoot network communications. It breaks the communication process into **seven layers**, each responsible for a specific task.

![[Pasted image 20251226072653.png]]
### Why the OSI Model Matters:  
Even though modern networks often use the simpler TCP/IP model, OSI helps in diagnosing problems and designing network systems by breaking down the communication steps into clear, understandable layers.
# IP address fundamentals
An **IP address** is a unique identifier assigned to each device on a network. It helps in routing data to the correct destination. IPv4 addresses are 32-bit values, typically written in **dotted decimal notation** (e.g., 192.168.0.1).
## Why using IP addresses and not MAC addresses
ip addresses are more flexible to subnet and even to connect to something or to someone we dont have to know his mac address that will be a lot.
# IP address
An **IP address** is a unique identifier assigned to each device on a network. It helps in routing data to the correct destination. IPv4 addresses are 32-bit values, typically written in **dotted decimal notation** (e.g., 192.168.0.1).

An IP v4 address is a set of 4 octe that is 8 bits for 1 octe so 32bits. it can be written 0b0000_0000.0000_0000.0000_0000.0000_0000 in binary

![[Pasted image 20251226131844.png]]

### **What is Subnetting?**

Subnetting allows a large network to be divided into smaller, manageable segments called **subnets**. This improves efficiency and network security.

Example:  
For a network 192.168.1.0/28, the subnet mask is 255.255.255.240.

- **Usable IPs per subnet:** 14 (out of 16)
- **Broadcast address:** Last IP in the range
- **First subnet:** 192.168.1.0 – 192.168.1.15
- **Second subnet:** 192.168.1.16 – 192.168.1.31  

Each subnet can be assigned to different departments or devices within an organization.
## IP address classes
IP addresses can subdivide into groups each has a max number of possible hosts.

|   |   |   |
|---|---|---|
|**Class**|**Range**|**Usage**|
|A|1.0.0.1 to 126.255.255.254|Large networks|
|B|128.1.0.1 to 191.255.255.254|Medium-sized networks|
|C|192.0.1.1 to 223.255.254.254|Small networks|
|D|224.0.0.0 to 239.255.255.255|Multicasting|
|E|240.0.0.0 to 255.255.255.254|Research and experimental|
![[Pasted image 20251226132020.png]]
## Network masking (classless)
this is the best way to subnet an ip address as it gives more flexibility.

Default (natural) subnet masks:

|   |   |
|---|---|
|**Class**|**Default Mask**|
|A|255.0.0.0|
|B|255.255.0.0|
|C|255.255.255.0|
![[Pasted image 20251226132930.png]]

## Exercise
We have an initial address of 10.0.0.0/8 `the /8 means that thers is 8bits that are part of the net ID so 8 - 32 bits usable by the host`
we can write it in binary `0b0000_01010.0000_0000.0000_0000.0000_0000`
### 10
we want to sub-net this address into an address for only 10 hosts.
so first we have to do the `log2(10 hosts) = 3`. so we take it 4, that mean that the 10 hosts take 4 bits of the address. thus 32 - 4 = 28, our new network for these 10 devices are 10.0.0.0/28 so in binary `0b1111_1111.0000_0000.00000_0000.0000____00010` the `____` make the delimitation between the host and network id.

to calculate the first host capable IP we work with binary our address in binary is `0b1111_1111.0000_0000.00000_0000.0000_0000` this is our network address 10.0.0.0 the first capable host is `0b1111_1111.0000_0000.00000_0000.0000_0001` so 10.0.0.1

the broadcast is the last capable address that serves to connect to all the hosts that is in binary `0b1111_1111.0000_0000.00000_0000.0000_1111` that gives 10.0.0.15

the first usable address for the next sub-net is in binary `0b1111_1111.0000_0000.00000_0000.0001___0001` that gives 10.0.0.17
### 1000
so for 10000 devices we calculate how much bits we need `log2(1000) = 9.9` we take 10 that we - 32 and gives 22. 10.0.0.0/22.

in binary that gives `0b0000_1010.0000_0000.0000_00___00.0000_0000` where `____` is the delimitation between the host and network id.

so the first is the same binary + 1 and gives 10.0.0.1

broadcast is `0b0000_1010.0000_0000.0000_00___11.1111_1111` and gives `10.0.3.255` we treat each octet alone.

first usable address for the 2nd sub-net in binary is `0b0000_1010.0000_0000.0000_01___00.0000_0001` that gives 10.0.4.1.
# note
### broadcast 
a broadcast is an address that is fixed, the last one in an ip range 192.168.1.255 as an example and allows to send packets to all the connected devices at once in binary `0b0000_1010.0000_0000.0000_00___11.1111_1111` 
