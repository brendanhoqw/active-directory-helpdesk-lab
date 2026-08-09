# Active Directory Helpdesk Lab

## Project Overview

This project simulates a small-business Active Directory environment using Windows Server 2022, Windows 11 Enterprise, and Oracle VirtualBox.

The lab was created to practise entry-level IT support tasks, including:

- Active Directory user administration
- Domain joining
- DNS configuration
- Group Policy deployment
- Shared-folder permissions
- Automatic network-drive mapping

**Project status:** Active development

## Lab Architecture

| System | Role | IP address |
|---|---|---|
| DC01 | Domain Controller, DNS server, and file server | `192.168.50.10` |
| CLIENT01 | Windows 11 domain client | `192.168.50.20` |

```text
VirtualBox Internal Network: ADLab

DC01
Windows Server 2022
Active Directory + DNS + File Sharing
192.168.50.10
        |
        |
CLIENT01
Windows 11 Enterprise
192.168.50.20
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
- Promoted `DC01` to a Domain Controller.
- Created the `brendanlab.local` domain.
- Configured Active Directory-integrated DNS.
- Created OUs for IT, Finance, Operations, and Workstations.
- Created and managed domain-user accounts.
- Practised password resets and account disabling and enabling.
- Created the `IT Support Staff` security group.
- Installed Windows 11 Enterprise as `CLIENT01`.
- Configured static IP addressing and DNS.
- Joined `CLIENT01` to the domain.
- Verified domain login using `whoami`.
- Created a Group Policy that blocks Control Panel for IT users.
- Verified Group Policy using `gpupdate` and `gpresult`.
- Created the `\\DC01\IT` department share.
- Configured share and NTFS permissions using the `IT Support Staff` group.
- Verified that an authorised IT user could create and modify files.
- Verified that an unauthorised Operations user received Access Denied.
- Used Group Policy Preferences to automatically map the IT share as drive `I:`.

## Validation and Troubleshooting Commands

```text
ping
ipconfig /all
nslookup
whoami
hostname
gpupdate /force
gpresult /scope user /r
```

## Key Learning

- Organizational Units organise users and computers and provide targets for Group Policy.
- Security groups grant users access to resources.
- Active Directory depends on DNS to locate domain services.
- Share and NTFS permissions work together to control network-folder access.
- Group Policy centrally manages settings across domain users and computers.
- Drive mapping provides users with a convenient connection to a central file share.

## Screenshots

- [Group Policy verification – Block Control Panel](screenshots/gpo-control-panel-policy-applied.png)
- [Automatic drive mapping – IT Shared Drive (I:)](screenshots/mapped-it-shared-drive.png)
## Planned Next Steps

- Configure password and account-lockout policies.
- Simulate and resolve a locked user account.
- Configure DHCP.
- Troubleshoot incorrect DNS settings.
- Troubleshoot failed domain logins and Group Policy application.
- Add PowerShell automation for user creation.
- Add screenshots and detailed troubleshooting documentation.

## Disclaimer

This is a personal home-lab project created for learning and portfolio purposes. It does not represent production Active Directory administration experience.
