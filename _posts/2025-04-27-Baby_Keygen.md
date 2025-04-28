---
title: "🔑 Baby Keygen"
date: 2025-04-27 14:31:00 +02:00
categories: [Writeup, "CIT@CTF"]
tags: [CIT@CTF, security, rev]
---
# Writeup - CIT CTF Challenge: Baby Keygen

## 📋 Challenge Information
- **Name**: Baby Keygen
- **Category**: Reverse Engineering
- **Description**: I didn't strip this one you're welcome

---

## 🛠️ Solution

In this chelleng we had a downloadable file that, when launched, displayed `Enter Key:`
After typing random characters nothing is displayed so we have to do Reverse Engineering.

In the IDA program, I performed an analysis of the main function.

![IDA screen](/assets/img/CIT_CTF/main.png "Main function")

I then performed an analysis of the `check_key` function.

![IDA screen](/assets/img/CIT_CTF/check.png "Check_key function")

I noticed that the key must start with "KEY_" and in total must have 16 characters and consist of alpha numeric characters

I tried to use a random key that meets these conditions, for example `KEY_ILOVECTF2025`, after which the program displayed a flag.

---

## 🎴 Flag

```plaintext
CIT{41jN8BKzz388}
```
---

