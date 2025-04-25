# Red Team Tactics and Exploitation Lab

This repository documents a hands-on offensive security project targeting **Metasploitable 2**, a vulnerable Linux-based virtual machine. Using **Kali Linux**, this lab simulates real-world attacker tactics to identify exploitable weaknesses, gain unauthorized access, and demonstrate the importance of hardening and secure configuration practices.

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Objectives](#objectives)
- [Key Achievements](#key-achievements)
- [Skills Demonstrated](#skills-demonstrated)
- [Recommendations for Future Enhancements](#recommendations-for-future-enhancements)
- [License](#license)

---

## Project Overview

The lab targets **Metasploitable 2**, a vulnerable virtual machine commonly used for penetration testing education. The offensive engagement focuses on discovering vulnerabilities, exploiting them using open-source tools, escalating privileges, and documenting findings for remediation.

---

## Technologies Used

- Kali Linux – Attacker operating system
- Metasploitable 2 – Vulnerable Linux target
- Nmap – Network and service discovery
- Metasploit – Automated exploitation framework
- Hydra & Medusa – Brute-force password cracking tools
- Netcat, SSH, Python – Post-exploitation utilities

---

## Objectives

- Identify common vulnerabilities including outdated services, weak credentials, and insecure configurations  
- Exploit services to achieve unauthorized access and escalate privileges  
- Demonstrate data exfiltration and post-exploitation techniques  
- Provide remediation guidance based on offensive findings  

---

## Key Achievements

- **Exploited command injection vulnerability in the web application**  
  *Used the web application's input fields to inject OS commands and gain access to the underlying Linux system, achieving remote code execution on the target.*

- **Exploited an insecure SMB service to enumerate users and share information**  
  *Leveraged weak configurations in the SMB service to access shared folders and enumerate users, revealing sensitive files and user credentials.*

- **Exploited weak SSH credentials through brute-forcing**  
  *Used Hydra to brute-force SSH login credentials, gaining unauthorized access to the system with default and weak passwords.*

- **Accessed an unsecured MySQL database**  
  *Exploited default configurations and weak passwords to gain access to an open MySQL service, retrieving sensitive data such as user credentials and database entries.*

- **Identified and documented 6 additional vulnerabilities in the system**  
  *Discovered the presence of unpatched services such as outdated Apache, VSFTPD, and OpenSSH versions that could be targeted for further exploitation, along with potential configuration weaknesses like world-readable files and unnecessary services running.*

---

## Skills Demonstrated

- **Penetration Testing Methodology**  
  *Followed a structured attack lifecycle including reconnaissance, exploitation, privilege escalation, and reporting.*

- **Vulnerability Discovery and Exploitation**  
  *Identified vulnerable services, exploited misconfigurations, and injected commands to compromise Metasploitable 2. Conducted brute-force attacks to crack weak credentials.*

- **Command Injection Attacks**  
  *Exploited vulnerable web application input fields to execute arbitrary commands on the underlying host, simulating real-world attack techniques.*

- **SMB Exploitation**  
  *Enumerated shared resources and user accounts by leveraging insecure SMB configurations, facilitating further access to sensitive files.*

- **Brute-Force Attack Techniques**  
  *Used Hydra to perform dictionary-based brute-force attacks on SSH and FTP services, bypassing weak password protections.*

- **Post-Exploitation Enumeration**  
  *Escalated access by exploiting unsecured services, enumerating users, extracting hashed passwords, and mapping the internal system.*

- **Red Team Reporting and Defense Recommendations**  
  *Generated findings and mitigation strategies to strengthen defensive posture based on offensive results.*

---

## Recommendations for Future Enhancements

- **Apply Patches and Update Vulnerable Services**  
  Ensure that all software, including **Apache**, **OpenSSH**, **VSFTPD**, and **Samba**, is updated to mitigate known vulnerabilities such as **CVE-2017-11103** (Apache), **CVE-2016-0748** (OpenSSH), and **CVE-2011-1087** (Samba).

- **Implement Strong Authentication**  
  Enforce strong password policies and implement two-factor authentication for critical services, particularly SSH and MySQL.

- **Restrict SMB Shares**  
  Secure SMB shares by limiting access to specific users or IP addresses and disabling the anonymous access that Metasploitable 2 permits by default.

- **Secure MySQL Database Access**  
  Configure MySQL to require strong, unique passwords, limit access to trusted IP addresses, and use encryption for sensitive data at rest.

- **Regular Audits of Sudo Permissions and Services**  
  Review and remove unnecessary sudo permissions and services that are not required by the system to minimize attack surfaces.

- **Service Hardening and Firewalls**  
  Disable unnecessary services and implement **iptables** or **ufw** to restrict inbound and outbound traffic to only trusted hosts and ports.

- **Introduce Advanced Evasion and Pivoting Techniques**  
  In future labs, simulate internal network pivoting after initial compromise to further assess how far an attacker could penetrate.

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.
