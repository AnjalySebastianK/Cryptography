# Overview
Digital signatures are a core component of modern cybersecurity.  
They provide a cryptographic way to ensure:
- **Authenticity** — the message truly comes from the claimed sender  
- **Integrity** — the message has not been altered  
- **Non‑repudiation** — the sender cannot deny sending the message  

This document explains:
1. What digital signatures are  
2. How hashing + asymmetric encryption work together  
3. The full signing and verification process  
4. Real‑world applications  

---

# 1. What Are Digital Signatures?

Digital signatures are the digital equivalent of handwritten signatures, but far more secure.  
They rely on **public‑key cryptography** and **cryptographic hash functions**.

## Purpose of Digital Signatures

### ✔ Authenticity
Ensures the message was created by the legitimate sender.

### ✔ Integrity
Ensures the message was not modified during transmission.

### ✔ Non‑Repudiation
The sender cannot later claim “I didn’t send this.”

Digital signatures achieve these goals using:
- A **private key** (kept secret by the signer)
- A **public key** (shared with everyone)
- A **hash function** (SHA‑256, SHA‑3, etc.)

---

## 2. How Digital Signatures Work Internally

Digital signatures combine **hashing** and **asymmetric encryption**.

### 2.1 Hashing
A hash function takes a message and produces a fixed‑size output.

Example: `H = Hash(message)`

Properties:
- One‑way (cannot reverse it)
- Small changes → completely different hash
- Fast to compute

### 2.2 Asymmetric Encryption
Uses a **key pair**:
- Private key → used to sign  
- Public key → used to verify  

The private key encrypts the hash to create the signature.

---

## 3. Digital Signature Process (Step-by-Step)

### Step 1: Hash the Message
`H = Hash(message)`

### Step 2: Encrypt the Hash with the Private Key
`Signature = Encrypt_private(H)`

### Step 3: Send:
- The original message
- The digital signature

## Step 4: Verification (Receiver Side)
1. Receiver hashes the message again:

`H1 = Hash(received_message)`

2. Receiver decrypts the signature using the sender’s public key:

`H2 = Decrypt_public(Signature)`


3. Compare:

If `H1 == H2 → Signature is valid`

Else → `Message was tampered or sender is not authentic`

---

## 4. Digital Signature Flow (ASCII Diagram)
´´´
## Digital Signature Flow (ASCII Diagram)

                SENDER (Signing)
        +--------------------------------+
        |        Original Message        |
        +--------------------------------+
                     |
                     v
              Hash Function (SHA-256)
                     |
                     v
              Hash of Message (H)
                     |
                     v
     Encrypt Hash with PRIVATE KEY
                     |
                     v
            Digital Signature (S)
                     |
                     v
                    Send

```
Send: [Message] + [Signature]

```

                RECEIVER (Verification)
                     |
                     v
        Hash received message → H1
                     |
                     v
     Decrypt signature with PUBLIC KEY → H2
                     |
                     v
          Compare H1 and H2
                     |
                     v
     If equal → Authentic + Untampered


---

## 5. Real‑World Applications of Digital Signatures

### ✔ Software Signing
Used by:
- Microsoft  
- Apple  
- Linux package maintainers  

Purpose:
- Ensure software updates are genuine  
- Prevent malware from impersonating legitimate software  

Example:

Windows .exe and .msi files contain embedded digital signatures


---

### ✔ Email Verification (S/MIME, DKIM)
Digital signatures ensure:
- The email truly came from the sender  
- The content was not modified  

DKIM (DomainKeys Identified Mail) signs outgoing emails using a domain’s private key.

---

### ✔ Legal Documents & Contracts
Digital signatures are legally recognized in many countries.

Used in:
- E‑contracts  
- Government forms  
- Banking documents  
- HR onboarding  

They provide:
- Identity verification  
- Tamper‑proof records  
- Legally binding proof of consent  

---

## 6. Summary

Digital signatures are essential for secure communication and trust in digital systems.  
They provide:
- **Authenticity** (verifies sender identity)  
- **Integrity** (detects tampering)  
- **Non‑repudiation** (sender cannot deny signing)  

They work by combining:
- Cryptographic hashing  
- Asymmetric encryption  

Real‑world systems like software distribution, email security, and legal digital workflows rely heavily on digital signatures.



