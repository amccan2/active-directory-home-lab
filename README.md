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

[Drag and drop Server Manager Dashboard image here]

---

### 2. Dual Network Adapter Provisioning
Configured dual virtual network adapters to separate external internet connectivity from the internal VirtualBox lab network (`intnet`).

[Drag and drop Network Connections image here]

---

### 3. External Network Adapter IPv4 Configuration (`_INTERNET_`)
Configured WAN interface via DHCP for external internet connectivity while binding local host DNS resolution (`127.0.0.1`) to the active Domain Controller.

[Drag and drop Internet NIC IPv4 Settings image here]

---

### 4. Internal LAN Adapter IPv4 Configuration (`X_internal_X`)
Assigned static IP parameters (`172.16.0.1/24`) on the internal interface to act as the primary gateway and local DNS server for all domain endpoints.

[Drag and drop Internal NIC IPv4 Settings image here]

---

## Server Roles & Implementation Proof

### 5. Domain Name System (DNS) Setup
Configured internal DNS zones for local Active Directory name resolution and domain lookup across the network.

<img width="1292" height="756" alt="77288a32-b084-46fc-9a56-242310adacd9" src="https://github.com/user-attachments/assets/2a132b89-555c-4e8c-90c2-b4eb8bfb64f7" />

---

### 6. File and Storage Services
Initialized local volume and file storage services to prepare the environment for domain file shares and administrative storage.

<img width="1175" height="705" alt="image" src="https://github.com/user-attachments/assets/fa8490c4-83fd-4491-bc1d-a4d7fa4e92f2" />

---

### 7. Internet Information Services (IIS) Setup
Installed and configured the web server role to enable local intranet applications and simulate corporate web hosting.

[Drag and drop IIS Setup image here]

---

### 8. Remote Access & Routing (NAT) Setup
Configured Remote Access routing and Network Address Translation (NAT) to allow isolated internal domain clients (`172.16.0.0/24`) to securely route traffic to the external interface.

[Drag and drop Remote Access image here]

---

### 9. Active DHCP Scope Leases
Verified that the Windows Server 2022 DHCP service dynamically leased IP address `172.16.0.100` to `CLIENT1.mydomain.com` over the internal network.

[Drag and drop DHCP Leases image here]

---

### 10. Active Directory Computer Integration
Confirmed successful domain joining in Active Directory Users and Computers (ADUC), where `CLIENT1` is registered as a trusted computer object under `mydomain.com`.

[Drag and drop ADUC Computer Object image here]

---

## Technical Skills Demonstrated
* **Directory & Identity Management:** AD DS installation, OU structuring, and endpoint domain integration.
* **Network Services:** Dynamic DHCP leasing, DNS zone management, and static dual-homed NAT routing.
* **Web & Storage Administration:** IIS deployment and File/Storage role initialization.
* **Automation & Troubleshooting:** PowerShell bulk scripting and virtual switch troubleshooting.
