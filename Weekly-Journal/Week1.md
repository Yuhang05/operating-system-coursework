[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---
# System Planning and Distribution Selection – Week 1

## Introduction
This week I set up the required virtualized environment for the Operating Systems coursework. The system consists of two virtual machines—a CLI-based Ubuntu Server and a GUI-based Xubuntu Workstation—running on Oracle VirtualBox. The architecture diagram below shows the host machine, VirtualBox, and both VMs with their respective network configurations.

### Interface of oracle VM
<img width="850" height="570" alt="VirtualBox Setup" src="https://github.com/user-attachments/assets/2c70e1dd-cab8-4f2a-b617-9075518c01a7" />

### VM Adapter Settings
Both VMs use: 

Adapter 1 (NAT): Provides internet access for updates and package installations.

Adapter 2 (Host-Only): Provides internal LAN connectivity between the server and workstation.

| Ubuntu-Server Network | Xubuntu-Workstation Network |
|------|------|
| <img src="https://github.com/user-attachments/assets/c53c896a-0fa4-475a-9b14-d13f57db2852" width="450"> | <img src="https://github.com/user-attachments/assets/6af32167-2bd3-4fb4-a53b-1d4d8237d7af" width="450" /> |
| <img src="https://github.com/user-attachments/assets/f8062fde-d896-4082-8763-9dae5cd9e905" width="450">| <img src="https://github.com/user-attachments/assets/234896ef-d921-415d-a9da-a81b8c6eb86c" width="450" /> |

## System Architecture Diagram

This diagram illustrates the relationship between the host machine, VirtualBox hypervisor, and the two virtual machines. The design ensures both external connectivity (via NAT) and an isolated internal LAN for server–workstation communication.

<img width="443" height="491" alt="System Architecture Diagram" src="https://github.com/user-attachments/assets/88fded5b-96b8-4326-8717-c46e35642f9f" />

## Network Configuration Documentation

Both VMs were configured with two network adapters in VirtualBox to meet the coursework requirements.

| Adapters | Ubuntu Server | Xubuntu Workstation |
|-----|-----|-----|
| Adapter 1：NAT  | Provides internet access for updates and package downloads.| Provides internet access for updates and package downloads. |
| Adapter 2: Host-Only | Host-only IP: 192.168.56.103.<br> Used for internal communication with the workstation (SSH/Ping). | Host-only IP: 192.168.56.104. <br> Used to access the Ubuntu Server via SSH. |

## Distribution Selection Justification
For the server environment, I selected Ubuntu Server 24.04.3 LTS. 

### Reasons for choosing Ubuntu Server 24.04.3 LTS:

Long-Term Support (LTS): Ubuntu 24.04 LTS provides 5+ years of security updates, ensuring stability throughout the duration of the coursework.

Extensive Documentation: Ubuntu has one of the largest communities and most comprehensive documentation, which is essential for troubleshooting and learning.

Compatibility with VirtualBox: Ubuntu is widely tested and known to run smoothly on VirtualBox without needing additional drivers or kernel modules.

Package Availability: The APT package manager provides access to thousands of precompiled packages, which simplifies installing tools required for later weeks (SSH, Apache, cron, firewall tools, etc.).

Industry Use: Ubuntu Server is one of the most commonly used Linux distributions in cloud, container, and DevOps environments, making it relevant for real-world skills.

#### Alternatives considered:

Debian: Very stable but updates slower; Ubuntu (based on Debian) offers newer software for learning purposes.

CentOS Stream / Rocky Linux: Good for enterprise RPM-based systems, but less beginner-friendly and fewer tutorials targeted at students.

Fedora Server: Up-to-date but not ideal for long-term coursework due to short life cycle.

Overall, Ubuntu Server provides the best balance between usability, documentation, performance, and long-term stability.

[1]


## Workstation Configuration Decision

For the workstation, I selected Xubuntu (XFCE desktop environment) instead of a full Ubuntu Desktop.

### Reasons for choosing Xubuntu:

Lightweight: XFCE uses fewer system resources (RAM/CPU), allowing the VM to run smoothly even with limited hardware.

Faster boot and shutdown: Makes the workflow more efficient during repetitive tasks.

Stable and simple UI: XFCE provides a clean interface without heavy animations, ideal for a workstation that will mainly be used for SSH, file editing, browser testing, and screenshot documentation.

Better performance in VirtualBox: XFCE environments are known to perform better than GNOME inside virtualization environments.

#### Alternatives considered:

Ubuntu Desktop (GNOME): Too heavy and slow inside VirtualBox on typical student hardware.

Kubuntu (KDE Plasma): Beautiful interface but more resource-intensive.

Linux Mint: Suitable but unnecessary since Xubuntu already meets all GUI requirements.

Xubuntu provides the most efficient GUI environment for interacting with the Ubuntu Server through SSH and performing coursework tasks.

[2]


## Ping Test (Workstation → Server)

The workstation successfully pings the server over the host-only network, proving that internal LAN communication is working.

<img width="850" height="570" alt="Xubuntu-Workstation ping test" src="https://github.com/user-attachments/assets/4a1cfe97-8843-47a1-932e-8d29099b141a" />

## SSH Remote Login

The workstation successfully logs into the server via SSH, confirming proper network configuration.

<img width="1270" height="800" alt="Xubuntu-Workstation ssh remote login " src="https://github.com/user-attachments/assets/c384369d-9180-4b01-b6c1-e1b99356829c" />

## CLI System Specification Documentation

The following commands were executed on the Ubuntu Server VM to document its system configuration.

<img width="1280" height="480" alt="Ubuntu-Server CLI code_1" src="https://github.com/user-attachments/assets/f6fb49d9-aaea-42b8-800e-11babeeeede4" />

<img width="1280" height="920" alt="Ubuntu-Server CLI code_2" src="https://github.com/user-attachments/assets/ddd45f2d-21ac-4d0e-a481-1d651437c848" />

| CLI | specifications |
|-----|-----|
| uname <br> (This command displays detailed kernel and system information.) | Kernel version: Linux 6.8.0-87-generic <br> Architecture: x86_64 <br> Operating system: GNU/Linux <br> The system is running inside a VirtualBox virtual machine |
| free <br> (This command shows memory usage in a human-readable format.) | Total RAM: ~ 2 GB <br> Used RAM and cached memory values indicate normal system operation. <br> Swap usage is 0, meaning the system has not needed swap memory yet. |
| df -h <br> (This command displays storage usage on all mounted filesystems.) | Root filesystem: /dev/sda2 <br> Disk size: 25 GB <br> Usage: ~ 12%, leaving plenty of space for logs and future labs <br> Other virtual filesystems (tmpfs, /run) are also shown |
| ip addr <br> (This command lists all network interfaces and their assigned IP addresses.) | NAT interface (enp0s3) → IP: 10.0.2.15 <br> Host-only interface (enp0s8) → IP: 192.168.56.103 <br> Confirms the machine is connected to both networks. |
| lsb_release <br> (This command provides Linux distribution details.) | Distributor ID: Ubuntu <br> Description: Ubuntu 24.04.3 LTS <br> Codename: noble <br> Confirms this VM uses the correct LTS version required for stability |

## Summary
This architecture supports both external connectivity (via NAT) and an isolated internal LAN (via Host-only), enabling SSH administration and inter-VM communication required for later weeks (firewall, services, automation, etc.).

## Reference
[1] J. Wallen, “10 Reasons To Choose Ubuntu Server Over the Competition,” TheNewStack, Nov. 24, 2024. [Online]. Available: https://thenewstack.io/10-reasons-to-choose-ubuntu-server-over-the-competition/  [Accessed: Nov. 7, 2025].

[2] “Debian vs Ubuntu: Which is best?,” ServerAcademy.com, Jun. 4, 2024. [Online]. Available: https://serveracademy.com/blog/debian-vs-ubuntu-which-is-best/. [Accessed: Nov. 7, 2025].
