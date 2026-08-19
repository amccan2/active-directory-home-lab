# active-directory-home-lab
Built a Windows Server 2022 AD DS lab in VirtualBox with DNS, DHCP, IIS, and NAT routing. Automated user account creation via PowerShell and integrated Windows 10 endpoints.

# Windows Server 2022 Enterprise Infrastructure & Active Directory Lab

## Overview
This home lab showcases the end-to-end deployment, configuration, and administration of an enterprise core infrastructure using Windows Server 2022 and Windows 10 inside Oracle VirtualBox. The project demonstrates Active Directory Domain Services (AD DS) management, core network services (DHCP, DNS, Remote Access/Routing), web services hosting (IIS), storage management, client endpoint integration, and automated user provisioning via PowerShell.

---

## Lab Architecture & Technical Specifications

* **Hypervisor:** Oracle VirtualBox
* **Domain Controller / Infrastructure Server (`DC`):** Windows Server 2022 Standard
  * **Domain Name:** `mydomain.com`
  * **Primary Network Adapters:**
    * Adapter 1 (WAN/Internet): NAT (`10.0.2.15`)
    * Adapter 2 (LAN): Internal Network (`intnet`) – Static IP `172.16.0.1`
  * **Active Server Roles:** AD DS, DHCP, DNS, Remote Access (NAT), IIS, File and Storage Services
* **Client Workstation (`CLIENT1`):** Windows 10 Enterprise
  * **Network Adapter:** Internal Network (`intnet`) set to DHCP (`172.16.0.100`)

---

## Server Roles & Configuration Proof

### 1. Domain Name System (DNS) Setup
Configured internal DNS zones for local Active Directory name resolution and domain lookup for managed endpoints across the network.

<img width="1292" height="756" alt="77288a32-b084-46fc-9a56-242310adacd9" src="https://github.com/user-attachments/assets/2a132b89-555c-4e8c-90c2-b4eb8bfb64f7" />


---

### 2. File and Storage Services
Initialized local volume and file storage services to prepare the environment for domain file shares, administrative access, and central data storage.

[Drag and drop image_445515.png here]

---

### 3. Internet Information Services (IIS) Setup
Installed and configured the web server role to enable local intranet applications and simulate corporate web hosting within the domain environment.

[Drag and drop image_44a6eb.png here]

---

### 4. Remote Access & Routing (NAT) Setup
Configured Remote Access routing and Network Address Translation (NAT) to allow isolated internal domain clients (`172.16.0.0/24`) to securely route traffic out to the external network interface.

[Drag and drop image_44a6f3.png here]

---

### 5. Active DHCP Scope Leases
Verified that the Windows Server 2022 DHCP service dynamically leased the IP address `172.16.0.100` to `CLIENT1.mydomain.com` over the internal network.

[Drag and drop image_44a802.png here]

---

### 6. Active Directory Computer Integration
Confirmed successful domain joining by checking Active Directory Users and Computers (ADUC), where `CLIENT1` is registered as a trusted computer object under `mydomain.com`.

[Drag and drop image_44aaed.png here]

---

## Skills Demonstrated
* **Directory & Identity Management:** AD DS installation, OU structuring, and endpoint domain integration.
* **Network Services:** DHCP scope management, DNS zone configuration, and dual-homed NAT routing.
* **Web & Storage Administration:** IIS deployment and File/Storage role initialization.
* **Automation & Troubleshooting:** PowerShell bulk scripting and virtual switch troubleshooting.
