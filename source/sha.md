# 🔐 SHA (Secure Hash Algorithm)

`SHA` (Secure Hash Algorithm) is a family of cryptographic hashing functions designed to ensure data integrity and security. It is widely used for password hashing, digital signatures, and data verification.

---

## 📌 Why Use SHA?

✅ **One-Way Hashing** - Irreversible transformation of data.  
✅ **Collision Resistance** - Hard to find two inputs that produce the same hash.  
✅ **Data Integrity** - Ensures message authenticity.  
✅ **Efficient Computation** - Optimized for performance.

---

## 📜 How SHA Works

![SHA Process](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/SHA-2.svg/512px-SHA-2.svg.png)

1. **Pre-processing:** Padding the message to a specific length.
2. **Divide Message:** Split into blocks of 512 or 1024 bits.
3. **Hash Computation:** Apply multiple rounds of bitwise operations.
4. **Final Digest:** Produces a fixed-length output (e.g., 256-bit hash).

### 🔍 Example SHA-256 Hash Output
```plaintext
"Hello, World!" → 7f83b1657ff1fc53b92dc18148a1d65dfa1c59a5f7a5b8c20e3a1b8a1dfd6e4d
```

---

## 🚀 Implementation Examples

### **Python (`hashlib` library)**
```python
import hashlib

password = "my_secure_password".encode()
hashed_password = hashlib.sha256(password).hexdigest()

print("SHA-256 Hashed Password:", hashed_password)
```

### **Node.js (`crypto` module)**
```javascript
const crypto = require('crypto');

const password = "my_secure_password";
const hashedPassword = crypto.createHash('sha256').update(password).digest('hex');

console.log("SHA-256 Hashed Password:", hashedPassword);
```

---

## ⚙️ SHA Variants and Hash Sizes

| Algorithm | Hash Size | Usage |
|-----------|----------|--------|
| **SHA-1** | 160-bit  | Deprecated, weak security |
| **SHA-224** | 224-bit  | Compact hashing |
| **SHA-256** | 256-bit  | General security (Recommended) |
| **SHA-384** | 384-bit  | Higher security needs |
| **SHA-512** | 512-bit  | Strongest, but slowest |

---

## 🛑 Common Mistakes to Avoid

❌ **Using SHA-1** → Weak against collision attacks.  
❌ **Not Salting Passwords** → Vulnerable to rainbow table attacks.  
❌ **Reusing Hashes** → Always hash new data securely.  
❌ **Using SHA for Passwords** → Use `bcrypt` or `Argon2` instead.

---

## ⚖️ SHA vs. Other Hashing Methods

| Feature       | SHA-256 | bcrypt | Argon2 |
|--------------|--------|--------|--------|
| **Salted**   | ❌ (Manual) | ✅ | ✅ |
| **Adaptive** | ❌ | ✅ | ✅ |
| **Memory-Hard** | ❌ | ❌ | ✅ |
| **Fast on GPUs?** | ✅ (Weak) | ❌ (Good) | ❌ (Best) |

---

## 🔎 When Should You NOT Use SHA?

🚫 **If storing passwords** → Use `bcrypt` or `Argon2`.  
🚫 **If protecting against brute-force attacks** → SHA is too fast.  
🚫 **If high security is needed** → Use `SHA-512` or `SHA-3`.  

---

## 🏆 Conclusion

✔️ SHA is **fast and secure** for integrity checks and digital signatures.  
✔️ SHA-256 and SHA-512 are **widely used for secure data hashing**.  
✔️ Do **NOT use SHA alone for password hashing** → use `bcrypt` or `Argon2`.  

---

## 📚 Resources
- [SHA-2 Wikipedia](https://en.wikipedia.org/wiki/SHA-2)
- [Python hashlib Documentation](https://docs.python.org/3/library/hashlib.html)
- [Node.js Crypto Module](https://nodejs.org/api/crypto.html)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀

