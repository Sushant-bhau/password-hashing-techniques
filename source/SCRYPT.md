# 🔐 scrypt: Secure Password Hashing

`scrypt` is a cryptographic key derivation function designed for **secure password storage**. It is resistant to brute-force attacks and optimized to be **memory-hard**, making it difficult for attackers to parallelize computations on specialized hardware (e.g., GPUs, ASICs).

---

## 📌 Why Use scrypt?

✅ **Memory-Hard Algorithm** - Makes brute-force attacks expensive.  
✅ **Resistant to Parallelization** - Hard to crack using specialized hardware.  
✅ **Automatic Salt Generation** - Protects against rainbow table attacks.  
✅ **Fast Key Derivation** - Efficient while maintaining high security.

---

## 📜 How scrypt Works

![scrypt process](https://upload.wikimedia.org/wikipedia/commons/3/3b/Scrypt.svg)

1. **Generate a random salt** (128 bits)
2. **Expand memory usage** via a large vector of pseudo-random values
3. **Mix the password & salt** using multiple iterations
4. **Compress the output** into a derived key
5. **Store: `$scrypt$N$r$p$Salt$HashedPassword`**

### 🔍 Hash Format Example
```plaintext
$scrypt$16384$8$1$Wkh6dXJhVE5RRQ==$7qMwdp5DCEgJmCftXKljwhlWloKqF6nX
```
**Breakdown:**
| Part | Description |
|------|------------|
| `$scrypt$` | Identifier for scrypt |
| `16384` | CPU/memory cost factor (N) |
| `8` | Block size factor (r) |
| `1` | Parallelization factor (p) |
| `Wkh6dXJhVE5RRQ==` | Base64-encoded salt |
| `7qMwdp5DCEgJmCftXKljwhlWloKqF6nX` | Hashed password |

---

## 🚀 Implementation Examples

### **Python (`pyscrypt` library)**
```python
import pyscrypt

password = b"my_secure_password"
salt = b"random_salt"
hashed_password = pyscrypt.hash(password, salt, N=16384, r=8, p=1, dkLen=32)

print("Hashed Password:", hashed_password.hex())
```

### **Node.js (`scrypt` library)**
```javascript
const crypto = require('crypto');
const password = "my_secure_password";
const salt = crypto.randomBytes(16);
const keylen = 32;

crypto.scrypt(password, salt, keylen, { N: 16384, r: 8, p: 1 }, (err, derivedKey) => {
    if (err) throw err;
    console.log("Hashed Password:", derivedKey.toString('hex'));
});
```

---

## ⚙️ Choosing the Right Parameters

Higher values increase security but slow performance.

| Parameter | Recommended Value | Purpose |
|------------|----------------|----------------------|
| **N** | 16384 | CPU/memory cost factor |
| **r** | 8 | Block size |
| **p** | 1 | Parallelization factor |
| **dkLen** | 32 | Derived key length |

---

## 🛑 Common Mistakes to Avoid

❌ **Using low `N` values (e.g., 1024, 4096)** → Weaker against brute-force.  
❌ **Not using a unique salt per password** → Vulnerable to precomputed attacks.  
❌ **Using weak salts (short or predictable)** → Less effective against dictionary attacks.  

---

## ⚖️ scrypt vs. Other Hashing Methods

| Feature       | scrypt | bcrypt | Argon2 | SHA-256 |
|--------------|--------|--------|--------|---------|
| **Memory-Hard** | ✅ | ❌ | ✅ | ❌ |
| **Salted**   | ✅ | ✅ | ✅ | ❌ (manual) |
| **Resistant to GPU Attacks** | ✅ | ❌ | ✅ | ❌ |
| **Adjustable Parameters** | ✅ | ✅ | ✅ | ❌ |

---

## 🔎 When Should You NOT Use scrypt?

🚫 **If hashing large amounts of data** → Use SHA-256 instead.  
🚫 **If performance is a major concern** → bcrypt may be faster.  
🚫 **If needing maximum GPU resistance** → Use **Argon2id** instead.  

---

## 🏆 Conclusion

✔️ scrypt is **highly secure** for password storage due to its **memory-hard** properties.  
✔️ Protects against **brute-force and GPU-based attacks**.  
✔️ Use **N=16384, r=8, p=1** for strong security settings.  
✔️ If available, **consider Argon2id** for even better security.

---

## 📚 Resources
- [scrypt Documentation](https://en.wikipedia.org/wiki/Scrypt)
- [Node.js crypto.scrypt](https://nodejs.org/api/crypto.html#cryptoscryptpassword-salt-keylen-options-callback)
- [Python pyscrypt](https://pypi.org/project/pyscrypt/)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀
