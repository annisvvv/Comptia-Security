That’s where **cryptographic solutions** come in. They form the **foundation of modern data protection**, helping organizations and individuals keep their information **confidential, accurate, and trustworthy**.

In this Superskill, you’ll explore a range of cryptographic technologies and how they support secure communication and data handling. We’ll cover:

- **Public Key Infrastructure (PKI)** – including public/private keys, certificates, and key escrow
- **Encryption techniques** – such as full-disk, file, and database encryption
- **Hardware security tools** – like **TPMs** (Trusted Platform Modules) and **HSMs** (Hardware Security Modules)
- **Hashing, digital signatures, and obfuscation**
- **Key management practices**
- The role of **blockchain** and **certificate authorities (CAs)** in decentralized trust

Understanding how and when to apply these tools is essential for building **secure systems**. Cryptography doesn’t just protect data — it also proves identities, validates integrity, and supports trust in everything from websites to smart contracts.
# Cryptographic concepts 

**Plaintext:** The original, readable message or data **before encryption.**  
It can be any type of information: text, documents, images, video files, or structured records — anything that needs protection.

---
**Ciphertext:** The **scrambled** **output** of the encryption process.  
Ciphertext should be unreadable to anyone who does not have the proper key. It provides no useful information about the plaintext — other than its approximate size.

---
**Cipher:** A **mathematical** **algorithm** that transforms plaintext into ciphertext and back. The cipher defines the encryption logic, but **not** **the** **key**. Well-known ciphers include **AES**, **RSA**, and **ChaCha20**.

Ciphers are public knowledge, but they rely on secret keys to stay secure.

---
**Key:** A unique **string** **of** **bits** used by a cipher to perform encryption and decryption.

In symmetric encryption, the same key is used to encrypt and decrypt.

In asymmetric encryption, different keys are used (public/private).

The key must be kept **secret** (except in public key systems where the public key is meant to be shared).

---
**Encryption:** The process of **transforming plaintext into ciphertext** using a cipher and a key. This is done to protect the confidentiality of the message. Encryption is **reversible** — but only if the correct key is used.

---
**Decryption:** The **reverse of encryption** — converting ciphertext back into readable plaintext using the same (or corresponding) key.  
A strong cipher ensures that decryption is **infeasible without the key**, even if the cipher itself is public.

---
Now, let’s say we want to protect that plaintext from being seen by unauthorized people. Here's what happens next:

1. The **plaintext** is passed into an **encryption function**.
2. This function uses a **cipher** (an encryption algorithm) and a **key** (a secret value).
3. The output is an unreadable block of data called **ciphertext**.

To get the original message back, we reverse the process:

4. We take the **ciphertext** and run it through a **decryption function**, again using the correct **key**.
5. This restores the original **plaintext**, assuming the key is valid.
# Cryptographic solutions
Modern cryptographic protection is built around four key areas:

| **Encryption**           | Uses algorithms and keys to transform plaintext into unreadable ciphertext. It includes symmetric and asymmetric techniques. |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **Hashing**              | Converts data into a fixed-length value (hash) used to ensure integrity.                                                     |
| **Digital Signatures**   | Prove message authenticity and integrity using asymmetric encryption.                                                        |
| **Digital Certificates** | Provide identity assurance in secure communications, typically via Public Key Infrastructure (PKI).                          |
# Stream cipher and block cipher

| Stream Ciphers | In a **stream cipher**, each byte or bit of data in the plaintext is encrypted one at a time. This is suitable for encrypting communications where the total length of the message is not known. The plaintext is combined with a separate randomly generated message, calculated from the key and an initialization vector (IV). The IV ensures the key produces a unique ciphertext from the same plaintext. The keystream must be unique, so an IV must not be reused with the same key. The recipient must be able to generate the same keystream as the sender and the streams must be synchronized. Stream ciphers might use markers to allow for synchronization and retransmission. Some types of stream ciphers are made self-synchronizing. |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Block Ciphers  | In a **block cipher**, the plaintext is divided into equal-size blocks (usually 128-bit). If there is not enough data in the plaintext, it is padded to the correct size using some string defined in the algorithm. For example, a 1200-bit plaintext would be padded with an extra 80 bits to fit into 10 x 128-bit blocks. Each block is then subjected to complex transposition and substitution operations, based on the value of the key used.                                                                                                                                                                                                                                                                                                  |
| Key Length     | The range of key values available to use with a particular cipher is called the keyspace. The keyspace is roughly equivalent to two to the power of the size of the key. Using a longer key (256 bits rather than 128 bits, for instance) makes the encryption scheme stronger. You should realize that key lengths are not equivalent when comparing different algorithms, however. Recommendations on minimum key length for any given algorithm are made by identifying whether the algorithm is vulnerable to cryptanalysis techniques and by the length of time it would take to "brute force" the key, given current processing resources.                                                                                                      |
# Cryptoprocessors and Key Management
To support strong cryptography, organizations rely on secure hardware and backup mechanisms to store and manage keys. Let’s look at the most common ones:


| Trusted Platform Module (TPM)  | - A **TPM** is a cryptographic processor embedded in a computer’s motherboard or CPU.<br>- It stores and protects encryption keys, certificates, and passwords.<br>- TPMs are used to secure boot processes and enable full-disk encryption tools like BitLocker.<br>- They are **hardware-isolated**, helping protect against software-based attacks.                                                                                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hardware Security Module (HSM) | - An **HSM** is a dedicated, tamper-resistant hardware appliance or virtual solution used to securely generate, store, and manage cryptographic keys.<br>- HSMs are ideal for enterprise use, especially in data centers, PKI systems, and cloud environments.<br>- Often used to manage keys for applications, digital signing, or high-volume encryption workloads.                                                                                                                                      |
| Secure Enclave                 | - Apple’s **Secure Enclave** is an isolated hardware subsystem built into its SoCs (Systems on Chip).<br>- It stores biometric data, passwords, and cryptographic keys separate from the main processor.<br>- Even if the OS kernel is compromised, the Secure Enclave helps keep sensitive data safe.                                                                                                                                                                                                     |
| Key Escrow                     | Key escrow is the practice of **backing up encryption keys** with a trusted third party. This ensures that data can be recovered in case the original keys are lost or corrupted.<br><br>- Keys are archived and stored securely, typically by a security team or external provider.<br>- **M-of-N control**: A method where recovery requires a minimum number (M) of authorized individuals out of a larger group (N).  <br>      <br>    Example: 3 of 5 key holders must agree to unlock a backup key. |
# Encryption application


| Full-Disk Encryption (FDE)         | - Encrypts the entire storage device (HDD or SSD).<br>- Prevents data access without the correct key, even if the drive is physically stolen.<br>- Often enhanced using **TPM** for key protection.<br>- **Self-encrypting drives (Opal standard)** and tools like **VeraCrypt** offer robust disk-level protection. |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| File Encryption                    | - Encrypts individual files (e.g., Word docs, images).<br>- Only users with the correct key or profile can open them.<br>- Example: **Windows EFS (Encrypted File System)** — stores keys in user profiles.                                                                                                          |
| Volume Encryption                  | - Encrypts an entire partition or logical volume (not the full disk).<br>- **BitLocker** combined with **TPM** is a common implementation in Windows environments.<br>- Protects against data theft if a drive is removed and connected to another machine.                                                          |
| Database Encryption                | - Applies encryption to entire databases or specific fields.<br>- Protects sensitive records like financial data or customer PII.<br>- Supports compliance with data protection laws like GDPR or HIPAA.                                                                                                             |
| Record-Level Encryption            | - Encrypts individual records within a database.<br>- Each record may use its own key — increasing granularity and control.<br>- Useful for high-security systems like financial apps, healthcare platforms, or classified data repositories.                                                                        |
| Transport/Communication Encryption | - Protects data **in motion** (e.g., between client and server).<br>- **TLS (Transport Layer Security)** is the most common protocol, replacing SSL.<br>    - Used in **HTTPS**, **VPNs**, **email**, **VoIP**, and more.<br>- Ensures secure sessions by encrypting traffic and validating server identity.         |
# Encryption in practice
Before diving deeper into modern encryption methods, it’s helpful to look back at one of the earliest known ciphers — the **Caesar Cipher**, named after Julius Caesar, who reportedly used it to protect military messages.

---

#### **How It Works**

The Caesar Cipher is a **substitution cipher** that shifts each letter in the alphabet by a fixed number of positions. This number is called the **key**.

Let’s walk through a simple example:

- **Plaintext**: GOMYCODE
- **Key**: 3 (Shift each letter **right** by 3 places)
- **Cipher**: Caesar Cipher

So, the resulting **ciphertext** is:  
JRPBFRGH

---

**Decryption**

To decrypt, we reverse the operation:

- **Ciphertext**: JRPBFRGH
- **Key**: 3
- **Direction**: Shift **left** by 3 places  

This brings us back to the original message:  
GOMYCODE

---

#### **Why Caesar Cipher Is Insecure**

While the Caesar Cipher may have been effective in ancient times, it is **trivially breakable today** for one major reason; It only has **25 possible keys** (a full rotation of 26 brings the alphabet back to its original state).

This means that an attacker can easily perform a **brute-force attack** — trying all 25 keys — to uncover the original message.

In fact, tools exist that automatically test every possible key and detect readable English text, often in seconds.