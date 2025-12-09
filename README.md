<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment on Azure </h1>
This repository contains instructions and configurations for deploying an on-premises Active Directory environment on Azure Virtual Machines. The steps outlined in this repository demonstrate the setup and management of Active Directory Domain Services within a cloud-based environment.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2 Gen 2)


<h2>Deployment and Configuration Steps</h2>

**1. Install Active Directory**
- Login to `DC-1`
  - Use the credentials:
    - Username: 
    - Password: 
- Install Active Directory Domain Services
  - Open Server Manager and install the Active Directory Domain Services role.
- Promote as a Domain Controller
  - Set up a new forest with the domain name `mydomain.com` (or any preferred name).
  - Restart the server after promotion.
- Login to `DC-1` as Domain User
  - Use the credentials:
    - Username: `mydomain.com\`


<img width="1129" height="809" alt="image" src="https://github.com/user-attachments/assets/17312f73-2187-4b6d-bac6-3b085e5b5c20" />
<img width="1232" height="762" alt="image" src="https://github.com/user-attachments/assets/c3bf50f5-509e-4737-824c-3b27704116ab" />
<img width="2446" height="688" alt="image" src="https://github.com/user-attachments/assets/c20921d1-04c4-4762-b366-c14c31ced9fa" />
<img width="1142" height="816" alt="image" src="https://github.com/user-attachments/assets/d192f184-c3c5-4a4e-afef-0c80197b2632" />


**2. Create a Domain Admin User**
- Open Active Directory Users and Computers (ADUC)
- Create Organizational Units (OUs)
  - Create an OU named `_EMPLOYEES`.
  - Create another OU named `_ADMINS`.
- Create a New Employee User
  - Add a user named "Jane Doe" with the following details:
    - Username: `jane_admin`
    - Password: `Cyberlab123!`
- Add User to Security Group
  - Add `jane_admin` to the Domain Admins Security Group.
- Log in as `jane_admin`
  - Log out from `DC-1` and log back in using:
    - Username: `mydomain.com\jane_admin`
    - Password: `Cyberlab123!`
  - Use `jane_admin` as the admin account from this point forward.


<img width="1384" height="1118" alt="image" src="https://github.com/user-attachments/assets/db49571a-45d3-47fd-8a6c-4662272a63fe" />
<img width="1368" height="1090" alt="image" src="https://github.com/user-attachments/assets/f7a354a0-cbf0-4ea7-9309-30badf44c5a9" />
<img width="1328" height="808" alt="image" src="https://github.com/user-attachments/assets/db66efae-935d-4665-9054-7afd0a783300" />
<img width="2670" height="1476" alt="image" src="https://github.com/user-attachments/assets/07239bcd-60d5-49ef-aed7-bce9c174c9d1" />
<img width="1302" height="1072" alt="image" src="https://github.com/user-attachments/assets/15cc7317-a1da-4524-94c1-3523fa31727d" />
<img width="1302" height="1072" alt="image" src="https://github.com/user-attachments/assets/db0d058a-f887-4adf-b74b-583f32c70634" />
<img width="1066" height="940" alt="image" src="https://github.com/user-attachments/assets/1560f6fb-da50-470f-a73b-eac81db40d21" />


 
**3. Join `Client-1` to the Domain**
- Login to `Client-1` as Local Admin
- Join `Client-1` to the Domain
  - Change the system properties to join the domain `mydomain.com.`
  - Restart `Client-1` after joining.
- Verify in ADUC
  - Log in to `DC-1` and confirm that `Client-1` appears in the Active Directory Users and Computers tool.
- Organize `Client-1` in ADUC
  - Create an OU named `_CLIENTS`.
  - Drag `Client-1` into the `_CLIENTS OU`.


<img width="1842" height="1314" alt="image" src="https://github.com/user-attachments/assets/7ba50abd-a735-4b28-9f34-4f63ff4a6078" />
<img width="852" height="768" alt="image" src="https://github.com/user-attachments/assets/d64f2603-f5c1-490b-8b0a-2bedf4e1d79e" />
<img width="842" height="548" alt="image" src="https://github.com/user-attachments/assets/599af4c0-b4b8-4469-9bbb-36b4ae31f848" />
<img width="554" height="312" alt="image" src="https://github.com/user-attachments/assets/96e887fd-728d-4476-ade5-a9fefdae5e64" />
<img width="1258" height="1060" alt="image" src="https://github.com/user-attachments/assets/f7b22bd5-79ca-4551-aa71-322a1e831e83" />
<img width="1148" height="780" alt="image" src="https://github.com/user-attachments/assets/e294e203-cad8-4d9a-8579-7a4b966dc59f" />
<img width="1214" height="524" alt="image" src="https://github.com/user-attachments/assets/380e23ac-c819-415a-bfc0-1d7e6cea7916" />
<img width="1456" height="650" alt="image" src="https://github.com/user-attachments/assets/da5bb6b5-c0c8-4ab7-9531-e63dfc68db11" />


**4. Setup Remote Desktop for Non-Administrative Users on Client-1**

- Login to `Client-1` as `mydomain.com\jane_admin`
  - Use the credentials for `jane_admin`.
- Allow Domain Users Access to Remote Desktop
  - Open system properties.
  - Click on "Remote Desktop."
  - Allow "domain users" access to Remote Desktop.
- Test Remote Desktop Access
  - You can now log into `Client-1` as a normal, non-administrative user.
   -Note: Typically, this configuration is managed using Group Policy for multiple systems.


<img width="1686" height="470" alt="image" src="https://github.com/user-attachments/assets/a4064812-d52e-47de-9d3c-99a9890815d8" />
<img width="650" height="220" alt="image" src="https://github.com/user-attachments/assets/2105bba9-3068-4f4d-bafb-d04d35f51f39" />
<img width="802" height="416" alt="image" src="https://github.com/user-attachments/assets/6447a23a-b191-4adf-a33c-1e22862b7bd0" />


**5. Create Additional Users and Test Login**

- Login to `DC-1` as `jane_admin`
  - Use the credentials for `jane_admin`.
- Open PowerShell ISE as Administrator
  - Launch PowerShell ISE with administrative privileges.
- Create Users with a Script
  - Create a new file and paste the provided [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it.
  - Run the script to create multiple user accounts.
- Verify Accounts in ADUC
  - Open Active Directory Users and Computers (ADUC).
  - Observe the newly created accounts in the `_EMPLOYEES OU`.
- Test Login
  - Attempt to log into `Client-1` using one of the newly created accounts.
  - Ensure the account password matches what is specified in the script.


<img width="926" height="534" alt="image" src="https://github.com/user-attachments/assets/0d36ca3b-fc26-4c9d-884e-8834091bcfe9" />
<img width="2112" height="1540" alt="image" src="https://github.com/user-attachments/assets/fb469ad0-8a41-480c-82c3-19b86839f162" />
<img width="2150" height="984" alt="image" src="https://github.com/user-attachments/assets/9311d8d0-8217-4301-bf4c-74a959a574a4" />
<img width="1520" height="964" alt="image" src="https://github.com/user-attachments/assets/a1aa8561-0965-4e8b-a41c-22c1182e7927" />
<img width="1570" height="1012" alt="image" src="https://github.com/user-attachments/assets/06722553-bd39-43e7-a4f3-a612938bf5d0" />
<img width="923" height="594" alt="image" src="https://github.com/user-attachments/assets/831dce65-d2ab-4149-9495-f41cb27cc3b8" />
<img width="1250" height="762" alt="image" src="https://github.com/user-attachments/assets/3411c221-511a-4071-ab52-40d307de7b38" />


<h2>Purpose</h2>
The purpose of this repository is to provide a comprehensive guide for deploying Active Directory through virtual machines on Azure. This implementation is intended to replicate on-premises infrastructure within a cloud environment, enabling scalable and manageable domain services for various organizational needs.
