# Symmetric vs Asymmetric Encryption

Symmetric and asymmetric encryption are the **two fundamental categories** of cryptographic encryption. Symmetric uses one shared secret key; asymmetric uses public-private key pairs to solve the key distribution problem.

## Quick Overview

| **Type** | **Key Model** | **Speed** | **Key Distribution** |
|----------|---------------|-----------|---------------------|
| **Symmetric** | 1 shared secret key | ⚡ **Fast** | 🔒 Hard (must share securely) |
| **Asymmetric** | Public + Private key pair | 🐌 **Slow** | ✅ Easy (public keys free) |

---

## a. The Two Categories

### Symmetric Encryption
Uses the **same secret key** for both encryption and decryption. Both parties must securely share this key beforehand.
Examples: AES, ChaCha20, Blowfish

Key sizes: 128, 192, 256 bits


### Asymmetric Encryption (Public-Key Cryptography)
Uses a **mathematically related key pair**:
- **Public key**: Shared with everyone (used for **encryption**)
- **Private key**: Kept secret (used for **decryption**)

Examples: RSA, ECC (Elliptic Curve Cryptography)

Key sizes: 2048-4096 bits (RSA), 256-521 bits (ECC)


---

## b. Encryption/Decryption Processes

### Symmetric Process (AES Example)


**Steps**:
1. Alice and Bob securely share key `K` (via Diffie-Hellman, pre-shared, etc.)
2. Alice: `Encrypt(plaintext, K) → ciphertext`
3. Bob: `Decrypt(ciphertext, K) → plaintext`

### Asymmetric Process (RSA Example)

**Steps**:
1. Bob generates key pair: Public Key (PK), Private Key (SK)
2. Bob shares PK publicly
3. Alice: `Encrypt(plaintext, Bob's PK) → ciphertext`
4. Bob: `Decrypt(ciphertext, Bob's SK) → plaintext`

---

## c. Advantages, Limitations, Applications

| **Aspect** | **Symmetric** | **Asymmetric** |
|------------|---------------|----------------|
| **Speed** | ⚡ **Very fast** (hardware accelerated) | 🐌 **Computationally expensive** |
| **Key Size** | Small (128-256 bits) | Large (2048+ bits RSA) |
| **Scalability** | N(N-1)/2 keys for N users | N public keys (1 private each) |
| **Strength** | Excellent (AES unbroken) | Excellent (RSA/ECC secure) |
| **Key Exchange** | 🔒 **Problem**: How to share securely? | ✅ **Solved**: Public keys anywhere |
| **Main Use** | Bulk data encryption | Key exchange, signatures |

### Symmetric Advantages

- ✅ Lightning fast for large files
- ✅ Hardware acceleration (AES-NI)
- ✅ Perfect for disk encryption, TLS bulk data
- ❌ Key distribution nightmare

  
### Asymmetric Advantages
- ✅ No shared secret needed
- ✅ Enables digital signatures
- ✅ Perfect forward secrecy (PFS)
- ✅ Public key infrastructure (PKI)
- ❌ Too slow for bulk data

---

### Hybrid Cryptosystem (Real World - TLS/HTTPS)

1. Client ─► RSA(ECC)/DH ─► Session Key Exchange ─► Server

2. Client ─► AES(Session Key) ─► Web Data ─► AES(Session Key) ─► Server

**99% of internet traffic uses this hybrid approach!**

---

## Real-World Applications

### Symmetric Encryption Everywhere
- Disk encryption: BitLocker, LUKS, FileVault (AES-256)
- TLS/HTTPS bulk data: AES-GCM, ChaCha20-Poly1305
- VPN tunnels: IPsec ESP (AES), WireGuard (ChaCha20)
- Database encryption: TDE (AES)


### Asymmetric Encryption Key Moments
- HTTPS handshakes: RSA/ECC certificates
- Digital signatures: Code signing, PDFs
- SSH authentication: Public key login
- PGP email: Encrypt with recipient's public key


---

## The Hybrid Solution (Why Both Exist)

**Problem**: Symmetric = fast but hard key exchange. Asymmetric = secure exchange but slow.

**Solution**: Use asymmetric to exchange symmetric keys, then symmetric for data.

**TLS Handshake Example**:

1. Client encrypts "AES session key" with server's RSA public key

2. Server decrypts session key with private key

3. Both use fast AES for the entire website session

**Conclusion**: Asymmetric for handshakes/signatures, symmetric for everything else.

---





