# Active Directory Helpdesk Lab

## Project Overview

This project simulates a small-business Active Directory environment using Windows Server 2022, Windows 11 Enterprise, and Oracle VirtualBox.

The lab was created to practice entry-level IT support tasks, including:

- Active Directory user administration
- Domain joining
- DNS configuration and troubleshooting
- Group Policy deployment
- Shared-folder permissions
- Automatic network-drive mapping
- Account lockout policy configuration and user-account recovery
- DHCP server configuration and automatic client addressing
- PowerShell-based user onboarding
- Event Viewer investigation

**Project status:** Completed

## Lab Architecture

| System | Role | IP address |
|---|---|---|
| DC01 | Domain Controller, DNS server, DHCP server, and file server | 192.168.50.10 |
| CLIENT01 | Windows 11 domain client | DHCP lease: 192.168.50.100 |

**VirtualBox Internal Network:** `ADLab`

```text
DC01
Windows Server 2022
Active Directory + DNS + DHCP + File Sharing
192.168.50.10
        |
        |
CLIENT01
Windows 11 Enterprise
DHCP: 192.168.50.100
DNS: 192.168.50.10
```

## Active Directory Structure

```text
brendanlab.local
└── Singapore Office
    ├── IT
    ├── Finance
    ├── Operations
    └── Workstations
```

## Work Completed

- Installed Windows Server 2022.
- Promoted DC01 to a Domain Controller.
- Created the `brendanlab.local` domain.
- Configured Active Directory-integrated DNS.
- Created OUs for IT, Finance, Operations, and Workstations.
- Created and managed domain-user accounts.
- Practised password resets and account disabling and enabling.
- Created the `IT Support Staff` security group.
- Installed Windows 11 Enterprise as CLIENT01.
- Configured IP addressing and DNS.
- Joined CLIENT01 to the domain.
- Verified domain login using `whoami`.
- Created a Group Policy that blocks Control Panel for IT users.
- Verified Group Policy using `gpupdate` and `gpresult`.
- Created the `\\DC01\IT` department share.
- Configured share and NTFS permissions using the `IT Support Staff` group.
- Verified that an authorised IT user could create and modify files.
- Verified that an unauthorised Operations user received Access Denied.
- Used Group Policy Preferences to automatically map the IT share as drive `I:`.
- Configured a domain account-lockout policy with a three-attempt threshold.
- Simulated, diagnosed, and resolved a locked domain-user account.
- Verified successful domain authentication after unlocking the account.
- Used Event Viewer Event ID 4740 to identify CLIENT01 as the lockout source.
- Installed and authorised the DHCP Server role on DC01.
- Created an active `192.168.50.0/24` scope with DNS options for `brendanlab.local`.
- Changed CLIENT01 to automatic addressing and verified its `192.168.50.100` lease.
- Diagnosed and repaired an APIPA address caused by incorrect network configuration.
- Simulated incorrect DNS by assigning `8.8.8.8` to CLIENT01.
- Confirmed that direct IP connectivity could work while private-domain name resolution failed.
- Restored the DHCP-provided DNS server `192.168.50.10` and verified domain resolution.
- Used PowerShell to create and configure the Michael Ong domain account.
- Added Michael to the IT OU and `IT Support Staff` security group.
- Verified Michael's domain login, mapped drive, and shared-folder access on CLIENT01.

## Validation and Troubleshooting Commands

```text
ping
ipconfig /all
ipconfig /release
ipconfig /renew
nslookup
whoami
hostname
gpupdate /force
gpresult /scope user /r
nltest /dsgetdc:brendanlab.local
nltest /sc_verify:brendanlab.local
```

PowerShell commands used included:

```powershell
Get-DnsClientServerAddress
Get-ADUser
New-ADUser
Add-ADGroupMember
Get-ADPrincipalGroupMembership
Get-Service DHCPServer
Get-DhcpServerv4Scope
Get-DhcpServerv4Binding
```

## Key Learning

- Organizational Units organise users and computers and provide targets for Group Policy.
- Security groups grant users access to resources.
- Active Directory depends on internal DNS to locate the Domain Controller and domain services.
- Share and NTFS permissions work together to control network-folder access.
- Group Policy centrally manages settings across domain users and computers.
- Drive mapping connects users to a central file share, while permissions determine whether they can open it.
- DHCP automatically provides clients with IP addresses, DNS servers, and other network settings.
- A `169.254.x.x` APIPA address indicates that the client could not obtain a DHCP lease.
- Event Viewer can identify the account and source computer involved in an account lockout.
- PowerShell enables repeatable administration, but commands should be checked and verified before use.

## Screenshots

- [Group Policy verification – Block Control Panel](screenshots/gpo-control-panel-policy-applied.png)
- [Automatic drive mapping – IT Shared Drive (I:)](screenshots/mapped-it-shared-drive.png)
- [Account lockout policy configuration](screenshots/account-lockout-policy.png)
- [Account unlock verification](screenshots/account-unlocked-verification.png)
- [DHCP client configuration](screenshots/dhcp-client-configuration.png)
- [DHCP address lease](screenshots/dhcp-address-lease.png)
- [PowerShell user onboarding verification](screenshots/powershell-user-onboarding-verification.png)
- [Event Viewer – John Tan account lockout](screenshots/event-4740-john-tan-lockout.png)

## Disclaimer

This is a personal home-lab project created for learning and portfolio purposes. It does not represent production Active Directory administration experience.
