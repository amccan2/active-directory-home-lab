# active-directory-home-lab
Built a Windows Server 2022 active directory domain server home lab in VirtualBox with DNS, DHCP, IIS, and NAT routing. Automated user account creation via PowerShell and integrated Windows 10 endpoints.

# Windows Server 2022 Enterprise Infrastructure & Active Directory Lab

## Overview
This home lab showcases the end-to-end deployment, configuration, and administration of an enterprise core infrastructure using Windows Server 2022 and Windows 10 inside Oracle VirtualBox. The project demonstrates Active Directory Domain Services (AD DS) management, core network services (DHCP, DNS, Remote Access/Routing), web services hosting (IIS), storage management, client endpoint integration, and automated user provisioning via PowerShell.

---

## Lab Architecture & Technical Specifications

* **Hypervisor:** Oracle VirtualBox
* **Domain Controller / Infrastructure Server (`DC`):** Windows Server 2022 Standard
  * **Domain Name:** `mydomain.com`
  * **Primary Network Adapters:**
    * Adapter 1 (WAN/Internet): NAT (`_INTERNET_` - `10.0.2.15`)
    * Adapter 2 (LAN): Internal Network (`X_internal_X` - Static IP `172.16.0.1`)
  * **Active Server Roles:** AD DS, DHCP, DNS, Remote Access (NAT), IIS, File and Storage Services
* **Client Workstation (`CLIENT1`):** Windows 10 Enterprise
  * **Network Adapter:** Internal Network (`intnet`) set to DHCP (`172.16.0.100`)

---

## Core Server Setup & Network Configuration

### 1. Server Manager Role Overview
Displays healthy status across all primary infrastructure roles managed on the Domain Controller.

<img width="1365" height="817" alt="image" src="https://github.com/user-attachments/assets/8a96ed0f-ac6e-4076-8a88-c95461478147" />
<img width="1232" height="762" alt="image" src="https://github.com/user-attachments/assets/fef9d147-660e-4b4a-b694-98240e30bff7" />

---

### 2. Dual Network Adapter Provisioning
Configured dual virtual network adapters to separate external internet connectivity from the internal VirtualBox lab network (`intnet`).

<img width="741" height="480" alt="image" src="https://github.com/user-attachments/assets/279c6c85-2018-4a27-86e0-7c610217db29" />

---

### 3. External Network Adapter IPv4 Configuration (`_INTERNET_`)
Configured WAN interface via DHCP for external internet connectivity while binding local host DNS resolution (`127.0.0.1`) to the active Domain Controller.

<img width="528" height="477" alt="image" src="https://github.com/user-attachments/assets/ef5cda67-d2f1-4a57-8814-1030ec61f639" />

---

### 4. Internal LAN Adapter IPv4 Configuration (`X_internal_X`)
Assigned static IP parameters (`172.16.0.1/24`) on the internal interface to act as the primary gateway and local DNS server for all domain endpoints.

<img width="537" height="555" alt="image" src="https://github.com/user-attachments/assets/06d37743-882e-4c25-9e3a-f536647f5c47" />


---

## Server Roles & Implementation Proof

### 5. Local Server Properties & Domain Binding
Displays the Domain Controller (`DC`) configuration, confirming integration with `mydomain.com` alongside both configured IP network interfaces.

<img width="1270" height="732" alt="image" src="https://github.com/user-attachments/assets/94ae84e5-db0e-4420-b4ea-1499454149fb" />

---

### 6. Managed Server Infrastructure Inventory
Shows central server inventory in Server Manager with active status reporting across both external and internal IPv4 network addresses.

<img width="1264" height="710" alt="image" src="https://github.com/user-attachments/assets/34ff52e6-eade-4941-aec7-a0a7f6871484" />

---

### 7. Active Directory Domain Services (AD DS) Operations
Displays active domain controller status and Directory Service operational logs for domain management.

<img width="1163" height="718" alt="image" src="https://github.com/user-attachments/assets/d56189e2-6475-4bbf-8d9c-652fe8134794" />

---

### 8. Domain Name System (DNS) Setup
Configured internal DNS zones for local Active Directory name resolution and domain lookup across the network.

<img width="1292" height="756" alt="77288a32-b084-46fc-9a56-242310adacd9" src="https://github.com/user-attachments/assets/2a132b89-555c-4e8c-90c2-b4eb8bfb64f7" />

---

### 9. File and Storage Services
Initialized local volume and file storage services to prepare the environment for domain file shares and administrative storage.

<img width="1175" height="705" alt="image" src="https://github.com/user-attachments/assets/fa8490c4-83fd-4491-bc1d-a4d7fa4e92f2" />

---

### 10. Internet Information Services (IIS) Setup
Installed and configured the web server role to enable local intranet applications and simulate corporate web hosting.

<img width="1159" height="723" alt="image" src="https://github.com/user-attachments/assets/a35d5425-c286-4c1c-b2c1-f04b3f6a9e4f" />

---

### 11. Remote Access & Routing (NAT) Setup
Configured Remote Access routing and Network Address Translation (NAT) to allow isolated internal domain clients (`172.16.0.0/24`) to securely route traffic to the external interface.

<img width="1172" height="704" alt="image" src="https://github.com/user-attachments/assets/a860ddf8-75f3-43ff-a66c-db863ce75a36" />

---

### 12. Active DHCP Scope Leases
Verified that the Windows Server 2022 DHCP service dynamically leased IP address `172.16.0.100` to `CLIENT1.mydomain.com` over the internal network.

<img width="1202" height="743" alt="image" src="https://github.com/user-attachments/assets/134ee03d-b635-4187-b2ee-f6d2825683a5" />

---

### 13. Active Directory Computer Integration
Confirmed successful domain joining in Active Directory Users and Computers (ADUC), where `CLIENT1` is registered as a trusted computer object under `mydomain.com`.

<img width="1204" height="715" alt="image" src="https://github.com/user-attachments/assets/d973f485-37bb-49c1-ab6e-826cf18f0db9" />

---

## Automated User Provisioning & PowerShell Scripts

### Repository Files
* **User Creation Script:** [`1_CREATE_USERS.ps1`](AD_PS-master/1_CREATE_USERS.ps1)
* **Name Generator Script:** [`Generate-Names-Create-Users.ps1`](AD_PS-master/Generate-Names-Create-Users.ps1)
* **User Input List:** [`names.txt`](AD_PS-master/names.txt)

---

### 14. User Creation Script Execution (`1_CREATE_USERS.ps1`)
Automated the mass creation of Active Directory user accounts using PowerShell. The script reads full names from an external text file (`names.txt`), extracts the first initial and last name to generate standardized SAM account usernames, assigns a default credentials password (`Password1`), and provisions accounts directly into Active Directory.

<img width="1024" height="482" alt="image" src="https://github.com/user-attachments/assets/a0a73f86-f3f4-4928-887b-a1d8ca44db60" />

---

### 15. Source User Name List (`names.txt`)
A plain text list containing full names (first and last) used by `1_CREATE_USERS.ps1` to automatically build active domain user accounts. Any user generated from this list can log in directly to the domain-joined client workstation (`CLIENT1`) using the standard assigned password (`Password1`).

<img width="1223" height="748" alt="image" src="https://github.com/user-attachments/assets/9a5e7f95-804e-47c4-b9a3-ca71edfda5e4" />

---

### 16. Random Name Generator Function (`Generate-Names-Create-Users.ps1`)
A custom PowerShell function designed to dynamically generate random first and last name combinations using structured consonant and vowel arrays for continuous bulk user creation testing.

<img width="1244" height="760" alt="image" src="https://github.com/user-attachments/assets/395b0db8-040c-42a6-816a-5d149f9388cb" />

---

### 17. Active Directory Object Creation Loop
The primary execution loop of the random name script, which loops through the target account count, formats user object properties, sets `-PasswordNeverExpires $true`, and places newly provisioned user accounts directly into the `_EMPLOYEES` Organizational Unit (OU).

<img width="1245" height="731" alt="image" src="https://github.com/user-attachments/assets/cd0dd372-c876-4a14-b0d6-ca84447d92c5" />


## Technical Skills Demonstrated
* **Directory & Identity Management:** AD DS installation, OU structuring, and endpoint domain integration.
* **Network Services:** Dynamic DHCP leasing, DNS zone management, and static dual-homed NAT routing.
* **Web & Storage Administration:** IIS deployment and File/Storage role initialization.
* **Automation & Troubleshooting:** PowerShell scripting and virtual switch troubleshooting.
