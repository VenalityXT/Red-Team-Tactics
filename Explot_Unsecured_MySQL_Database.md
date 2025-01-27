# Exploit 2: Unsecured MySQL Database                                                                                 

## Discovery Process                                                                                  
Conducted an Nmap scan of the target to identify open ports and running services:

![NMAP Scan](https://github.com/user-attachments/assets/e5d33e05-78da-48f0-a3e3-a1c308f17f50)

Identified the MySQL service running on port 3306, which is commonly used for database connections.

## Exploitation:                                                                                 
Attempted to access the MySQL database using the mysql client from the Kali Linux VM.

Initial Command:                                                                                 
![MySQL Error_1](https://github.com/user-attachments/assets/52bf360b-d789-4edf-8ba4-d3a9a89dc807)

When running this command, we encountered the error 2026 (HY000): TLS/SSL error: wrong version number.                                           
This was due to an SSL/TLS version mismatch between the MySQL client and the server.

Fix Applied: To resolve this, the connection was modified to disable SSL by using the *--skip-ssl* option:

![MySQL Fix](https://github.com/user-attachments/assets/0ede96c3-1cfe-41f6-85e4-77c3c86b96f3)

This successfully allowed us to bypass the SSL/TLS connection issue and access the MySQL database.

### Explanation of Command:                                                                                 

__-u root:__ Specifies the root user to attempt login.                                                                           
__-p:__ Prompts for a password (used to test the default password or perform a brute-force attack).                                                                          
__--skip-ssl:__ Disables SSL (Secure Sockets Layer), which resolved the error related to SSL/TLS version mismatch.                                                                                 
__-h 192.168.1.184:__ Specifies the Metasploitable VM's IP address.                                                                                 

No Password Set:                                                                                 
![MySQL GainedAccess](https://github.com/user-attachments/assets/4ca770eb-4f75-48d5-aade-e57952a8ecc8)                                                                              

### Proof of Work:
Upon logging in without specifying a password, the MySQL service allowed access without authentication, as no password had been set.                                                                                 
This highlights the unsecured nature of the MySQL service on Metasploitable, allowing unauthenticated access to the database.   

After gaining access, we verified the connection by querying the databases:                                
![MySQL ShowDatabases](https://github.com/user-attachments/assets/39378eaf-e8d1-40b7-a8c8-47aa3e2baa6f)

Searching for sensitive tables which may contain credentials of users:                                
![MySQL Access Database](https://github.com/user-attachments/assets/8a98e1a9-73d1-4153-aee1-693f52aa2f17)

Querying the **user** table to extract usernames and password hashes:                                
![MySQL Access_2](https://github.com/user-attachments/assets/07b73488-69c4-4aaf-aa3f-d1ca680cee0e)

Read Files on the Target:                                                                                                
![MySQL_1](https://github.com/user-attachments/assets/8a37ea5a-fdb8-45ab-acac-7457733c4b13)

Successfully logged in and accessed the MySQL service.                                                                           

Writing a backdoor (Failed)                                                                           
![BackdoorAttemptFailed](https://github.com/user-attachments/assets/b2b2d9d9-6d2d-4ab7-83d2-dd748931ddbc)                                                                           
Writing a backdoor (Success)                                                                           
![BackdoorAttemptSuccess](https://github.com/user-attachments/assets/2bb7efe1-0b53-4f47-a74b-12bcdce9689c)                                                                           
                                                                        

## Recommendations for Mitigation:                                                                           

1. Enforce Strong Password Policies:                                                                           
    - Use a minimum password length of 12 characters with a combination of uppercase, lowercase, numbers, and special characters.

2. Disable Remote Access for MySQL:                                                                           
    - Modify the MySQL configuration to restrict access to only trusted IP addresses.

3. Enable SSL/TLS Encryption for MySQL:                                                                           
    - Configure MySQL to use SSL/TLS encryption to protect data in transit and prevent man-in-the-middle attacks.

4. Ensure proper configuration of SSL certificates to avoid version mismatches.                                                                           
    - Use trusted Certificate Authorities (CAs) to issue SSL certificates.
      
5. Limit User Privileges:                                                                           
    - Use least-privilege principles when creating MySQL users, ensuring they only have the necessary permissions.
   
7. Use Intrusion Detection and Prevention Tools:                                                                           
    - Deploy a Network Intrusion Detection System (NIDS) such as Snort or Suricata to monitor database traffic.

8. Use Rate-Limiting and Intrusion Prevention Tools:                                                                                                                                       
    - Install fail2ban to block IPs after multiple failed login attempts
