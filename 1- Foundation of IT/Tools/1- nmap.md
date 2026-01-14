### Some switches and settings
- `-sS` syn scan
- `-sU` `UDP`scan
- `-O` `-A` Operating system detection / full OS version discovery
- `-sV` version detection
- `-v` , `-vv` increase verbosity level 1 and 2
- `-oA` , `-oN` , `-oG` save result in thee major format, normal format, `grepable` format
- `-A` aggressive mode
- `-T<number>` timing template to increase of speed of the scan result
- `-p <port or post-post>`, `-p-` scan specified port, scan all ports
- `--script`, `--script=vuln` activate a scripting library, activate `vuln` category
- `-sT`, `-sN`, `-sF`, `-sX` `TCP` scan, Null scan, FIN scan, `Xmax` scan
## Scan types
#### `TCP` scan `-sT`
when `nmap` is scanning for open ports he sends a `TCP SYN` packets if an` SYN/ACK` is received that mean that the port is open otherwise a `RST` packet is sent meaning that the port is closed `RFC 9293`. when a firewall blocks the scan there is no response so the `nmap` flags the port as filtered.
#### `SYN` scan `-sS`
Referred as stealth scan or half-open operates with the `tcp` however when `nmap` sends an `ACK` when receiving the `SYN/ACK` response `nmap` respond with a `RST` (this prevents the server from repeatedly trying to make the request).

This has a variety of advantages for us as hackers:

- It can be used to bypass older Intrusion Detection systems as they are looking out for a full three way handshake. This is often no longer the case with modern IDS solutions; it is for this reason that SYN scans are still frequently referred to as "stealth" scans.
- SYN scans are often not logged by applications listening on open ports, as standard practice is to log a connection once it's been fully established. Again, this plays into the idea of SYN scans being stealthy.
- Without having to bother about completing (and disconnecting from) a three-way handshake for every port, SYN scans are significantly faster than a standard `TCP` Connect scan.

There are, however, a couple of disadvantages to SYN scans, namely:

- They require `sudo` permissions[1] in order to work correctly in Linux. This is because SYN scans require the ability to create raw packets (as opposed to the full `TCP` handshake), which is a privilege only the root user has by default.
- Unstable services are sometimes brought down by SYN scans, which could prove problematic if a client has provided a production environment for the test.
#### `UDP` scan `-sU`
`UDP` connections are stateless, so no connection are initiated it just send a packet and hope it arrives. when `nmap` receives no response it flags it as open and filtered (we have no way to know if it was received or not or maybe a firewall is blocking the connection) however when an `UDP` response is received the port is opened.

when a closed `UDP` port receive an `UDP` packet he respond with an `icmp` ping packet with a message that the port is unreachable.

Due to this difficulty in identifying whether a `UDP` port is actually open, `UDP` scans tend to be incredibly slow in comparison to the various `TCP` scans (in the region of 20 minutes to scan the first 1000 ports, with a good connection). For this reason it's usually good practice to run an `Nmap` scan with `--top-ports <number>` enabled.

When scanning `UDP` ports, `Nmap` usually sends completely empty requests -- just raw `UDP` packets. That said, for ports which are usually occupied by well-known services, it will instead send a protocol-specific payload which is more likely to elicit a response from which a more accurate result can be drawn.
#### `NULL, FIN, Xmas` scan
NULL, FIN and Xmas `TCP` port scans are less commonly used than any of the others, All three are interlinked and are used primarily as they tend to be even stealthier, relatively speaking, than a SYN "stealth" scan. Beginning with NULL scans:

As the name suggests, NULL scans (`-sN`) are when the TCP request is sent with no flags set at all. As per the RFC, the target host should respond with a RST if the port is closed.  
![[Pasted image 20251229081909.png]]

FIN scans (`-sF`) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed.
![[Pasted image 20251229081924.png]]

As with the other two scans in this class, Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark.
![[Pasted image 20251229081958.png]]

The expected response for _open_ ports with these scans is also identical, and is very similar to that of a UDP scan. If the port is open then there is no response to the malformed packet. Unfortunately (as with open UDP ports), that is _also_ an expected behaviour if the port is protected by a firewall, so NULL, FIN and Xmas scans will only ever identify ports as being _open|filtered_, _closed_, or _filtered_. If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.  

It's also worth noting that while RFC 793 mandates that network hosts respond to malformed packets with a RST TCP packet for closed ports, and don't respond at all for open ports; this is not always the case in practice. In particular Microsoft Windows (and a lot of Cisco network devices) are known to respond with a RST to any malformed TCP packet -- regardless of whether the port is actually open or not. This results in all ports showing up as being closed.  

That said, the goal here is, of course, firewall evasion. Many firewalls are configured to drop incoming TCP packets to blocked ports which have the SYN flag set (thus blocking new connection initiation requests). By sending requests which do not contain the SYN flag, we effectively bypass this kind of firewall. Whilst this is good in theory, most modern IDS solutions are savvy to these scan types, so don't rely on them to be 100% effective when dealing with modern systems.
#### `ICMP` network scanning `-sn`
on a first connection to a target network the first objective is to map active `IP` addresses so `nmap` performs a 'ping sweep' sending an `ICMP` packet to each possible `ip` (this is not always accurate).

The `-sn` switch tells Nmap not to scan any ports -- forcing it to rely primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets. In addition to the ICMP echo requests, the `-sn` switch will also cause nmap to send a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.
## `NSE` scripts
The **N**map **S**cripting **E**ngine (NSE) is an incredibly powerful addition to Nmap, extending its functionality quite considerably. NSE Scripts are written in the _Lua_ programming language, and can be used to do a variety of things: from scanning for vulnerabilities, to automating exploits for them. The NSE is particularly useful for reconnaisance, however, it is well worth bearing in mind how extensive the script library is.

There are many categories available. Some useful categories include:

- `safe`:- Won't affect the target
- `intrusive`:- Not safe: likely to affect the target  
- `vuln`:- Scan for vulnerabilities
- `exploit`:- Attempt to exploit a vulnerability
- `auth`:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
- `brute`:- Attempt to bruteforce credentials for running services
- `discovery`:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

A more exhaustive list can be found [here](https://nmap.org/book/nse-usage.html).
#### Working with `NSE`
##### Using script categories
To use a script category the `--script=<category>` command is used.
##### Using script name
To run a specific script we use the `--script=<scriptname,....>` Some scripts require arguments these can be given with the `--script-args` Nmap switch after specifying the script.

example: `nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'` 

A full list of scripts and their corresponding arguments (along with example use cases) can be found [here](https://nmap.org/nsedoc/).
##### Using script menuhttps://student.learn.gomycode.co/
Nmap scripts come with built-in help menus, which can be accessed using `nmap --script-help <script-name>`. This tends not to be as extensive as in the link given above, however, it can still be useful when working locally.
#### Searching for scripts
you can search for scipts either in the nmap website or locally.

 Nmap stores its scripts on Linux at `/usr/share/nmap/scripts`. All of the NSE scripts are stored in this directory by default -- this is where Nmap looks for scripts when you specify them.

There are two ways to search for installed scripts. One is by using the `/usr/share/nmap/scripts/script.db` file. Despite the extension, this isn't actually a database so much as a formatted text file containing filenames and categories for each available script.

Nmap uses this file to keep track of (and utilise) scripts for the scripting engine; however, we can also _grep_ through it to look for scripts. For example: `grep "ftp" /usr/share/nmap/scripts/script.db`.

The second way to search for scripts is quite simply to use the `ls` command. For example, we could get the same results as in the previous screenshot by using `ls -l /usr/share/nmap/scripts/*ftp*` you can specify other than ftp.

The same techniques can also be used to search for categories of script. For example:  
`grep "safe" /usr/share/nmap/scripts/script.db`
#### Installing new scripts
We mentioned previously that the Nmap website contains a list of scripts, so, what happens if one of these is missing in the `scripts` directory locally? A standard `sudo apt update && sudo apt install nmap` should fix this; however, it's also possible to install the scripts manually by downloading the script from Nmap (`sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`). This must then be followed up with `nmap --script-updatedb`, which updates the `script.db` file to contain the newly downloaded script.
#### Firewall evasion
Some of the technique we have seen are `stealth scans, along with NULL, FIN and Xmas scans`.

typically windows config block the `ICMP` ping packet and nmap rely on then to determine if a host is up or not however the `-Pn` switch work in a way where nmap thinks that every device is up and skips the ping.

This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block; however, it comes at the price of potentially taking a very long time to complete the scan (if the host really is dead then Nmap will still be checking and double checking every specified port).

It's worth noting that if you're already directly on the local network, Nmap can also use ARP requests to determine host activity.

There are a variety of other switches which Nmap considers useful for firewall evasion. We will not go through these in detail, however, they can be found [here](https://nmap.org/book/man-bypass-firewalls-ids.html).

The following switches are of particular note:

- `-f`:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
- An alternative to `-f`, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This _must_ be a multiple of 8.
- `--scan-delay <time>ms`:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
- `--badsum`:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.