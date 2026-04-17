
# 🧾 Simple CTF Journal Documentation

## Task 1 – Simple CTF

```bash
nmap -A 10.112.135.35
```

Starting Nmap 7.99 at 2026-04-16 12:06 +0300

Nmap scan report for 10.112.135.35
Host is up (0.16s latency)

Not shown: 997 filtered tcp ports

### Open Ports:

* 21/tcp ftp vsftpd 3.0.3

  * FTP anonymous login allowed (FTP code 230)
  * Can't get directory listing: TIMEOUT
* 80/tcp http Apache httpd 2.4.18 (Ubuntu)

  * Apache default page: “It works”
  * robots.txt has:

    * `/`
    * `/openemr-5_0_1_3`
* 2222/tcp ssh OpenSSH 7.2p2 Ubuntu

OS guess: Linux kernel

---

In the scan I found FTP is allowing anonymous login.

---

## Task Questions

### 1. How many services are running under port 1000?

I scanned the network using nmap and found 3 ports:

* FTP (21)
* HTTP (80)
* SSH (2222)

SSH is on port 2222, but it is still under 1000? (I was confused here)

So I concluded:

* Answer: **2 services**

---

### 2. What is running on the higher port?

The highest port is 2222
It is running:

* **SSH**

So answer: **SSH**

---

### 3. What’s the CVE you’re using against the application?

At first I searched vsftpd 3.0.3 exploit online but it was not the answer.

I got a hint (Echo THM AI) which suggested it is related to a CMS version.

So instead of copying random exploits, I tried to understand it.

By checking the `/openemr-5_0_1_3` hint and version, I researched more.

After some confusion and AI help, I found:

* **CVE-2019-9053**

What I understood:

* This CVE allows **blind SQL injection**

---

### 4. To what kind of vulnerability is the application vulnerable?

By confirming the CVE and testing ideas:

I realized:

* It is **SQL injection**

So answer:

* **SQLi**

---

While doing this I connected to FTP but it was not useful / was unstable.

It felt disabled sometimes, so I asked AI how to enable/use it.

Inside FTP I saw a message about “mitch” using same password / weak password hints.

So I tried brute force but it failed.

---

I also used searchsploit and found CMS exploitation scripts again pointing to SQL injection.

I tried running exploit code but I struggled because:

* Python setup issues
* I didn’t fully understand how to run it

So I got stuck for a bit.

---

### 5. What’s the password?

After researching GitHub for the CVE, I found an exploit script.

I ran it and got:

```
[+] Salt for password found: 1dac0d92e9fa6bb2
[+] Username found: mitch
[+] Email found: admin@admin.com
[+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96
```

At this point I struggled a lot with cracking the password.

I had no experience with hash cracking using tools like:

* hashcat
* john the ripper

My system also had issues so I couldn’t properly use hashcat.

I tried different methods but nothing worked smoothly.

I stopped and learned basics of:

* hashing
* encoding/decoding
* John the Ripper usage

Eventually with help (AI), I got the password:

* **secret**

---

### 6. Where can you login with the details obtained?

We have:

* username: mitch
* password: secret

SSH is available so:

* Login method: **SSH**

---

### 7. What’s the user flag?

I connected to SSH on port 2222:

Inside the system I found `user.txt`

```
G00d j0b, keep up!
```

---

### 8. Is there any other user in the home directory? What’s its name?

I searched `/home` and found:

* **sunbath**

---

### 9. What can you leverage to spawn a privileged shell?

I checked sudo permissions:

```bash
sudo -l
```

I found:

* vim can be run as sudo without password

I checked GTFOBins but I didn’t fully understand at first.

I was confused and felt like I didn’t know what I was doing.

So I asked ChatGPT and it gave me the command to get root.

So the answer:

* **vim**

---

### 10. What’s the root flag?

I used vim privilege escalation, got root access.

Then:

```
cat /root/root.txt
```

Output:

```
W3ll d0n3. You made it!
```


