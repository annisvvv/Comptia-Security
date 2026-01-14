# Cisco CLI Basics  
This lab introduces you to the Cisco CLI—a powerful tool for router and switch configuration.

- The CLI is structured with different command modes:  
    - **User Exec Mode:** RouterName> (basic commands like ping)  
    - **Privileged Exec Mode:** RouterName# (advanced commands, enter by typing enable)  
    - **Global Configuration Mode:** RouterName(config)# (for configuring the device)  
    - **Interface Configuration Mode:** RouterName(config-if)# (configure specific interfaces)  

- Use exit to go back one level, or Ctrl+Z to return to privileged mode instantly.   

- If a command is not recognized, you may be at the wrong mode. Use ? to view available commands at any level.  

- The CLI has progressive help: typing ? after part of a command shows valid options to complete it.  

- Common commands you’ll use frequently:  
    - show run — Displays the current running configuration
    - show ip route — Displays the routing table
    - copy run start — Saves the running configuration to startup configuration
    - no ip domain-lookup — Prevents delays caused by mistaken DNS lookups on typos  

_Tip:_ You can abbreviate commands if they are unique (e.g., conf t for configure terminal).
# Config IP over an Eth port

| **Mode**             | **Prompt**           | **How to get there**      | **Purpose**                                   |
| -------------------- | -------------------- | ------------------------- | --------------------------------------------- |
| **User EXEC**        | `Router>`            | Default on login          | View basic stats (Read-only).                 |
| **Privileged EXEC**  | `Router#`            | Type `enable`             | High-level viewing and saving.                |
| **Global Config**    | `Router(config)#`    | Type `configure terminal` | Change settings that affect the whole router. |
| **Interface Config** | `Router(config-if)#` | Type `interface <name>`   | Change settings for one specific port.        |

name = `fastEthernet(x/x)`
# Config RIPv2
`RIPv2` stands for Routing Version Protocol version 2 is an older, simple distance-vector dynamic routing protocol used within local networks (Autonomous Systems) to automatically create routing tables, relying on hop count (max 15) as its metric, but offering key enhancements over RIPv1 like support for subnet masks(VLSM) and authentication, using multicast to send updates efficiently to neighbors, making it suitable for small, simple networks, though largely replaced by more scalable protocols like OSPF in larger environments

```
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# no auto-summary
Router(config-router)# network <network-address>
Router(config-router)# network <network-address>
Router(config-router)# end
########## write // to save
Router# copy running-config startup-config
```

| Command                              | Explanation                                                                                                                                                                               |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enable`                             | Enters privileged EXEC mode.                                                                                                                                                              |
| `configure terminal`                 | Enters global configuration mode.                                                                                                                                                         |
| `router rip`                         | Enables the RIP routing protocol.                                                                                                                                                         |
| `version 2`                          | Specifies that the router should use RIP version 2.                                                                                                                                       |
| `no auto-summary`                    | Disables automatic route summarization, allowing for classless routing and support for Variable Length Subnet Masks (VLSM). This is essential for modern networks.                        |
| `network <network-address>`          | Tells the router which directly connected classful networks to advertise via RIP. For example, if an interface has an IP address of 192.168.1.10/24, you would use `network 192.168.1.0`. |
| `end`                                | Exits configuration modes and returns to privileged EXEC mode.                                                                                                                            |
| `copy running-config startup-config` | Saves the current configuration so it is not lost upon a device reboot.                                                                                                                   |
| `show ip route`                      | To see if everything is working fine.                                                                                                                                                     |
# Configure a DNS server
To configure a DNS server pointing to a http server hosting a web page:
1. Configure the necessities `ip addresses, routers, ect`
2. configure the RIPv2 or any other routing protocol between the routers
3. Give the DNS server the address of the http server, the computers the address of the DNS server.
# Configure IP addresses

| **Command**               | **Purpose**                                           |
| ------------------------- | ----------------------------------------------------- |
| `enable`                  | Switches to Privileged EXEC mode.                     |
| `config t`                | Short for `configure terminal`; enters global config. |
| `interface <name>`        | Accesses a specific port (e.g., `fa0/0`, `g0/1`).     |
| `ip address <ip> <mask>`  | Sets the static IP and subnet mask.                   |
| `no shutdown`             | "Wakes up" the interface (changes status to UP).      |
| `show ip interface brief` | **Verification:** Shows all ports and their status.   |
# configure `IGRP` routing
```
Router>enable
Router#configure terminal
Router(config)#router eigrp [AS_number] // choose a same number netween all routers 0 - 65535
Router(config-router)#network [network-address] [wildcard-mask (255... - 255.)] 
Router(config-router)#no auto-summary
Router(config-router)#passive-interface [interface-name]
Router(config-router)#exit
Router(config)#exit
Router#copy running-config startup-config
```

- `show ip eigrp neighbors`: Displays a list of all EIGRP neighbors the router has discovered.
- `show ip route eigrp`: Shows only the routes learned via EIGRP in the routing table (indicated by the letter "D").
- `show ip eigrp topology`: Displays the EIGRP topology table, including all learned routes and potential backup routes.
- `show ip protocols`: Provides an overview of all active routing protocols and their parameters.
- **Test connectivity:** Use the `ping` command from one end device to another across different networks to verify full end-to-end connectivity.
- `show ip eigrp interfaces`