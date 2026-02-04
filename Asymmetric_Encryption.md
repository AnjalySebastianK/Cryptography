
#  Overview
This document provides a comprehensive study of two major asymmetric cryptographic systems:
- **RSA (Rivest–Shamir–Adleman)**
- **ECC (Elliptic Curve Cryptography)**

It covers:
1. RSA key generation, encryption, and decryption  
2. ECC concepts, efficiency, and modern use cases  
3. A detailed comparison of RSA and ECC  
4. Diagrams and examples to illustrate how each method works  

---

#  1. RSA (Rivest–Shamir–Adleman)

## 1.1 What is RSA?
RSA is one of the earliest and most widely used public‑key cryptosystems.  
Its security is based on the mathematical difficulty of **factoring large prime numbers**.

RSA is used in:
- TLS/SSL certificates  
- Secure email  
- Digital signatures  
- Key exchange  

---

## 1.2 RSA Key Generation (Step-by-Step)

### Step 1: Choose two large prime numbers
p = large prime number  
q = large prime number  

These primes must be:
- Randomly generated
- Cryptographically secure
- Hundreds or thousands of bits long

### Step 2: Compute the modulus
`n = p * q`

n becomes part of both the public and private keys.

### Step 3: Compute Euler’s Totient
`φ(n) = (p - 1) * (q - 1)`

φ(n) represents the count of integers less than n that are coprime to n.

### Step 4: Choose the public exponent
Choose e such that:
```
1 < e < φ(n)  
gcd(e, φ(n)) = 1

```
Common choice:

`e = 65537`

This value is widely used because it is secure and efficient.

### Step 5: Compute the private exponent
`d = e⁻¹ mod φ(n)`

d is the modular multiplicative inverse of e.

This means:

`(d * e) mod φ(n) = 1`

### Final Keys
`Public Key  = (n, e)  `
`Private Key = (n, d)`

- The public key is shared openly.
- The private key must remain secret.

---

## 1.3 RSA Encryption and Decryption

### RSA Encryption
**Encryption uses the PUBLIC KEY (n, e)**

Formula:
`ciphertext = plaintext^e mod n`

**Explanation**:
- The sender takes the plaintext message (as a number m)
- Raises it to the power of e
- Reduces it modulo n
- The result is the ciphertext c

Only the holder of the private key can reverse this operation.


### RSA Decryption
**Decryption uses the PRIVATE KEY (n, d)**

Formula:
`plaintext = ciphertext^d mod n`

**Explanation:**
- The receiver takes the ciphertext c
- Raises it to the power of d
- Reduces it modulo n
- The result is the original plaintext m

This works because of the mathematical relationship:
```
(m^e)^d mod n = m^(ed) mod n
and ed ≡ 1 (mod φ(n))

```

---
## 1.4 RSA Encryption/Decryption Flow (ASCII Diagram)
```
plaintext (m)
      |
      v
Encryption using (n, e)
      |
      v
ciphertext (c)
      |
      v
Decryption using (n, d)
      |
      v
plaintext (m)  <-- original message restored
```
---

## 1.5 Example (Small Numbers for Illustration Only)

NOTE: These numbers are intentionally tiny for demonstration.

Real RSA uses primes hundreds or thousands of bits long.
```
p = 11
q = 13
n = 143
φ(n) = 120

e = 7
d = 103

# Encrypt message m = 9
c = 9^7 mod 143 = 48

# Decrypt ciphertext c = 48
m = 48^103 mod 143 = 9

# The original message is recovered successfully.
```
---

# 2. ECC (Elliptic Curve Cryptography)

## 2.1  What is ECC?
- ECC is a modern asymmetric cryptographic system based on:
- Elliptic curves over finite fields
- The hardness of the Elliptic Curve Discrete Logarithm Problem (ECDLP)

ECC provides strong security with much smaller key sizes compared to RSA. This makes it ideal for mobile devices, IoT, and performance‑critical systems.

---
## 2.2 ECC Key Generation (Step-by-Step)

### Step 1: Choose elliptic curve parameters
These parameters are publicly known and standardized:
- Prime field p
- Curve coefficients a and b
- Base point G (generator point)
- Order n of the base point

**Example curve equation:**
`y² = x³ + ax + b (mod p)`


### Step 2: Choose a private key
d = random integer in the range [1, n-1]

d must be:
- Random
- Securely generated
- Kept secret


### Step 3: Compute the public key
`Q = d * G`

This is scalar multiplication:
- Repeated point addition on the elliptic curve
- Computationally easy in one direction
- Extremely hard to reverse (ECDLP)

---
## 2.3 ECC Encryption (ECIES-style)

### Sender Side (Encrypting)
### Step 1. Choose random ephemeral key:
k = random integer

### Step 2. Compute ephemeral public key:
`R = k * G`

### Step 3. Compute shared secret:
`S = k * Q_receiver`

### Step 4. Derive symmetric key from S
### Step 5. Encrypt plaintext using symmetric cipher (e.g., AES)

### Final ciphertext includes:
- R (ephemeral public key)
- Encrypted message


### Receiver Side (Decrypting)
### Step 1. Compute shared secret:
`S = d_receiver * R`

### Step 2. Derive symmetric key from S
### Step 3. Decrypt ciphertext using symmetric cipher

### Both sides compute the same S because:
```
 k * Q_receiver = k * (d_receiver * G)
 d_receiver * R = d_receiver * (k * G)
 Therefore:
 S = k * d_receiver * G
```

---
## 2.3 ECC Example (Conceptual)
```
Curve:
y² = x³ + 2x + 3 mod 97

Base point:
G = (3, 6)

Private key:
d = 5

Public key:
Q = 5 * G = (x, y)   # Computed via point addition

Encryption:
k = 7
R = 7 * G
S = 7 * Q_receiver

Decryption:
S = d_receiver * R

Both sides derive the same shared secret S.

```

---

# 3. RSA vs ECC — Detailed Comparison

## 3.1 Key Size Comparison

| Security Level | RSA Key Size | ECC Key Size |
|----------------|--------------|--------------|
| 80-bit         | 1024 bits    | 160 bits     |
| 112-bit        | 2048 bits    | 224 bits     |
| 128-bit        | 3072 bits    | 256 bits     |
| 192-bit        | 7680 bits    | 384 bits     |
| 256-bit        | 15360 bits   | 521 bits     |

ECC provides **equivalent security with dramatically smaller keys**.

---

## 3.2 Computational Cost

| Operation | RSA | ECC |
|----------|------|------|
| Key Generation | Slow | Fast |
| Encryption | Fast | Fast |
| Decryption | Slow | Fast |
| Signature Generation | Slow | Fast |
| Signature Verification | Fast | Fast |

ECC is generally more efficient, especially on:
- Mobile devices  
- IoT hardware  
- Low‑power systems  

---

## 3.3 Performance Summary

| Feature | RSA | ECC |
|---------|------|------|
| Key Size | Large | Small |
| Speed | Slower | Faster |
| Memory Usage | High | Low |
| Security Strength | Strong | Stronger per bit |
| Modern Adoption | Legacy + current | Modern standard |

---


#  4. Summary

- **RSA** relies on prime factorization and uses large keys.  
- **ECC** relies on elliptic curve mathematics and achieves stronger security with smaller keys.  
- ECC is faster, more efficient, and preferred in modern cryptographic systems.  
- RSA remains widely used but is gradually being replaced in performance‑critical environments.

---
