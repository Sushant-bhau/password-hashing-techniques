
# 🔐 Password Hashing Techniques

Password hashing is a crucial technique for securely storing passwords in databases. Instead of saving plain-text passwords, which can be stolen if the database is compromised, hashing ensures that even if the data is leaked, recovering the original password is extremely difficult. 

## 🔍 Commonly Used Password Hashing Techniques

### 1. MD5 (Message Digest Algorithm 5)
- **Output Length**: 128-bit (32 hexadecimal characters)
- **Security**: ❌ Weak (due to collision vulnerabilities)
- **Usage**: Previously used for password hashing but now considered insecure due to fast brute-force attacks.
- **Example**: `md5("password") → 5f4dcc3b5aa765d61d8327deb882cf99`

### 2. SHA Family (Secure Hash Algorithm)
- **Variants**: SHA-1, SHA-256, SHA-512
- **Security**:
  - **SHA-1**: ❌ Deprecated due to collision attacks.
  - **SHA-256 & SHA-512**: ⚠️ Stronger, but not ideal for password hashing due to speed.
- **Example (SHA-256)**: `sha256("password") → 5e884898da28047151d0e56f8dc62927...`

### 3. bcrypt
- **Key Features**: Slow, adaptive hashing with salt.
- **Security**: ✅ Strong, designed for password hashing.
- **Salting**: Automatically adds salt to prevent rainbow table attacks.
- **Work Factor**: Adjustable (cost factor determines computational complexity).
- **Example**: `$2a$12$Nw0HQpo.Dl4XJ0N3pyktqu98UJOnvPtHpLPYjZ1BSuD84h6N7V8O6`

### 4. PBKDF2 (Password-Based Key Derivation Function 2)
- **Key Features**: Uses salt and multiple iterations to slow down brute-force attacks.
- **Security**: ✅ Strong, but can be optimized with modern hardware.
- **Adjustability**: Number of iterations can be increased over time.
- **Example**: `PBKDF2-HMAC-SHA256(password, salt, iterations)`

### 5. scrypt
- **Key Features**: Memory-hard function, designed to resist GPU/ASIC cracking.
- **Security**: ✅ Stronger than PBKDF2 for password hashing.
- **Example**: `scrypt(password, salt, N, r, p)`

### 6. Argon2 (Winner of the Password Hashing Competition)
- **Variants**:
  - **Argon2d**: Resistant to GPU attacks.
  - **Argon2i**: Resistant to side-channel attacks.
  - **Argon2id**: 🔥 Hybrid of both (**recommended**).
- **Key Features**: Highly secure, memory-hard, and resistant to brute-force attacks.
- **Example**: `argon2id(password, salt, iterations, memory_cost, parallelism)`

## 🔥 Which Hashing Technique Should You Use?

### ✅ **Best Options (Modern & Secure)**
- **Argon2id** (🏆 Recommended)
- **bcrypt**
- **scrypt**

### ❌ **Avoid Using**
- **MD5, SHA-1, SHA-256 alone** (Too fast for password storage, prone to brute-force attacks)

🔗 **For best security practices, always use a slow, memory-hard hashing algorithm like Argon2id, bcrypt, or scrypt!**





# 🔐 Comprehensive Comparison of Password Hashing Algorithms

Choosing the right password hashing algorithm is crucial for security, performance, and scalability. This document provides a detailed comparison of **SHA, Argon2, MD5, bcrypt, scrypt, and PBKDF2** based on efficiency, security, best use cases, and industry recommendations.

---

## 📌 Efficiency & Security Comparison

| Algorithm  | Security Level | Speed (Faster = Less Secure) | Memory-Hard | GPU/ASIC Resistant | Salting Required | Recommended Use |
|------------|---------------|-----------------------------|-------------|------------------|-----------------|----------------|
| **MD5**   | ❌ Weak       | ⚡ Very Fast  | ❌ No  | ❌ No  | ❌ No  | ❌ Not Recommended |
| **SHA-256** | ⚠️ Moderate | ⚡ Very Fast  | ❌ No  | ❌ No  | ❌ No  | ✅ Digital Signatures |
| **bcrypt** | ✅ Strong    | 🐢 Slow      | ❌ No  | ✅ Yes | ✅ Yes | ✅ Web Apps |
| **scrypt** | ✅ Strong    | 🐢 Slow      | ✅ Yes | ✅ Yes | ✅ Yes | ✅ High-Security Apps |
| **PBKDF2** | ✅ Strong    | 🐌 Slower    | ✅ Yes | ❌ No  | ✅ Yes | ✅ Legacy Systems |
| **Argon2** | 🏆 Best      | 🐌 Slowest   | ✅ Yes | ✅ Yes | ✅ Yes | 🚀 Recommended |

🚀 **Best Choice:** **Argon2id** (Resistant to brute-force, memory-hard, and GPU-resistant).

---

## 📜 Which Algorithm Should You Use?

### 🏗️ **System Design & RESTful API Recommendations**

| Use Case | Recommended Algorithm | Reason |
|----------|----------------------|--------|
| **High-Security Systems (e.g., Banking, Government)** | **Argon2id / scrypt** | Highest security with memory-hard features |
| **Web Apps & REST APIs (User Authentication)** | **bcrypt / Argon2id** | Secure and widely supported |
| **Legacy Systems (Backward Compatibility)** | **PBKDF2** | Long-standing industry standard |
| **Cryptographic Signatures / Digital Documents** | **SHA-256 / SHA-3** | Fast, irreversible hashing |
| **Fast Lookups (Low Security, Non-Password Data)** | **MD5 (Only for non-password use cases)** | Fast but insecure |

---

## 🎓 Student Learning Perspective

| Student Goal | Recommended Algorithm | Reason |
|-------------|----------------------|--------|
| **Learning Basics** | **MD5 / SHA-256** | Simple & fast for understanding hashing |
| **Web Development (Low Cost)** | **bcrypt** | Industry standard, easy to use |
| **Deep Security Learning** | **scrypt / Argon2id** | More advanced and secure |
| **Industry-Level Applications** | **Argon2id / bcrypt** | Best balance of security and performance |

💡 **For students**, starting with **bcrypt** is ideal due to its ease of use and industry adoption. As they advance, **Argon2id** is the best for real-world applications.

---

## ⚖️ Detailed Pros & Cons of Each Algorithm

### 🔷 **MD5**
✅ Very fast  
❌ Weak security, prone to collisions and brute-force attacks  
❌ Not suitable for password hashing  

### 🔷 **SHA-256**
✅ Stronger than MD5, widely used in cryptographic applications  
❌ Not designed for password hashing, susceptible to brute-force attacks  

### 🔷 **bcrypt**
✅ Slow hashing makes brute-force attacks difficult  
✅ Salting prevents rainbow table attacks  
❌ Not memory-hard (can be accelerated using specialized hardware)  

### 🔷 **scrypt**
✅ Memory-hard, making GPU attacks more difficult  
✅ Stronger than bcrypt in some cases  
❌ More complex to implement and configure  

### 🔷 **PBKDF2**
✅ Secure and industry-approved  
❌ Can be vulnerable to GPU-based brute-force attacks  

### 🔷 **Argon2** (Recommended)
🏆 **Winner of the Password Hashing Competition (PHC)**  
✅ Most secure, memory-hard, and resistant to side-channel attacks  
✅ Recommended for modern applications  
❌ Requires fine-tuning for optimal security/performance  

---

## 🏆 Industry Best Practices

✔️ **Use Argon2id** for highest security.  
✔️ **Use bcrypt** for general authentication.  
✔️ **Avoid MD5 & SHA-256 for password hashing** (Not secure enough).  
✔️ **Always use salting & adaptive cost factors** to enhance security.  

---

## 📚 Resources
- [Argon2 Documentation](https://github.com/P-H-C/phc-winner-argon2)
- [bcrypt Overview](https://en.wikipedia.org/wiki/Bcrypt)
- [PBKDF2 Explained](https://en.wikipedia.org/wiki/PBKDF2)
- [SHA-256 Explained](https://en.wikipedia.org/wiki/SHA-2)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀
