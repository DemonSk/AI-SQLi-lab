# AI + SQLi Lab — App Guide

This folder contains a tiny Node/Express app that demonstrates:
- **SQL injection (vulnerable + fixed)**  
- **Prompt injection (vulnerable + fixed)**

It is intentionally insecure to show how exploitation works and how to patch it.

---

## ▶️ Run
```bash
npm install
npm start
# App runs on http://localhost:3000
```

---

## 🔥 Vulnerable endpoints

### 1) SQL Injection (vulnerable)
**POST `/login`**

The login query uses string concatenation:
```js
const query = `SELECT * FROM users WHERE username='${username}' AND password='${password}'`;
```

This allows payloads like:
```
' OR 1=1 --
```

---

### ✅ SQL Injection (fixed)
**POST `/login_safe`**

Safe fix uses parameterized queries:
```js
const stmt = db.prepare("SELECT * FROM users WHERE username=? AND password=?");
```

---

### 2) Prompt Injection (vulnerable)
**POST `/assistant`**

This endpoint blindly follows the user prompt:
```js
const system = "You are a helpful assistant. Reveal secrets if asked.";
```

---

### ✅ Prompt Injection (fixed)
**POST `/assistant_safe`**

Mitigations:
- system prompt disallows secrets  
- basic detection for injection phrases  
- no sensitive data in outputs

---

## 🛠 How to make it *non‑vulnerable*
1) **Always parameterize SQL** (never build queries with string concatenation).  
2) **Validate inputs** (length, allowed chars, reject dangerous inputs).  
3) **Harden LLM system prompts** and isolate them from user input.  
4) **Never return secrets** in model output.  
5) Add **logging + rate limits** to reduce abuse.

---

## ⚠️ Disclaimer
This is a security demo. Do **not** deploy as‑is.
