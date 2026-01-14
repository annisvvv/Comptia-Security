These are the foundation of modern cyber-security
# The CIA triad
this is the core model that guides how we protect systems and information

- C : Confidentiality
- I : integrity
- A : Availability

this outlines the key principles that every secure system should be built upon, this ensure the perfect equilibrium between protection, reliability, and ease of access.

a weakness in one area can compromise the others.

- Confidentiality is all about keeping information private. It ensures that only authorized individuals can access sensitive data — whether it’s personal records, business documents, or internal communications. Techniques like encryption, access control, and secure authentication are commonly used to protect confidentiality and keep prying eyes out.
- Integrity ensures that information remains accurate and unaltered. Whether data is being stored or transmitted, it must stay complete and trustworthy. Mechanisms like hashing (e.g., SHA-256, SHA-1) are often used to verify that data hasn’t been tampered with or corrupted during transit or storage.
- Availability means that information and systems are accessible when needed. Even the most secure data is useless if users can’t access it. To maintain availability, organizations rely on strategies like redundancy, system monitoring, backups, and disaster recovery planning.
# Non repudiation
Non-repudiation is the assurance that someone cannot deny having performed an action, this ensures accountability. (log utilization)
# Authentication, Authorization, and Accounting
this is the AAA model, this ensure secure management of who access to systems and resources and hat they are allowed to do.

AAA is often implemented using dedicated servers and protocols that manage user and device interactions.
### Authentication
Authentication is the first step — it verifies the identity of a user or a device trying to access the network. Without proper authentication, no further access is granted.

examples:
Require user and device authentication before being able to connect to a network for example, handled using 802.1X  IEEE standart, to ensure that only trusted devices can join the network. Devices typically use digital certificates to prove their identity.