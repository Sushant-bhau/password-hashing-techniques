# 🔐 PBKDF2: Password-Based Key Derivation Function 2

`PBKDF2` (Password-Based Key Derivation Function 2) is a cryptographic algorithm used for **secure password hashing** and **key derivation**. It incorporates **salting**, **key stretching**, and **HMAC (Hash-based Message Authentication Code)** for enhanced security.

---

## 📌 Why Use PBKDF2?

✅ **Salted Hashing** - Protects against rainbow table attacks.  
✅ **HMAC for Integrity** - Ensures protection against tampering.  
✅ **Key Stretching** - Makes brute-force attacks computationally expensive.  
✅ **Widely Supported** - Available in OpenSSL, Python, Node.js, Java, etc.

---

## 📜 How PBKDF2 Works

![PBKDF2 process](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/PBKDF2.svg/500px-PBKDF2.svg.png)

1. **Generate a random salt** (16 bytes recommended).
2. **Combine salt + password**.
3. **Apply HMAC (e.g., HMAC-SHA256) multiple iterations**.
4. **Repeat hashing for `N` iterations (work factor)**.
5. **Output a derived key of desired length**.

### 🔍 PBKDF2 Output Format
```plaintext
SaltedHash = PBKDF2(HMAC, Password, Salt, Iterations, KeyLength)
```

| Parameter  | Description |
|-----------|------------|
| `HMAC` | Hash function used (SHA-256, SHA-512, etc.) |
| `Password` | User's password input |
| `Salt` | Randomly generated salt value |
| `Iterations` | Number of hashing rounds (e.g., 100,000) |
| `KeyLength` | Output key size (e.g., 256 bits) |

---

## 🚀 Implementation Examples

### **Python (`hashlib.pbkdf2_hmac` Library)**
```python
import hashlib
import os

password = b"my_secure_password"
salt = os.urandom(16)  # Generate a random 16-byte salt
iterations = 100000
key_length = 32  # 256-bit output

hashed_password = hashlib.pbkdf2_hmac('sha256', password, salt, iterations, dklen=key_length)
print("Hashed Password:", hashed_password.hex())
```

### **Node.js (`crypto.pbkdf2` Library)**
```javascript
const crypto = require('crypto');
const password = "my_secure_password";
const salt = crypto.randomBytes(16);
const iterations = 100000;
const keyLength = 32;

crypto.pbkdf2(password, salt, iterations, keyLength, 'sha256', (err, derivedKey) => {
    if (err) throw err;
    console.log("Hashed Password:", derivedKey.toString('hex'));
});
```

---

## ⚙️ Choosing the Right Iteration Count

More iterations increase security but slow performance.

| Iterations | Approx. Time per Hash |
|------------|----------------------|
| **10,000**  | ~10ms  |
| **50,000**  | ~50ms  |
| **100,000** | ~100ms (**Recommended Minimum**) |
| **500,000** | ~500ms  |
| **1,000,000** | ~1s  |

---

## 🛑 Common Mistakes to Avoid

❌ **Using too few iterations (e.g., <10,000)** → Easier to brute-force.  
❌ **Using a weak hash function (e.g., MD5, SHA-1)** → Use SHA-256 or SHA-512.  
❌ **Not using a salt** → Makes hashes predictable.  
❌ **Hardcoding salt values** → Each password should have a unique salt.

---

## ⚖️ PBKDF2 vs. Other Hashing Methods

| Feature       | PBKDF2 | bcrypt | Argon2 | SHA-256 |
|--------------|--------|--------|--------|---------|
| **HMAC-Based** | ✅  | ❌ | ❌ | ❌ |
| **Salted**   | ✅  | ✅ | ✅ | ❌ (manual) |
| **Adaptive** | ✅  | ✅ | ✅ | ❌ |
| **Memory-Hard** | ❌ | ❌ | ✅ | ❌ |
| **Fast on GPUs?** | ✅ (Weak) | ❌ (Good) | ❌ (Best) | ✅ (Weak) |

---

## 🔎 When Should You NOT Use PBKDF2?

🚫 **If you need memory-hard security** → Use Argon2 instead.  
🚫 **If hashing large amounts of data** → Use SHA-256 for speed.  
🚫 **If GPU resistance is required** → bcrypt or Argon2 are better choices.

---

## 🏆 Conclusion

✔️ PBKDF2 is **a strong hashing algorithm** for password security.  
✔️ Uses **HMAC for additional integrity** and **adaptive iterations**.  
✔️ **Recommended minimum:** 100,000 iterations for modern applications.  
✔️ If available, **consider Argon2 for even better security**.

---

## 📚 Resources
- [PBKDF2 Wikipedia](https://en.wikipedia.org/wiki/PBKDF2)
- [Python hashlib PBKDF2](https://docs.python.org/3/library/hashlib.html)
- [Node.js PBKDF2](https://nodejs.org/api/crypto.html#cryptopbkdf2password-salt-iterations-keylen-digest-callback)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀
