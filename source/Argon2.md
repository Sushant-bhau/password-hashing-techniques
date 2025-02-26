# 🔐 Argon2: Next-Generation Password Hashing

`Argon2` is a **memory-hard password hashing algorithm** designed to be highly resistant to **brute-force attacks**, **GPU cracking**, and **side-channel attacks**. It won the [2015 Password Hashing Competition (PHC)](https://password-hashing.net/).

---

## 📌 Why Use Argon2?

✅ **Memory-Hard** - Uses significant RAM to slow down brute-force attempts.  
✅ **Highly Configurable** - Adjustable memory, time, and parallelism settings.  
✅ **Resistant to GPU Attacks** - Unlike bcrypt and PBKDF2, Argon2 is difficult to parallelize.  
✅ **Three Variants**:
   - **Argon2d**: Best for cryptographic applications.
   - **Argon2i**: Best for password hashing, resistant to side-channel attacks.
   - **Argon2id** (**Recommended**): Hybrid approach, combining both Argon2i and Argon2d.

---

## 📜 How Argon2 Works

![Argon2 process](https://upload.wikimedia.org/wikipedia/commons/5/56/Argon2.png)

1. **Generates a random salt** (16+ bytes)
2. **Divides memory into blocks**
3. **Computes pseudo-random values** iteratively
4. **Performs XOR and mixing operations**
5. **Returns final hash**

### 🔍 Hash Format Example
```plaintext
$argon2id$v=19$m=65536,t=3,p=4$base64_salt$base64_hash
```
**Breakdown:**
| Part | Description |
|------|------------|
| `$argon2id$` | Argon2 version |
| `v=19` | Version number |
| `m=65536` | Memory usage (64MB) |
| `t=3` | Iterations (time cost) |
| `p=4` | Parallelism factor |
| `base64_salt` | Salt |
| `base64_hash` | Hashed password |

---

## 🚀 Implementation Examples

### **Python (`argon2-cffi` library)**
```python
from argon2 import PasswordHasher
ph = PasswordHasher()

# Hash a password
hash = ph.hash("my_secure_password")
print("Hashed Password:", hash)

# Verify a password
try:
    ph.verify(hash, "my_secure_password")
    print("✅ Password is correct!")
except:
    print("❌ Incorrect password!")
```

### **Node.js (`argon2` library)**
```javascript
const argon2 = require('argon2');

(async () => {
    try {
        const hash = await argon2.hash("my_secure_password", { type: argon2.argon2id });
        console.log("Hashed Password:", hash);

        const isMatch = await argon2.verify(hash, "my_secure_password");
        console.log(isMatch ? "✅ Password is correct!" : "❌ Incorrect password!");
    } catch (err) {
        console.error(err);
    }
})();
```

---

## ⚙️ Choosing the Right Parameters

**Recommended Settings:**
| Parameter | Low Security | Medium Security | High Security |
|-----------|-------------|----------------|---------------|
| Memory (m) | 64MB  | 128MB | 256MB+ |
| Iterations (t) | 3  | 4-6 | 6-10 |
| Parallelism (p) | 1-2  | 2-4 | 4-8 |

---

## 🛑 Common Mistakes to Avoid

❌ **Using default parameters without tuning** → Always adjust based on security needs.  
❌ **Ignoring parallelism (p) setting** → Optimizing parallelism helps performance.  
❌ **Using a low memory cost (m)** → Increases vulnerability to attacks.  
❌ **Forgetting to store salt with the hash** → Salt is necessary for verification.

---

## ⚖️ Argon2 vs. Other Hashing Methods

| Feature       | Argon2id (**Recommended**) | bcrypt | PBKDF2 |
|--------------|--------|--------|--------|
| **Memory-Hard** | ✅ | ❌ | ❌ |
| **Resistant to GPUs?** | ✅ (Best) | ❌ (Weak) | ❌ (Weak) |
| **Salting**   | ✅ | ✅ | ✅ |
| **Customizable** | ✅ | ✅ | ✅ |
| **Fast on CPUs?** | ✅ | ✅ | ✅ |
| **Best for Passwords?** | ✅ | ✅ | ✅ |

---

## 🔎 When Should You NOT Use Argon2?

🚫 **If hashing large amounts of data** → Use SHA-256 for general-purpose hashing.  
🚫 **If working on old hardware** → Argon2 may be too resource-intensive.  
🚫 **If you need fast, single-use hashing** → Consider bcrypt for simplicity.  

---

## 🏆 Conclusion

✔️ Argon2 is **the most secure** password hashing algorithm available today.  
✔️ Offers **salting, memory-hard computation, and parallelism** to prevent attacks.  
✔️ Use **Argon2id** for **best security** against brute-force and side-channel attacks.  
✔️ Always **tune memory, iterations, and parallelism** for optimal security.  

---

## 📚 Resources
- [Argon2 Official Paper](https://github.com/P-H-C/phc-winner-argon2)
- [Python argon2-cffi](https://pypi.org/project/argon2-cffi/)
- [Node.js argon2](https://www.npmjs.com/package/argon2)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀
