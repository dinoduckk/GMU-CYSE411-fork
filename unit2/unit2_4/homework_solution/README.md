# CYSE 411 – Instructor Solution (Unit 2.4)
Secure Coding: CSRF, Authentication, and Logic Abuse

---

## 🎯 Purpose of This Version

This is the **secure instructor solution** for the Unit 2.4 homework.

It demonstrates:

- How vulnerabilities manifest in real systems
- How to fix them using **defensive coding principles**
- Why each fix is necessary

All fixes are **implemented and commented in the code**, and explained here.

---

# 🧠 Key Concept

> Security failures occur when systems trust the client, the session, or the workflow without proper validation.

---

# 🔍 Vulnerabilities and Fixes

---

## 1️⃣ CSRF (Cross-Site Request Forgery)

### ❌ Problem

The vulnerable version allowed requests like:

```http
POST /transfer

```

without verifying:

- where the request came from

- whether the user intended the action

Because:

- the browser automatically sends session cookies


### ✅ Fix Implemented

```JavaScript

if (req.body.csrfToken !== req.session.csrfToken)

```

✔ Explanation

- A random token is generated and stored in the session

- The same token must be sent in the request

- Attackers cannot guess this token

📌 Key Insight: CSRF is not about stealing credentials — it is about abusing trusted requests.

🔗 Reference: https://www.npmjs.com/package/csurf

---

## 2️⃣ Weak Password Handling

### ❌ Problem
```SQL
SELECT * FROM users WHERE username=? AND password=?
```

- Passwords stored in plaintext

- Easily compromised if database leaks


### ✅ Fix Implemented
```SQL
const match = await bcrypt.compare(password, user.password);
```

✔ Explanation

- Passwords are hashed using bcrypt

- Even if database leaks → passwords are not directly exposed


📌 Key Insight: Never store passwords — store hashes.


🔗 Reference: https://www.npmjs.com/package/bcrypt

---

## 3️⃣ Session Fixation

### ❌ Problem

```JavaScript
req.session.user = username;
```

- Session ID remains the same after login

- Attacker can predefine session ID

### ✅ Fix Implemented

```JavaScript
req.session.regenerate(() => { ... });

```

✔ Explanation

- Generates a new session after login

- Prevents attacker from reusing a known session ID

📌 Key Insight: Authentication must create a new trusted session.

