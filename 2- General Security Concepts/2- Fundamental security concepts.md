These are the foundation of modern cyber-security
# The CIA triad
this is the core model that guides how we protect systems and information

- C : Confidentiality
- I : integrity
- A : Availability

this outlines the key principles that every secure system should be built upon, this ensure the perfect equilibrium between protection, reliability, and ease of access.

a weakness in one area can compromise the others.

| Confidentiality | is all about keeping information private. It ensures that only authorized individuals can access sensitive data — whether it’s personal records, business documents, or internal communications. Techniques like encryption, access control, and secure authentication are commonly used to protect confidentiality and keep prying eyes out. |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Integrity       | ensures that information remains accurate and unaltered. Whether data is being stored or transmitted, it must stay complete and trustworthy. Mechanisms like hashing (e.g., SHA-256, SHA-1) are often used to verify that data hasn’t been tampered with or corrupted during transit or storage.                                              |
| Availability    | means that information and systems are accessible when needed. Even the most secure data is useless if users can’t access it. To maintain availability, organizations rely on strategies like redundancy, system monitoring, backups, and disaster recovery planning.                                                                         |

# Non repudiation
Non-repudiation is the assurance that someone cannot deny having performed an action, this ensures accountability. (log utilization)
# Authentication, Authorization, and Accounting
this is the AAA model, this ensure secure management of who access to systems and resources and hat they are allowed to do.

AAA is often implemented using dedicated servers and protocols that manage user and device interactions.


| Authentication | Authentication is the first step it verifies the identity of a user or a device trying to access the network. Without proper authentication, no further access is granted.                                                                    | Require user and device authentication before being able to connect to a network for example, handled using 802.1X  IEEE standart, to ensure that only trusted devices can join the network. Devices typically use digital certificates to prove their identity |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization  | Once the identity is verified, **authorization** determines what that user or device is permitted to do. Authorization models help enforce **least privilege** — giving users only the access they need to perform their tasks, nothing more. | - Access to specific files or applications<br>- Permission to modify settings<br>- Rights to use certain network services                                                                                                                                       |
| Accounting     | **Accounting** tracks and records activity. It keeps a detailed log of who accessed what, when, and from where. Typical accounting data includes login times, IP addresses, commands run, and resources accessed.                             | - Monitoring user behavior<br>- Troubleshooting issues<br>- Meeting compliance requirements<br>- Investigating suspicious activities                                                                                                                            |

## Some AAA protocols
AAA functions are handled by specific **protocols** that enforce these processes securely across network devices.

| Radius (Remote Authentication Dial-In User Service)             | Remote Authentication Dial-In User Service (RADIUS) is a networking protocol providing centralized Authentication, Authorization, and Accounting (AAA) for users accessing a network, handling security for dial-up, VPN, and wireless connections by verifying credentials and managing access rights between network access servers (clients) and a RADIUS server. It simplifies security by separating it from the network infrastructure, often working with databases like Active Directory for user verification. | https://datatracker.ietf.org/doc/html/rfc2865        |
| --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------- |
| Diameter                                                        | **Diameter AAA** refers to the Diameter Protocol, a crucial network protocol for **Authentication, Authorization, and Accounting (AAA)** in modern mobile and IP networks== (like LTE/4G and IMS). It acts as a next-generation, more robust replacement for RADIUS, handling user identity verification (Authentication), deciding what users can access (Authorization), and tracking resource usage (Accounting) for billing and monitoring.                                                                         | https://datatracker.ietf.org/doc/html/rfc6733#page-7 |
| TACACS+ (Terminal Access Controller Access-Control System Plus) | is a network protocol family for centralized Authentication, Authorization, and Accounting (AAA) for network devices like routers and switches, with TACACS+ being the widely used, enhanced version that separates AAA functions for granular control, security, and auditing, preventing unauthorized access and tracking user actions over TCP                                                                                                                                                                       | https://datatracker.ietf.org/doc/html/rfc1492        |
# Gap analysis
It’s a strategic tool used to compare an organization’s **current security practices** with **industry standards, regulatory requirements, and best practices.** The goal is to uncover weaknesses, or “gaps,” that need attention to strengthen the overall security posture.

| Assessment           | Start by analyzing the current environment — including policies, procedures, tools, and technical controls. This gives you a clear picture of what’s already in place.                         |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Benchmarking         | Next, compare your findings against established frameworks or standards (such as ISO 27001, NIST, or internal compliance requirements). This step helps identify what _should_ be there.       |
| Gap Identification   | This is where the real work happens: spotting the gaps between current practices and the ideal or required state. Gaps could range from missing policies to outdated tools or untrained staff. |
| Prioritization       | Not all gaps carry the same level of risk. Prioritize them based on potential impact, how likely they are to be exploited, and how quickly they need to be addressed.                          |
| Remediation Strategy | Finally, create an action plan to fix the most critical gaps. This might include implementing new tools, updating procedures, training employees, or tightening access controls.               |
Security isn’t static threats evolve, technologies change, and business needs shift. That’s why **gap analysis should be done regularly**, not just once. By repeating the process on a scheduled basis, organizations can stay aligned with current risks and maintain a strong, up-to-date security posture.
# Zero trust
Zero Trust challenges the outdated assumption that users or devices inside the network perimeter are inherently safe. Instead, it requires **continuous verification of identity and trustworthiness**, no matter where a user or system is located.

Every request — whether from a user or a device — must be:
- **Verified** (Is this really who/what it claims to be?)
- **Authorized** (Should this request be allowed?)
- **Monitored** (What is happening with this access?)

This approach reduces the chance of unauthorized access and lateral movement inside the network, even if an attacker gets through the perimeter.
## Network Parallel: Control Plane vs. Data Plane
Just like Zero Trust separates access control from assumptions of internal safety, modern networks separate **control** and **data** functions:

- The **Control Plane** handles **policy decisions**, access control, and coordination. It’s like the brain of the network.
- The **Data Plane** handles **the actual flow of traffic**, forwarding packets between systems.

![[Pasted image 20260114193125.png]]

Key components include:
- **Policy Engine:** Makes access decisions based on defined rules and live context (e.g., SIEM alerts, user behavior, device status).
- **Policy Administrator:** Enforces the decision made by the policy engine. It delivers access tokens or instructions to the system.
- **Policy Enforcement Point (PEP):** This acts as the gatekeeper. It inspects requests, verifies permissions, and allows or blocks access based on the received instructions — much like a bouncer checking your ID at the door.


| Adaptive Identity            | Traditional identity systems grant fixed permissions. But in a Zero Trust environment, identity must adapt to context. **Adaptive Identity** adjusts access rights based on factors               | - Device type and health<br>- Location<br>- Time of access<br>- Behavior patterns                           |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Threat Scope Reduction       | A core goal of Zero Trust is to **limit the attack surface**. By minimizing what's visible and accessible, organizations reduce the number of ways attackers can enter or move through a network. | - Reducing exposed services<br>- Removing unnecessary permissions<br>- Keeping systems patched and isolated |
| Policy-Driven Access Control | Rather than relying on manual approvals or basic rules, Zero Trust promotes **automated, policy-based decisions**. It ensures consistent enforcement and reduces the risk of human error.         | - Who can access what<br>- Under what conditions<br>- With what level of trust                              |
# Trust zones in network architectures
Trust zones allow organizations to classify parts of their network based on how much trust is assigned and how strict access should be.

| Implicit Trust Zone      | A network segment where systems are assumed to trust each other without needing constant re-verification. While convenient, this model can introduce risk if not tightly controlled.                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Internal Network Zone    | This includes trusted company devices behind firewalls (e.g., domain controllers, intranet servers). Often referred to as the **LAN**. While generally secure, Zero Trust recommends treating even internal users with caution.                               |
| Demilitarized Zone (DMZ) | A buffer zone between the trusted internal network and the untrusted internet. It hosts services that need to be accessed from both sides (like web servers or VPN gateways). These systems are more exposed, so they’re isolated and more tightly monitored. |
| External Network Zone    | This is the **untrusted internet** — full of unknown users and risks. Any traffic coming from this zone must go through heavy inspection, authentication, and validation before interacting with internal resources.                                          |
# Deception and Disruption Technology
these tools are designed not just to block attackers, but to confuse, slow down, and study them.

This approach shifts the advantage back to the defenders by creating traps and decoys that expose malicious activity, reveal attacker behavior, and protect real systems. Let’s take a closer look at the most common deception techniques used today.

#### **Honeypot**
A **honeypot** is a decoy system or application that mimics a real service but is isolated from the main environment. It’s intentionally left vulnerable to attract attackers.  
Security teams use honeypots to:

- Observe attack methods in real time
- Distract attackers from real assets
- Collect intelligence to strengthen defenses

For example, a fake website or server may be created to lure hackers away from the real production environment.

#### **Honeynet**
A **honeynet** is an extended version of a honeypot — a group of interconnected decoys designed to simulate an entire network.  
It provides a more realistic environment and:

- Helps researchers analyze complex attacks
- Creates confusion for attackers
- Keeps threats occupied while alerting security teams  

Think of it as a fake neighborhood that attackers think is real — while the real systems remain hidden and protected.

#### **Honeyfile**
A **honeyfile** is a fake but convincing file — often placed where an attacker is likely to look (like a desktop folder or shared drive).  
Example: A file named passwords.xlsx that contains no real data but triggers an alert when opened.

This simple trick helps:

- Detect unauthorized access
- Pinpoint an intruder’s location
- Signal a potential breach early  
#### **Honeytoken**

A **honeytoken** is a piece of fake data designed to look valuable — like a fake database record, API key, or internal credential.

When an attacker tries to use it:

- The system triggers an alert
- The source of the activity can be traced
- Investigators gain insight into where and how the attack is happening

Honeytokens can be used to monitor insider threats as well as external attackers.

#### **Fake Information**
Sometimes deception goes beyond files and tokens. Organizations may return **intentionally false data** to confuse attackers or block further reconnaissance.

Two examples include:
- **DNS Sinkholes:** When a malicious domain is requested, the DNS server redirects the request to a controlled or fake address (instead of the real target), stopping malware from connecting to command-and-control servers.  

- **Fake Telemetry:** Attackers who think they’re extracting data may actually be receiving fake logs, false system information, or useless telemetry, leading them in the wrong direction.