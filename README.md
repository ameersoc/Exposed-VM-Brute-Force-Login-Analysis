# Exposed-VM-Brute-Force-Login-Analysis
Overview

This project focused on identifying virtual machines within a shared services environment that were unintentionally exposed to the public internet. The objective was to detect any brute-force login attempts, verify if any of them were successful, and implement security controls to prevent future exposure.


<img width="1000" height="1024" alt="image" src="https://github.com/user-attachments/assets/50081321-f197-4d30-b1fb-01ec13572c26" />


# Identified Internet-Exposed Devices

<img width="1000" height="650" alt="Screen Shot 2025-11-18 at 9 55 54 am" src="https://github.com/user-attachments/assets/36719670-67f9-4141-a2d4-62a4b81d78b8" />

# Investigated Brute-Force Login Attempts

I queried the DeviceLogonEvents table in Microsoft Sentinel and identified multiple failed login attempts originating from external IP addresses.
The screenshot shows each attacking IP, along with the total number of failed authentication attempts.

<img width="1000" height="812" alt="Screen Shot 2025-11-18 at 9 40 56 am" src="https://github.com/user-attachments/assets/c4ddbc1c-1587-4dcc-af85-cda2f3b7a954" />

# Analyzed Top 5 Failed Logon IPs for Successful Logins

To ensure no compromise occurred, I pivoted from the top 5 attacking IP addresses and checked whether any had successfully authenticated.
The query returned 0 successful logins, confirming that no unauthorized access had taken place.

<img width="1000" height="594" alt="Screen Shot 2025-11-18 at 10 16 21 am" src="https://github.com/user-attachments/assets/7f072cd0-4655-42c3-b67d-9c20749a8117" />

# Checked for Failed Login Attempts Against My Own Account

I reviewed all failed authentication attempts targeting my account name to ensure my credentials were not being attacked.
No suspicious or unusual activity was found.

<img width="1000" height="420" alt="Screen Shot 2025-11-18 at 10 32 03 am" src="https://github.com/user-attachments/assets/f4060e65-be01-43f8-8e43-d74ca022aef4" />

# Mapped Geolocation of All Successful Logon IP Addresses

To validate that only approved sources were connecting to the VM, I extracted all IP addresses associated with successful logins and checked their geolocation.
All successful logon IPs were confirmed to be legitimate and from expected regions.

<img width="1000" height="368" alt="Screen Shot 2025-11-18 at 10 44 41 am" src="https://github.com/user-attachments/assets/932ac50d-92b1-4f43-845e-c1b15c2daefc" />

# Mitigation & Hardening Actions

# Hardened Network Security Group (NSG) Configuration

I updated the NSG attached to the VM by:
* Restricting RDP access to only specific trusted IP addresses
* Removing any public inbound rules that could allow unauthorized internet exposure

# Implemented Authentication Security Controls

To strengthen access protection:
* Enabled Account Lockout Policy to prevent brute-force attacks
* Enforced Multi-Factor Authentication (MFA) for all user logins

# Outcome

This project demonstrates end-to-end SOC investigation and remediation skills, including threat hunting, log analysis, security hardening, and implementation of preventive controls. No unauthorized access was found, and the environment was secured against future brute-force attempts.
