# IT Help Desk Simulation

**Short Summary:**  
A hands-on training guide and virtual lab demonstrating **Active Directory (AD DS), Group Policy, CMD troubleshooting, remote support tools, and ticketing workflows** — designed for entry-level helpdesk practitioners to build practical skills and clear interview talking points.

**Skills Demonstrated:**
- Active Directory installation & administration (users, groups, OUs, delegation)
- Group Policy creation & troubleshooting (`gpupdate`, `gpresult`, RSOP)
- CMD essentials (`ipconfig`, `ping`, `net user`, `net use`)
- Shared drives & NTFS permissions (manual and automated mapping)
- Remote support workflows (RDP, Remote Assistance, Remote Registry)
- Ticketing system practice (Spiceworks)

---

## I. Introduction
This briefing document summarizes key concepts and practical skills essential for entry-level IT Helpdesk and Support roles, drawing from a series of instructional videos. The primary focus is on establishing a foundational understanding of Active Directory, common CMD commands, software deployment, and troubleshooting, all within a virtual lab environment.

## II. Building Your IT Lab Environment
A crucial step for aspiring IT professionals is to create a personal lab environment. This hands-on experience allows for practical learning, skill development, and the ability to articulate technical knowledge confidently in job interviews.

### A. Virtualization Software and Server Installation
- **VirtualBox / VMware**: Use virtualization software to create virtual machines (VMs) and run multiple operating systems on a single host.
- **System Requirements**: Check host RAM and CPU; enable virtualization in BIOS if required.
- **Server 2016 Installation**: Download the Server 2016 ISO and choose **Desktop Experience** for a GUI.
- **VM Configuration**
  - Rename the server to a short, clear name (e.g., `Server2016`).
  - Set system options for "best performance" to reduce VM lag.
  - Remove the mounted ISO after installation to enable normal boot.
  - Configure a **static IP** for consistent VM networking (example: `10.1.10.2`).
  - Use a **Host-Only Adapter** (or equivalent) so lab VMs can communicate in an isolated network.

### B. Windows 10 Client Installation
- **Windows 10 Pro ISO**: Use Pro (Home cannot join a domain).
- **Local Administrator Account**: Create a local admin for recovery if the machine falls off the domain.
- **RSAT Tools**: Install Remote Server Administration Tools on Windows 10 for AD, GPO, and server management from the client.
- **Join to Domain**: Rename the client (e.g., `DesktopOne`) and join it to the Active Directory domain created on the server.

## III. Active Directory Domain Services (AD DS)
Active Directory is core to Windows Server environments for managing users, computers, and resources.

### A. Installation and Promotion
- **Install AD DS role** using Server Manager.
- **Promote to Domain Controller**: create a new forest and define a domain name (example: `techtone.com`).

### B. User and Group Management
- **Active Directory Users and Computers (ADUC)** is the primary management tool.
- **Creating Accounts**
  - Create a dedicated **Helpdesk** account (consider copying an admin account to inherit permissions).
  - Create standard user accounts (e.g., `Patty`).
- **Organizational Units (OUs)**: create OUs such as `HR`, `IT` to organize users and computers.
- **Security vs. Distribution Groups**
  - *Distribution Groups* are for email lists.
  - *Security Groups* control access to resources (shared drives, applications, VPN).
- **Search Tips**: Search the *Entire Directory* in ADUC; enable *Advanced Features* to view object metadata (location, attributes).
- **Recycle Bin**: enable AD Recycle Bin to recover deleted objects.

### C. Common Active Directory Issues & Troubleshooting
- **Account Lockout**: unlock in ADUC -> Account tab -> *Unlock account*.
- **Disabled Account**: re-enable in ADUC.
- **Password Reset**: reset via ADUC; consider *User must change password at next login*.
- **Account Expiration**: extend or set to *Never* in ADUC.
- **Trust Relationship Failure**: log in with a local admin, remove the computer from the domain, reboot, and rejoin.
- **Account Lockout Status Tool**: use Microsoft’s lockout troubleshooting tool to identify lockout sources and events.

### D. Delegate Control
- Use **Delegate Control** on OUs to grant limited permissions (e.g., reset password) to junior staff or consultants.

## IV. Command Line (CMD) Essentials
Key commands every helpdesk tech should know:
- `ipconfig` / `ipconfig /all` — view network configuration (IP, DHCP, DNS).
- `ping <IP|hostname>` (and `ping -t`) — test connectivity.
- `net use` — list mapped network drives.
- `net user <username> /domain` — view domain user details (password dates, group membership).
- `gpupdate /force` — force Group Policy update.
- `gpresult /r` — view Resultant Set of Policy applied to user/computer.

## V. Group Policy Management (GPM)
- Open **Group Policy Management** from Server Manager.
- **Password Policy**: set complexity, max age (e.g., 90 days), and lockout thresholds (e.g., 5 invalid attempts).
- **Disable Features**: GPOs can disable Task Manager or Start Menu shutdown options for users.
- **RSOP**: use RSOP Wizard or `gpresult /r` to verify applied policies.

## VI. Shared Drives and Permissions
- **Creating Shares**: create shared folders (e.g., `HR`, `Personal`) in File and Storage Services.
- **NTFS Permissions**: assign permissions to security groups, avoid using `Everyone`.
- **Mapping Network Drives**
  - Manual: Map in File Explorer using `\\Server2016\ShareName` and select *Reconnect at sign-in*.
  - Automatic: Map drives via AD profile properties using `%USERNAME%` for personal drives.
- **Security**: restrict sensitive folders (HR, Legal) to specific security groups.

## VII. Remote Access and Support Tools
### A. Remote Desktop Protocol (RDP)
- Enable *Allow remote connections* in System Properties.
- Add the Helpdesk security group to permitted users.
- Use RDP client with hostname or IP address.
- Admin shares (e.g., `\\DesktopTwo\C$`) provide access to local drives if you have admin credentials.

### B. Windows Remote Assistance
- User generates an invitation file and password; IT connects interactively and can request control.

### C. Remote Registry Editing
- Advanced troubleshooting: use `regedit` to connect to remote registries when services and privileges allow. (Be careful — registry edits can break systems.)

## VIII. Ticketing Systems
- **Spiceworks**: a recommended free ticketing system with community support. Practice ticket workflow: create, assign, document, escalate, and close.
- **Remote Session Integration**: ticketing tools often integrate with remote tools (TeamViewer, AnyDesk, Bomgar) to start screen shares, elevate privileges, transfer files, and chat.

## IX. Conclusion
This briefing covers critical areas for entry-level IT Helpdesk roles. Building a personal lab, understanding Active Directory, mastering CMD commands, managing Group Policy, setting up shared drives, using remote access tools, and practicing with ticketing systems are foundational skills. Hands-on practice and the ability to describe these skills clearly in interviews will help you advance in IT support.
