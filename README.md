# Red Team Tactics and Exploitation Lab

This repository provides a detailed overview of a hands-on offensive security project designed to simulate real-world attack scenarios. The target is *Metasploitable 2*, a vulnerable Linux-based virtual machine. The project leverages *Kali Linux* and a suite of open-source tools to identify and exploit weaknesses, all while emphasizing the importance of system hardening and secure configurations. Through this exercise, we highlight the crucial role offensive security plays in understanding vulnerabilities and improving defenses.

> [!IMPORTANT]
> **Understanding how attacks unfold is essential for effective defense**. By simulating attacker tactics, we gain insights into how vulnerabilities are exploited, helping defenders to better secure systems before real attackers can exploit them.

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Objectives](#objectives)
- [Attacks and Exploits](#attacks-and-exploits)
- [Skills Demonstrated](#skills-demonstrated)
- [Recommendations for Future Enhancements](#recommendations-for-future-enhancements)

## Project Overview

The **Red Team Tactics and Exploitation Lab** targets *Metasploitable 2*, a machine purposely configured with a range of common security flaws to simulate the type of vulnerabilities often found in real-world systems. The main goal of this project was to replicate the kind of attacks that an adversary might use to compromise a system. By identifying weaknesses, exploiting them, and then escalating privileges, the exercise demonstrates how attackers can move from initial access to full control of a system. Ultimately, the aim is to better understand how to defend against these tactics by simulating them in a controlled environment.

> [!NOTE]
> **This lab serves two main purposes**: first, to simulate real-world attacks on a vulnerable system, and second, to gain actionable insights into securing systems by understanding the methods used by attackers. Knowing how an attacker thinks and operates is a critical part of building stronger defenses.

## Technologies Used

To replicate a realistic attack scenario, a variety of tools and technologies were employed. These tools are commonly used in penetration testing and offensive security, each playing a role in the attack lifecycle.

- **`Kali Linux`**: The operating system used for offensive operations, pre-loaded with essential penetration testing tools.
- **`Metasploitable 2`**: The vulnerable target machine, intentionally configured with flaws to simulate common security issues.
- **`Nmap`**: A network scanning tool used to identify open ports and active services on the target machine.
- **`Metasploit`**: An exploitation framework that automates the attack process against vulnerable services.
- **`Hydra & Medusa`**: Password cracking tools used for brute-forcing weak or default credentials.
- **`Netcat`, `SSH`, `Python`**: Utilities for post-exploitation, allowing for interaction with the compromised system.

## Objectives

The key goals for this project were:

1. **Identify and exploit vulnerabilities**: These included outdated services, weak credentials, and misconfigurations that leave systems open to attack.
2. **Achieve unauthorized access**: By exploiting weaknesses, the goal was to escalate privileges and gain full control of the system.
3. **Simulate post-exploitation activities**: This involved actions such as data exfiltration, credential theft, and system enumeration.
4. **Provide actionable remediation recommendations**: Based on the vulnerabilities discovered, the project aimed to provide steps to improve system security.

## Attacks and Exploits

Several attack vectors were tested in this project. Below are detailed descriptions of the key methods used to exploit vulnerabilities and escalate privileges.

### Service Vulnerabilities and Exploitation

The first stage of the attack was identifying vulnerable services running on *Metasploitable 2*. Using `Nmap` and banner grabbing, services like OpenSSH, VSFTPD, Samba, and Apache were found to be running outdated versions with known vulnerabilities.

- **OpenSSH (CVE-2017-11103)**  
  The OpenSSH version was outdated and vulnerable to a remote code execution bug. This flaw allowed us to gain SSH access to the machine, using the service itself as an entry point.

- **VSFTPD Backdoor**  
  The VSFTPD service was running a vulnerable version that included a backdoor. This backdoor allowed for unauthenticated remote access, which provided an easy method to gain control of the system.

- **Samba Vulnerabilities**  
  The Samba service had weak configurations that allowed for the enumeration of shared files and services. By exploiting these weaknesses, we were able to access sensitive files and gain insight into the internal system structure.

> [!CAUTION]
> **Old software and weak configurations are major security risks**. Services like OpenSSH and Samba, when not properly updated, open the door for attackers to bypass security measures. Regular patching and configuration reviews are essential for reducing the attack surface.

### Privilege Escalation

After gaining access to the system, privilege escalation techniques were used to move from a low-privileged user account to root access. This was done to demonstrate how attackers can escalate their privileges and take full control of a compromised system.

- **Sudo Misconfigurations**  
  By exploiting poorly configured `sudo` permissions, we were able to execute commands with root privileges without needing a password, allowing us to control the system entirely.

- **SUID Binaries**  
  Exploiting insecure SUID binaries, we were able to execute commands as the root user, bypassing standard access controls.

- **Kernel Exploits**  
  Using known kernel vulnerabilities, we escalated from a limited user to root, demonstrating how attackers can gain full control of a system by exploiting flaws in the underlying operating system.

### Brute-Force Attacks

Another attack vector was the use of brute-force techniques to crack weak or default credentials. By employing `Hydra` and `Medusa`, we were able to perform dictionary-based attacks on SSH and FTP services.

- **SSH and FTP Brute-Force**  
  We attempted to crack login credentials for these services using common dictionary lists and weak passwords. This allowed unauthorized access to the system, revealing the importance of using strong, unique passwords.

### Post-Exploitation and Data Extraction

After escalating privileges, the next step was to perform various post-exploitation tasks to extract sensitive data and maintain access.

- **Extracting Password Hashes**  
  By accessing `/etc/shadow`, we extracted password hashes, which could then be cracked offline to gain additional access.

- **Sensitive File Exfiltration**  
  We accessed web server directories and other sensitive file locations to extract valuable information, such as system configurations and passwords.

- **User Enumeration**  
  Using tools like `Netcat` and custom Python scripts, we enumerated user accounts, which gave us additional targets for credential harvesting.

> [!NOTE]
> **Post-exploitation activities are critical to understanding the full impact of a system compromise**. In a real-world attack, attackers would use these techniques to extract data, maintain access, and prepare for further exploitation.

## Skills Demonstrated

This lab showcased a range of offensive security skills, from reconnaissance to post-exploitation.

- **Penetration Testing Methodology**: We followed a structured methodology that included reconnaissance, exploitation, privilege escalation, and post-exploitation.
- **Credential Attacks**: Brute-force attacks on weak or default credentials, demonstrating the effectiveness of tools like `Hydra` and `Medusa`.
- **Privilege Escalation**: Using misconfigured services and kernel vulnerabilities to escalate from a limited user account to root.
- **Post-Exploitation Enumeration**: Extracting sensitive data, including password hashes and user information, and maintaining access for further exploitation.

> [!NOTE]
> **This lab was not just about executing attacks, but understanding how they unfold**. Each stage demonstrated how attackers think and operate, which is essential for building strong defenses against such attacks.

## Recommendations for Future Enhancements

While this lab provided valuable insights into exploiting vulnerabilities, there are opportunities to expand and improve:

1. **Simulate Pivoting and Lateral Movement**  
   Add more vulnerable machines to the lab and simulate internal pivoting from compromised hosts to other parts of the network.

2. **Incorporate Evasion Techniques**  
   Explore how attackers evade detection by AV or IDS using tools like `Veil` and `msfvenom`.

3. **Introduce Logging and Detection Simulation**  
   Integrate monitoring tools such as `syslog` or `auditd` to simulate detection of attack behaviors and correlate with the attacker's activities.

4. **Expand Web Application Exploits**  
   Leverage tools like `Burp Suite` to exploit common web application vulnerabilities such as XSS, SQLi, and RFI.

5. **Patching and Updating Vulnerable Services**  
   Ensure all services are up to date to mitigate known vulnerabilities and prevent exploitation in future attacks.

> [!IMPORTANT]
> **Continuous assessment and improvement are key to staying ahead of attackers**. As attack techniques evolve, so too must defensive strategies. Regularly updating and expanding the scope of penetration testing ensures a more resilient system.

