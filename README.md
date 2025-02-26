# 🔐 bcrypt: Secure Password Hashing

`bcrypt` is a cryptographic hashing function designed for **secure password storage**. It includes **salting**, **key stretching**, and an **adaptive work factor** to make brute-force attacks difficult.

---

## 📌 Why Use bcrypt?

✅ **Salted Hashing** - Prevents rainbow table attacks.  
✅ **Adaptive Work Factor** - Makes cracking attempts slower over time.  
✅ **Resistant to Brute-Force** - Computation-intensive hashing deters attackers.  
✅ **Automatic Salt Generation** - Each password gets a unique salt.

---

## 📜 How bcrypt Works

![bcrypt process](https://upload.wikimedia.org/wikipedia/commons/4/46/Bcrypt_stacked.svg)

1. **Generate a random salt** (16 bytes)
2. **Combine salt + password**
3. **Hash using Blowfish encryption**
4. **Repeat hashing 2^cost_factor times**
5. **Store: `$2a$Cost$Salt$HashedPassword`**

### 🔍 Hash Format Example
```plaintext
$2a$12$Nw0HQpo.Dl4XJ0N3pyktqu98UJOnvPtHpLPYjZ1BSuD84h6N7V8O6
```
**Breakdown:**
| Part | Description |
|------|------------|
| `$2a$` | bcrypt version |
| `12` | Cost factor (work factor) |
| `$Nw0HQpo.Dl4XJ0N3pyktqu` | Salt |
| `98UJOnvPtHpLPYjZ1BSuD84h6N7V8O6` | Hashed password |

---

## 🚀 Implementation Examples

### **Python (`bcrypt` library)**
```python
import bcrypt

password = b"my_secure_password"
salt = bcrypt.gensalt(rounds=12)
hashed_password = bcrypt.hashpw(password, salt)

print("Hashed Password:", hashed_password)

# Verify password
entered_password = b"my_secure_password"
if bcrypt.checkpw(entered_password, hashed_password):
    print("✅ Password is correct!")
else:
    print("❌ Incorrect password!")
```

### **Node.js (`bcryptjs` library)**
```javascript
const bcrypt = require('bcryptjs');
const password = "my_secure_password";
const saltRounds = 12;

bcrypt.hash(password, saltRounds, (err, hash) => {
    console.log("Hashed Password:", hash);

    // Verify password
    bcrypt.compare(password, hash, (err, result) => {
        console.log(result ? "✅ Password is correct!" : "❌ Incorrect password!");
    });
});
```

---

## ⚙️ Choosing the Right Cost Factor

Higher cost factor increases security but slows performance.

| Cost Factor | Approx. Time per Hash |
|------------|----------------------|
| **8**  | ~20ms  |
| **10** | ~100ms |
| **12** | ~300ms (**Recommended**) |
| **14** | ~1s    |
| **16** | ~4s    |

---

## 🛑 Common Mistakes to Avoid

❌ **Using a low cost factor (e.g., 6, 8)** → Easier to brute-force.  
❌ **Rehashing an already hashed password** → Unnecessary.  
❌ **Storing bcrypt hashes in plaintext files** → Use a secure database.  
❌ **Using the same salt for all passwords** → bcrypt generates a unique salt automatically.

---

## ⚖️ bcrypt vs. Other Hashing Methods

| Feature       | bcrypt | PBKDF2 | Argon2 | SHA-256 |
|--------------|--------|--------|--------|---------|
| **Salted**   | ✅     | ✅     | ✅     | ❌ (manual) |
| **Adaptive** | ✅     | ✅     | ✅     | ❌ |
| **Memory-Hard** | ❌ | ❌ | ✅ | ❌ |
| **Fast on GPUs?** | ❌ (Good) | ✅ (Weak) | ❌ (Best) | ✅ (Weak) |

---

## 🔎 When Should You NOT Use bcrypt?

🚫 **If hashing large amounts of data** → Use SHA-256 instead.  
🚫 **If protecting short-lived secrets** → bcrypt may be too slow.  
🚫 **If needing extra GPU resistance** → Use **Argon2id** instead.  

---

## 🏆 Conclusion

✔️ bcrypt is **one of the best** hashing algorithms for securely storing passwords.  
✔️ Offers **salting, adaptive work factor, and key stretching** to prevent attacks.  
✔️ Always use **cost factor ≥ 12** for security against modern attacks.  
✔️ If available, **consider Argon2id** for even better security.

---

## 📚 Resources
- [bcrypt Documentation](https://en.wikipedia.org/wiki/Bcrypt)
- [Node.js bcryptjs](https://www.npmjs.com/package/bcryptjs)
- [Python bcrypt](https://pypi.org/project/bcrypt/)

🔗 **Want to contribute?** Fork this repository and submit a pull request! 🚀
