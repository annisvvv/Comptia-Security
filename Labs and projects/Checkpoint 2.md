Checkpoint 2:

1- Securing a web application - Access control strategies : 

A- Managerial controls : i would ensure that the daily activities with the organization overall goals and values, this by setting up policies and procedures that creates an environment where risk is manged and anticipated. some example of controls are Risk assessments to identify and evaluate potential risks and store a code of conduct that outlines the values and behavior excepted from employees. For this categories the control type is preventive (Code of conduct) and corrective (Risk assessments).

B- Operational controls : this ensure that daily task are carried according to best practices and security standards, this by in storing incident response procedures that walks through how to detect and react to problems and recover from security incidents, also training employees to recognize and respond to problems so risk are minimized, and above all controlling who has access to the server and who doesn't. For this category the control type is compensating (incident response) , detective (awareness of abnormal event), preventive (security awareness).
  
C- Technical controls : implementing software security measures to maintains the security, integrity and availability of our servers by setting firewalls, strong data encryption etc. For this category the control types are preventive (firewalls) , detective (SIEMS).

D- Physical controls : Every other security control would be useless if anyone could enter the server room so physical security should not be neglected by setting man traps, cameras, security fences, security guards, access control vestibules, bio metric locks etc. For this category the type of security control is Deterrent (warning signs) and Detective (cameras).

2- Security principles CIA tried and AAA

A- What is the CIA triad ? The CIA triad describes 3 fundamentals concept of security that are :
- confidentiality : A person can access data it doesn't have explicit authorization, this is done by encrypting messages as an example before sending them over an untrusted network as the internet.
- Integrity : that data remains unchanged and unmodified, this is done by hashing (comparing the original hash of the data to the one you have and see if there is any difference)
- Availability : That a service remain always available to access at any time and moment (we don't want our website server to go down, it would be a loss of money).

these three pillar are essential and a balance has to be done between them to ensure a healthy service.

B- what is AAA ? the AAA stands for :
- Authentication : this helps define who a person trying to access a network is. this can be applied by User and device authentication using 802.1x IEEE standard. Devices typically use digital certificates to prove their identity.
- Authorization : What are you permitted to do and access in the service, this helps enforce least privilege to give user only what they need and nothing more that would add more risk. This can be access to specific files, modify settings, and right to use certain networks.
- Accounting : After a user is in the network all his action (what, when, where) are tracked and saved. this for monitoring, troubleshooting issues etc.

3- Data confidentiality

Key management :
What is the difference between symmetric and asymmetric encryption ?  In symmetric encryption both the receiver and sender have the same key used from encryption and decryption the major problem this have is that in order for the two to have the same key, key sharing has to take place that makes the procedure unsafe if n attacker could intercept the key, however in asymmetric encryption both sender and receiver have two keys on for encrypting public key and one for decryption private key, the private one is never shared in opposite of public key that are shared. the sender receives the public key of the receiver encrypt the data send it to him and he decrypt it with his private key. 

Algorithm :
Symmetric : AES, DES
Asymmetric : RSA, Diffie hellman

utilization :
- symmetric is very fast ans used for large data encryption.
- asymmetric is very secure but slower and used for simple data sharing, like for banks.

4- Practice encryption with Cyberchef

![](../zzfiles/Pasted%20image%2020260131220255.png)

key : encryptionkey002
IV : keyofencryption1
input : you have been hacked
output : 30481cf7c9b4303af9558c2f06360ab263d77f325b79937a9cf860310a7b85cf

the HTML i used for index.html :
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hash Display</title>
    <style>
        body {
            background: linear-gradient(135deg, #667eea, #764ba2);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .hash-container {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            padding: 40px 60px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            backdrop-filter: blur(10px);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .hash-container:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        }

        h1 {
            margin-bottom: 20px;
            font-size: 2rem;
            letter-spacing: 2px;
        }

        .hash {
            font-family: 'Courier New', Courier, monospace;
            font-size: 1.2rem;
            word-break: break-all;
            background: rgba(255, 255, 255, 0.2);
            padding: 15px 20px;
            border-radius: 10px;
            display: inline-block;
            user-select: all;
        }
    </style>
</head>
<body>
    <div class="hash-container">
        <h1>Your Hash</h1>
        <div class="hash">
            30481cf7c9b4303af9558c2f06360ab263d77f325b79937a9cf860310a7b85cf
        </div>
    </div>
</body>
</html>
```

starting the web server :
```
ubuntu@ubuntu:~$ sudo /opt/lampp/lampp start
Starting XAMPP for Linux 8.2.12-0...
XAMPP: Starting Apache...already running.
XAMPP: Starting MySQL...already running.
XAMPP: Starting ProFTPD...already running.
```

accessing it at the server ip :
```
http://192.168.122.8/index.html
```

![](../zzfiles/Pasted%20image%2020260131221627.png)

5- what is Steganography ? Steganography is the practice of concealing information. It involves hiding data within an ordinary, non-secret file or message to prevent detection. The hidden information is being extracted at the receiving end. it can be done inside pictures, files etc.

Difference between encryption and steganography : Encryption transforms data into an unreadable format using mathematical algorithms and keys, making the content incomprehensible to anyone without the decryption key everyone can see that encrypted data exists, it just appears as gibberish or ciphertext, and the focus is entirely on protecting the confidentiality of the message content itself. Steganography, on the other hand, conceals the very existence of secret data by hiding it within innocent-looking file like images, audio, or video, the hidden message remains completely invisible to casual observers who only see the normal looking cover file, and the goal is to avoid drawing any attention or suspicion that secret communication is even taking place.

Defenders embed invisible watermarks or digital fingerprints in sensitive documents, images, and intellectual property to track leaks and identify the source of data breaches when confidential information appears externally. Security teams use steganographic techniques to hide honeytokens or canary data within files and databases, which trigger alerts when accessed or exfiltrated, helping detect insider threats and unauthorized access attempts while the attackers remain unaware they've been detected.

Attackers embed malicious payloads, command-and-control communications, or stolen data inside innocent-looking files to evade detection by security tools that scan for suspicious network traffic or malware signatures. They hide malware executables within image files on compromised websites, so when victims download what appears to be a harmless picture, they're actually getting infected with hidden malicious code that traditional antivirus software might miss.

6- Hide secret using Steghide

using this picture :
![](../zzfiles/images.jpeg)

using this command :
![](../zzfiles/Pasted%20image%2020260131225711.png)
![](../zzfiles/Pasted%20image%2020260131225248.png)

output:
![](../zzfiles/images%201.jpeg)

reverse operation :
![](../zzfiles/Pasted%20image%2020260131225656.png)

7- Serve the Steganographic Image via XAMPP

i will send the picture to the xampp VM `/opt/lampp/htdocs/`, then modify the index.html to add the index.jpeg :
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hash Display</title>
    <style>
        body {
            background: linear-gradient(135deg, #667eea, #764ba2);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .container {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            padding: 30px 50px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            backdrop-filter: blur(10px);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .container:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        }

        h1 {
            margin-bottom: 10px;
            font-size: 2rem;
            letter-spacing: 2px;
        }

        .name {
            font-size: 1.5rem;
            margin-bottom: 20px;
            font-weight: bold;
            color: #ffd700; /* golden color to make it stand out */
            letter-spacing: 1px;
        }

        .hash {
            font-family: 'Courier New', Courier, monospace;
            font-size: 1.2rem;
            word-break: break-all;
            background: rgba(255, 255, 255, 0.2);
            padding: 15px 20px;
            border-radius: 10px;
            display: inline-block;
            user-select: all;
            margin-bottom: 20px;
        }

        .image-container img {
            max-width: 100%;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Your Hash</h1>
        <div class="name">Nasri Anis</div>
        <div class="hash">
            30481cf7c9b4303af9558c2f06360ab263d77f325b79937a9cf860310a7b85cf
        </div>
        <div class="image-container">
            <img src="index.jpeg" alt="Your Image">
        </div>
    </div>
</body>
</html>
```

then start the server :
```
ubuntu@ubuntu:/opt/lampp/htdocs$ sudo /opt/lampp/lampp start
Starting XAMPP for Linux 8.2.12-0...
XAMPP: Starting Apache...ok.
XAMPP: Starting MySQL...ok.
XAMPP: Starting ProFTPD...ok.
```

we get :
![](../zzfiles/Pasted%20image%2020260131230933.png)
