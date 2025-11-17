# ⚠️🌐 Threat Hunting - Device Exposure To the Internet
---
## :bookmark_tabs: Scenario

During routine maintenance, the security team is tasked with investigating any VMs in the shared services cluster (handling DNS, Domain Services, DHCP, etc.) that have mistakenly been exposed to the public internet. The goal is to identify any misconfigured VMs and check for potential brute-force login attempts/successes from external sources.

## Time Line Summary and Investigation:

ENDPOINT-LAB-ZA has been internet facing for several days:

Last Internet Facing Time : 2025-11-17T20:30:05.8957499Z

<img width="846" height="657" alt="Screenshot 2025-11-17 at 3 45 59 PM" src="https://github.com/user-attachments/assets/f6f81b89-e4e3-46a1-9cda-25b91a8dd5a2" />

### Check most failed logons
Several bad actions have been attempting to log into the target machine (ENDPOINT-LAB-ZA)

<img width="823" height="413" alt="Screenshot 2025-11-17 at 3 56 17 PM" src="https://github.com/user-attachments/assets/a1493871-56a1-46f1-8c23-ff33b73cc9b1" />

### Check to see if any of the listed IP's successfully logged onto the PC
Confirmed none of the listed IP's above were able to successfully log onto the PC

<img width="846" height="369" alt="Screenshot 2025-11-17 at 3 59 10 PM" src="https://github.com/user-attachments/assets/24a10e06-749c-4734-b7b7-170edb47554a" />

### Check to see if there were any successes under those IP addresses

<img width="852" height="416" alt="Screenshot 2025-11-17 at 4 16 26 PM" src="https://github.com/user-attachments/assets/1730b339-bf23-4ee9-82aa-5a8914aaebea" />

### Check to see if there were any failed connections from the Network using the 'zubadmin' user account. 
Doing this will allow us to identify if anyone is attempting to brute-force our PC. Confirmed they no results were found.

<img width="862" height="338" alt="Screenshot 2025-11-17 at 4 20 53 PM" src="https://github.com/user-attachments/assets/f06127a8-6d55-4d65-8bbd-cb6c1fc28d47" />

The only successful remote/network logons were for the 'zubadmin' account (5 total)
There were zero (0) failed logons for the labuser account, indicating that a brute force attack for this account didnt take place and a one password guess is unlikely. 

Though the device was exposed to the internet and clear brute force attempts have taken place, there is no evidence of any brute force success or unauthorized access from the legitimate account 'zubadmin'

### Relevant MITRE ATT&CK TTPs

- T1110 – Brute Force
    Multiple rapid authentication attempts indicate brute-force guessing.

- T1110.001 – Password Guessing
    Repeated attempts to guess individual user credentials.

- T1110.003 – Password Spraying
    Attempts using common passwords across multiple usernames.

- T1078 – Valid Accounts
    Attackers tried to authenticate using legitimate account names but did not succeed.

### Response Actions
1. Hardened the NSG attached to windows-target-1 to allow only RDP traffic from specific endpoints (no internet access)
Implemented internet access
2. Implemented Account Lockout Policy 



