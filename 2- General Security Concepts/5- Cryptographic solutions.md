# Encryption

| Crypto solution       | How it works                                                                                                                                                                                                                                                                                                                  | Pros                                                                                                                                                                                                                        | Cons                                                                                                                                                                                                                                                       | Keys                                                                                                      | Algorythms / use cases                | Key size                              |                                                                                                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symmetric Encryption  | - A **cipher** is chosen — an algorithm that performs the transformation.  <br>- A **secret key** is agreed upon by both parties.<br>- The sender encrypts the **plaintext** using the cipher and the key.<br>- The receiver uses the **same key** and cipher to decrypt the **ciphertext** and recover the original message. | - Very fast<br>- Efficient for large data<br>- Hard to securely share the key                                                                                                                                               | - Key sharing                                                                                                                                                                                                                                              | only a secret key                                                                                         | DE                                    | 56 bits                               | Outdated and insecure; replaced due to being easily cracked                                                                                                   |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            |                                                                                                           | 3DES                                  | 112–168 bits                          | An improvement over DES; deprecated since 2019                                                                                                                |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            |                                                                                                           | AES                                   | 112–168 bits                          | Fast, secure, and the current industry standard                                                                                                               |
| Asymmetric Encryption | While symmetric encryption secures data with **one shared secret key**, asymmetric encryption—also called **public-key cryptography**—uses **two mathematically related keys**<br><br>1. **Key generation** <br>2. **Key distribution**<br>3. **Confidential message**                                                        | - **Solves key-distribution problem**—public key can be shared freely.<br>- Enables **authentication** and **non-repudiation** (digital signatures).<br>- Forms the basis of key-agreement protocols (e.g., TLS handshake). | - **Slower** than symmetric algorithms; inefficient for large files or high-volume traffic.<br>- Ciphertext size is limited to (or slightly less than) the key size.<br>- Still depends on secure private-key storage; loss or theft compromises security. | **Public key**<br><br>Encrypts data or verifies a digital signature<br><br>Meant to be shared with anyone | **RSA**                               | 2 048 bits (min) – 3 072 / 4 096 bits | Most common public-key system; relies on integer-factorization hardness                                                                                       |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            | **Private key**<br><br>Decrypts data or creates a digital signature<br><br>Must remain secret             | **Diffie-Hellman**                    | 2 048 bits (min) – 3 072 / 4 096 bits | Used for secure key exchange rather than direct encryption                                                                                                    |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            |                                                                                                           | **Elliptic Curve Cryptography (ECC)** | 256 bits (min) – 384 / 521 bits       | Provides RSA-level security with far shorter keys, reducing bandwidth and CPU load                                                                            |
| Hybrid Encryption     | 1. **Key Generation**<br>2. **Public Key Distribution**<br>3. **Session Key Creation**  <br>4. **Key Encryption**<br>5. **Key Decryption**<br>6. **Data Encryption**                                                                                                                                                          | Combine pros of symmetric with asymmetric                                                                                                                                                                                   |                                                                                                                                                                                                                                                            |                                                                                                           | **TLS/SSL (HTTPS)**                   |                                       | Uses asymmetric encryption during the handshake to securely exchange symmetric session keys. Data is then encrypted using symmetric encryption (usually AES). |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            |                                                                                                           | **PGP/GPG (secure email)**            |                                       | Encrypts the symmetric key with the recipient’s public key. The message body is encrypted symmetrically.                                                      |
|                       |                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                            |                                                                                                           | **VPN protocols (e.g., IKE/IPsec)**   |                                       | Exchange symmetric keys using Diffie-Hellman or ECC, then secure traffic with symmetric ciphers.                                                              |
# Hashing
In cybersecurity, **hash functions** are foundational tools used to ensure **data integrity** and protect **passwords**. A hash transforms any input — a sentence, a file, or even an entire hard drive — into a **fixed-length string of characters** called a **hash value** or **digest**.

But here’s the catch:  
Hashing is **one-way**.  
You can convert data _into_ a hash, but you cannot reverse the process to recover the original input.

ashing relies on specific cryptographic properties:

| **Property**             | **Description**                                                                      |
| ------------------------ | ------------------------------------------------------------------------------------ |
| **Fixed Output Length**  | No matter how large or small the input is, the hash has a consistent length.         |
| **One-Way Function**     | You cannot reverse a hash to retrieve the original data.                             |
| **Collision Resistance** | It is extremely unlikely that two different inputs will produce the same hash value. |
| **Deterministic**        | The same input always generates the same hash value (if using the same algorithm).   |
Popular hashing algorithms include:

|               |                 |                                                                           |
| ------------- | --------------- | ------------------------------------------------------------------------- |
| **Algorithm** | **Digest Size** | **Notes**                                                                 |
| **MD5**       | 128 bits        | Fast but no longer considered secure; may still be used for compatibility |
| **SHA-1**     | 160 bits        | Also broken; not recommended                                              |
| **SHA-256**   | 256 bits        | Secure and widely used today (part of the SHA-2 family)                   |
### **Real-World Uses**
1. Verifying File Integrity
2. Password Storage
### Salting
While hashing helps secure passwords, it’s still vulnerable to **rainbow table attacks** (precomputed hash lookup attacks). That’s where **salting** comes in.
**Salting** is the process of adding a **random string** (called a salt) to a password **before** hashing it.
This makes every password hash **unique**, even if two users choose the same password.

**Example:**
- Password: Gomycode123
- Salt: 8rTz!xQ4
- Combined: Gomycode1238rTz!xQ4 → then hashed

Even if hackers know the hash of Gomycode123, the added salt ensures it won’t match unless the salt is also known.
### **HMAC (Hash-Based Message Authentication Code)**
While hashing ensures **integrity**, it doesn’t verify **authenticity** — that’s where **HMAC** comes in. An **HMAC** is a special type of hash that uses **a secret key along with the data**. It ensures:
- The data has **not been modifie**
- The data came from a **trusted source**

**Common use cases**: API authentication, TLS handshakes, digital signatures.
### **Key Stretching**
While salting protects passwords from rainbow table attacks, **key stretching** is used to make brute-force and dictionary attacks **computationally expensive**.
Key stretching transforms a short, possibly weak password into a **stronger cryptographic key** by **repeating hashing operations thousands of times**. This makes it take significantly longer for an attacker to guess a password — even with powerful hardware.
#### **Techniques for Key Stretching**
- **PBKDF2 (Password-Based Key Derivation Function 2)**  
    Applies a hash function thousands of times with a salt. Commonly used in secure password storage and encryption key generation.
- **Bcrypt**  
    Specifically built for password hashing. It adds salting and automatically increases its workload over time (configurable with a "cost" factor).
# Digital signatures
In the digital world, just like signing a paper contract proves authorship and agreement, **digital signatures** serve as the **electronic equivalent** of a handwritten signature. But rather than using ink, they use **cryptography** to ensure:

- **Integrity** — the data wasn’t altered
- **Authentication** — the sender is who they claim to be
- **Non-repudiation** — the sender can’t later deny sending the message

A digital signature combines **hashing** and **asymmetric encryption**. Here’s a simplified step-by-step process using RSA:

1. **Hashing the message**:  
    The sender (Alice) runs a **hash function** (e.g., SHA-256) on the message to generate a **digest**.  
    
2. **Encrypting the digest**:  
    Alice **encrypts the digest** using her **private key**. This encrypted hash becomes the **digital signature**.  
    
3. **Attaching the signature**:  
    Alice sends both the **original message** and the **digital signature** to the recipient (Bob).  
    
4. **Verification**:
    - Bob uses Alice’s **public key** to **decrypt** the signature and recover the hash.
    - He also hashes the original message himself using the same algorithm.
    - If the two digests match, the message is **authentic** and **unaltered**.

Key Points :

- **The message itself is not encrypted** — it passes in cleartext.  
- The **private key signs** (encrypts the hash), and the **public key verifies**.  
- If someone tampers with the message, the hash won’t match.  
- This process ensures that only Alice (the private key holder) could have created the signature.

|   |   |
|---|---|
|**Feature**|**Description**|
|**Integrity**|Confirms that the data has not been modified during transmission|
|**Authentication**|Confirms the identity of the sender (via their private key)|
|**Non-repudiation**|Prevents the sender from denying they sent the message|

|   |   |
|---|---|
|**Algorithm**|**Notes**|
|**RSA**|Uses the sender’s private key to sign a hash of the message|
|**DSA** (Digital Signature Algorithm)|Based on **Elliptic Curve Cryptography (ECC)**; widely used in modern secure systems (e.g., SSH, TLS)|

To prevent forgery or impersonation, the recipient must **validate** that the public key actually belongs to the sender — usually done using a **digital certificate**, which we’ll cover next.
# Digital certificate

# Note
digital signature are made to verify that the sender is legitimate, and certificate that the receiver is legitimate.