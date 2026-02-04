# Block Ciphers vs Stream Ciphers

Block ciphers and stream ciphers are the **two main types of symmetric encryption algorithms**. Block ciphers process data in fixed chunks; stream ciphers encrypt continuously bit-by-bit.

## Comparison

| **Type** | **Processing** | **Speed** | **Best For** |
|----------|----------------|-----------|--------------|
| **Block** | Fixed blocks (128 bits) | Parallelizable | Files, storage, TLS |
| **Stream** | Bit/byte stream | Real-time/low latency | Video, VoIP, IoT |

---

## a. Block Ciphers

**Definition**: Encrypt data in **fixed-size blocks** (typically 64, 128, or 256 bits). Each block processed independently or chained via modes.

**Examples**:

- AES: 128-bit blocks, 128/192/256-bit keys (modern standard)
- DES: 64-bit blocks, 56-bit keys (broken, legacy only)
- Blowfish, Twofish: 64-bit blocks

---

## b. Stream Ciphers

**Definition**: Encrypt data **one bit or byte at a time** using a keystream generated from key + nonce/IV. Plaintext XOR keystream = ciphertext.

**Examples**:
- ChaCha20: Modern, fast, secure (WireGuard, TLS 1.3)
- RC4: Deprecated (broken)
- Salsa20: ChaCha20 predecessor


---

## c. Detailed Comparison

| **Aspect** | **Block Ciphers** | **Stream Ciphers** |
|------------|-------------------|--------------------|
| **Data Processing** | Fixed blocks (AES: 128 bits) | Continuous stream |
| **Performance** | Slower startup, parallelizable (CTR mode) | **Faster continuous**, low latency |
| **Memory Use** | Higher (block buffering) | **Lower** (ideal IoT/embedded) |
| **Error Propagation** | High in CBC (1 bit corrupts block) | **Low** (errors localize) |
| **Nonce/IV Reuse** | Safe in most modes | **CRITICAL**: Reuse = plaintext recovery |
| **Hardware Support** | AES-NI everywhere | ChaCha20 growing |
| **Security** | Mature (AES unbroken) | Good if nonce unique |


---

## Real-World Use Cases

### Block Ciphers Dominate Storage

- Disk encryption: BitLocker, LUKS, FileVault (AES)
- Database TDE: Oracle, SQL Server (AES)
- File encryption: VeraCrypt, 7-Zip (AES/Twofish)
- TLS bulk data: AES-GCM (99% of HTTPS)


### Stream Ciphers for Real-Time
 
 - Video streaming: ChaCha20 (TLS 1.3)
 - WireGuard VPN: ChaCha20-Poly1305
 - VoIP: Low-latency stream encryption
 - IoT devices: Minimal memory/CPU


---

## Critical Security Rules

### Block Cipher

- ✅ Use AES-GCM or AES-CTR (authenticated/parallel)
- ✅ Never use ECB alone (pattern leakage)
- ✅ Always use random IV/nonce per message
- ❌ Avoid DES, 3DES (broken


### Stream Cipher 

- ✅ Nonce/IV MUST be unique per key
- ✅ ChaCha20-Poly1305 (authenticated)
- ❌ Never reuse nonce (full plaintext recovery)
- ❌ RC4 is broken (don't use)

--- 

**Block ciphers** = storage/general purpose (AES‑GCM)  
**Stream ciphers** = real-time/low-resource (ChaCha20)

---





