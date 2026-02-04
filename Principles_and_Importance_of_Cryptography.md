# Cryptography Basics for Cybersecurity

Cryptography is the science and engineering of protecting information using mathematics and keys. It transforms readable data (plaintext) into an unreadable form (ciphertext) so that only authorized parties can access, verify, or prove actions related to that data. 
In cybersecurity, cryptography is a foundational building block: it secures web traffic, protects stored data, enables secure logins, and underpins digital signatures, cryptocurrencies, and secure software updates. 

---

## Core Objectives of Cryptography
Classical modern cryptography is usually described in terms of four core security objectives (often called “security services”). 
### 1. Confidentiality
Confidentiality means only authorized parties can read the information.
Even if an attacker intercepts or steals the data, they should see only unintelligible ciphertext.
-	Achieved primarily through encryption (symmetric algorithms like AES, asymmetric algorithms like RSA/ECC).
-	Used to protect web traffic (HTTPS), VPN tunnels, disk encryption, messaging apps, and stored database records. 
### 2. Integrity
Integrity means data has not been modified accidentally or maliciously between creation and use.
-	Achieved via cryptographic hash functions (e.g., SHA 256) and Message Authentication Codes (MACs), or via digital signatures. 
-	If the received data’s hash/MAC doesn’t match the expected value, the system detects tampering.
-	Used in software update verification, file integrity checks, log protection, and blockchain data structures. 
### 3. Authentication
Authentication answers “Who are you?” or “Where did this data really come from?”
-	Achieved with passwords + secure channels, digital certificates (PKI), challenge response protocols, hardware tokens, and digital signatures. 
-	In protocols like TLS, the server proves its identity using a certificate signed by a trusted Certificate Authority (CA).
-	At the application level, digital signatures prove that a message or document originates from a particular key (and thus identity). 
### 4. Non Repudiation
Non-repudiation ensures a party cannot credibly deny a specific action later, such as sending a message, signing a contract, or authorizing a transaction.
-	Achieved primarily using digital signatures on messages or documents, often combined with timestamps and secure logs. 
-	If a contract is digitally signed with Alice’s private key and verified via her certificate, she cannot later deny having signed it (assuming her key was properly protected). 
Together, these four properties—confidentiality, integrity, authentication, and non-repudiation—define the main goals cryptography tries to provide in secure systems. 

---

## How Cryptography Protects Data in Transit and at Rest
Cryptography is applied differently depending on the “state” of the data: in transit, at rest, and (to a more limited extent) in use. 
### Data in Transit
Data in transit is any data moving across a network (e.g., browser ↔ server, client ↔ API, remote VPN client ↔ corporate gateway). 
Cryptography protects data in transit by:
-	Encrypting the communication channel so eavesdroppers see only ciphertext (e.g., TLS, SSH, IPsec). 
-	Authenticating endpoints using certificates or keys (e.g., the browser verifies the real bank website via an X.509 certificate chain). 
-	Providing integrity with MACs or AEAD modes (like AES GCM), so any tampering in transit is detected and rejected. 
Typical mechanisms and examples:
-	TLS/SSL (HTTPS) – protects HTTP traffic between browsers and web servers. 
-	SSH – secure remote login and tunnelling for system administration. 
-	VPN protocols (IPsec, WireGuard, OpenVPN) – encrypt and authenticate all traffic between sites or remote clients and corporate networks. 
### Data at Rest
Data at rest is stored data: disks, SSDs, USB drives, database tables, backups, and cloud object storage. 
Cryptography protects data at rest by:
-	Encrypting storage media so physical theft or unauthorized copies don’t expose plaintext.
-	Separating keys from data, so stealing disks alone is insufficient to read information. 
Common approaches:
-	Full disk/volume encryption (BitLocker, LUKS, FileVault, self-encrypting drives) using AES. 
-	Database and file-level encryption, sometimes with encryption at the application layer for especially sensitive columns (e.g., card numbers, health data). 
-	Encrypted backups and archives, so off-site media and cloud backups remain confidential. 
Note: encryption at rest usually protects against offline attackers (lost/stolen devices, copied disks), not against a fully compromised OS that already has access to unlocked keys. 
### Data in Use 
Data in use is being processed in RAM or CPU registers and is usually in plaintext, even if encrypted at rest and in transit. 
Emerging techniques help reduce risk here:
-	Trusted Execution Environments (TEE) – e.g., Intel SGX, AMD SEV, ARM TrustZone: isolate sensitive computations in enclaves with hardware level protections. 
-	Homomorphic encryption / secure multi-party computation – allow limited computation on encrypted data without fully decrypting it (still mostly niche/advanced). 

---

# Real World Use Cases of Cryptography
Cryptography appears in almost every modern digital system. Some of the most important real-world use cases are:
## 1. Secure Web Browsing (HTTPS / TLS)
What: HTTPS uses TLS to encrypt HTTP traffic between browsers and web servers. 

How:
-	Asymmetric cryptography (certificates, key exchange) to authenticate the server and agree on a session key.
-	Symmetric cryptography (e.g., AES GCM, ChaCha20 Poly1305) to encrypt the actual data.
-	MAC/AEAD tags for integrity. 
Why: Protects login credentials, cookies, payment details, personal data, and API calls from eavesdropping and tampering. 
## 2. Virtual Private Networks (VPNs)
What: VPNs create encrypted tunnels over untrusted networks. 

How: IPsec, WireGuard, and OpenVPN use symmetric ciphers (AES or ChaCha20), authentication, and key exchange to protect traffic between endpoints. 

Why: Secure remote work, protect internal services, bypass hostile networks, and mitigate traffic analysis to some extent. 
## 3. Password Protection
What: Passwords are not stored in plaintext; they’re processed using hashing (often with salts and slow KDFs like bcrypt, scrypt, Argon2). 

How:
-	System stores hash (password + salt) instead of the password itself.
-	On login, it recomputes the hash and compares.
-	Why: If the user database is breached, attackers must still brute force each hash rather than reading passwords directly. 
## 4. Digital Signatures and Software Integrity
What: Operating systems and app stores verify that software updates and packages are signed by trusted vendors. 

How:
-	Vendor uses its private key to sign a hash of the update.
-	The user’s system uses the vendor’s public key to verify the signature.

Why: Prevents attackers from distributing malicious updates that appear legitimate.

Digital signatures are also used in:
-	Electronic contracts and e-signing platforms for legal non-repudiation.
-	Secure email (PGP, S/MIME) to authenticate senders and protect integrity. 
## 5. Encrypted Messaging and End-to-End Encryption
What: Apps like Signal, WhatsApp, and others use end-to-end encryption (E2EE) to protect messages. 

How:
- Messages are encrypted on the sender’s device and only decrypted on the receiver’s device.
- Servers can store and forward ciphertext, but cannot read content.

Why: Ensures private conversations even if the network, servers, or storage are compromised. 
## 6. Disk and Database Encryption
What: Full disk encryption (BitLocker, FileVault, LUKS) and Transparent Data Encryption (TDE) for databases. 

How: Use symmetric ciphers (typically AES) with keys tied to user credentials or hardware security modules. 

Why: Protects data on lost/stolen devices, discarded disks, or unauthorized low level access to storage. 
## 7. Cryptocurrencies and Blockchain
What: Bitcoin, Ethereum, and other blockchains rely heavily on cryptography

How:
- Hash functions (e.g., SHA-256) to link blocks and secure transaction data.
- Digital signatures (ECDSA, EdDSA) to prove ownership of addresses and authorize transactions. 

Why: Prevents double-spending, ensures ledger integrity, and enforces ownership without a central authority. 

---

# Why Cryptography Is Important in Cybersecurity
Cryptography is not just one security control; it is embedded into almost every other security mechanism. Its importance in cybersecurity comes from several key roles. 
## 1. Foundation for Confidentiality and Privacy
Without encryption, most internet traffic, stored data, and digital communications would be readable to anyone with access to the underlying network or storage. Cryptography:
-	Protects sensitive personal information (credentials, personal data, health records).
-	Secures business secrets, intellectual property, and strategic communications.
-	Enables privacy-respecting services and compliance with regulations like GDPR by enforcing data protection at the technical level. 
## 2. Ensuring Data Trustworthiness (Integrity + Authenticity)
Security is not just about keeping secrets; it is also about trusting that what you see is correct and from the right source.
-	Hashes, MACs, and digital signatures ensure that data has not been altered in transit or at rest.
-	Digital certificates and signature schemes bind keys to identities, enabling strong authentication of systems and users.
-	This underpins secure software supply chains, safe web browsing, trustworthy configuration management, and reliable logs
## 3. Enabling Secure Architectures and Protocols
Modern security protocols are essentially carefully structured cryptographic constructions:
-	TLS, SSH, IPsec, and secure messaging protocols use combinations of symmetric encryption, public key cryptography, and hash/MAC functions to build secure channels.
-	VPNs, Zero Trust architectures, and SSO systems rely on cryptographic tokens, assertions, and certificates to control and monitor access across distributed systems. 
As a cybersecurity practitioner, understanding cryptography at a conceptual level is essential to:
-	Correctly configure and audit these protocols.
-	Recognise weak algorithms and misconfigurations (e.g., deprecated ciphers, small keys).
-	Avoid design flaws like key reuse, insecure modes, or missing integrity protection.
## 4. Defense Against Evolving Cyber Threats
Attackers constantly seek to intercept, modify, or forge data. Cryptography helps defend against:
-	Eavesdropping (sniffing cleartext credentials or sensitive data).
-	Data breaches (leaked databases or lost devices exposing sensitive information).
-	Man in the middle attacks (spoofing endpoints and injecting malicious content).
-	Ransomware and extortion (protecting backups and sensitive archives).
-	Supply chain attacks (fake updates, tampered binaries). 
While cryptography cannot solve every security problem by itself, no serious cybersecurity strategy can exist without robust cryptographic controls.
## 5. Building Trust in Digital Systems
Ultimately, cybersecurity is about enabling safe and trustworthy digital interactions. Cryptography supports this by:
-	Providing technical guarantees about who can see what, who did what, and whether something has been altered.
-	Allowing organizations and individuals to rely on digital processes (online banking, e‑government, e‑commerce, remote work) with confidence.
- Forming the mathematical backbone for identity systems, secure payments, digital contracts, and privacy‑preserving technologies
