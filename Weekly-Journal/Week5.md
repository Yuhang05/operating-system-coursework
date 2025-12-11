[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---

# Week 5 – Advanced Security and Monitoring Infrastructure

## Introduction
This week focuses on strengthening the security posture of the Ubuntu Server through AppArmor access control, automatic security updates, Fail2ban intrusion detection, and the creation of two automation scripts: a security baseline verification script and a remote monitoring script.  
All work was performed from the Xubuntu Workstation using SSH.

## Access Control Implementation Using AppArmor

AppArmor provides mandatory access control (MAC) and restricts applications based on predefined security profiles.

To verify AppArmor status:

```
sudo aa-status
```

### AppArmor Status Output
- 123 profiles loaded  
- 28 profiles enforcing  
- Critical services such as `man`, `dhclient`, and `snapd` confined  

<img width="509" height="339" alt="aa-status" src="https://github.com/user-attachments/assets/72812cef-cdf6-4578-9ca0-4c0fe5f56cef" />


<img width="431" height="799" alt="sudo aa-status" src="https://github.com/user-attachments/assets/46ecb814-12a7-4400-b946-47d2b84bab5a" />

AppArmor restricts applications using per-program security profiles, which prevents compromised processes from accessing files or performing actions outside their defined permissions. This significantly reduces the impact of zero-day vulnerabilities or misconfigurations.

## Configure Automatic Security Updates

Automatic security updates ensure the system receives patches without manual intervention.

### Install unattended-upgrades
```
sudo apt install unattended-upgrades
```

<img width="561" height="128" alt="sudo apt install unattended-upgrades" src="https://github.com/user-attachments/assets/c73f75c9-584d-4d19-b43f-1037b9c7514c" />


### Verify automatic upgrade configuration
```
cat /etc/apt/apt.conf.d/20auto-upgrades
```

<img width="493" height="55" alt="cat etcaptapt conf d20auto-upgrades" src="https://github.com/user-attachments/assets/72b357c4-1069-4660-89bc-29a1fb2d6517" />


The file confirmed:
- `APT::Periodic::Update-Package-Lists "1";`
- `APT::Periodic::Unattended-Upgrade "1";`

Enabling unattended upgrades ensures that critical security patches are applied automatically, reducing exposure time to known vulnerabilities and eliminating reliance on manual updates.

### Dry-run update test
```
sudo unattended-upgrade --dry-run --debug
```

<img width="1277" height="790" alt="sudo unattended-upgrade --dry-run --debug" src="https://github.com/user-attachments/assets/3cd0e3e7-a3fc-4143-9eda-bef79919ad48" />


## Fail2ban Intrusion Detection Setup

Fail2ban protects the server by banning IP addresses with repeated failed SSH login attempts.

### Installation
```
sudo apt install fail2ban
```

<img width="513" height="95" alt="sudo apt install fail2ban" src="https://github.com/user-attachments/assets/873d76ad-34a3-4446-8e2c-16de610cfc54" />


### Review Fail2ban jail configuration
```
cat /etc/fail2ban/jail.conf | head -n 30
```

<img width="689" height="513" alt="cat etcfail2banjail conf  head -n 30" src="https://github.com/user-attachments/assets/ee156f77-c8a2-420e-9b54-8d11648cbfb7" />

Fail2ban reduces the risk of brute-force attacks by dynamically banning IP addresses after repeated authentication failures. This adds an additional layer of protection beyond password policies and firewall rules.

### Check Fail2ban Status
```
sudo systemctl status fail2ban
```

<img width="1282" height="244" alt="sudo systemctl status fail2ban" src="https://github.com/user-attachments/assets/cf072925-cdd4-4441-9538-0c1a98b86875" />

Fail2ban service was active and the SSH jail was enabled.

## Security Baseline Verification Script (`security-baseline.sh`)

This script verifies all major security settings configured in Week 4 and Week 5.

### Script Contents

The baseline script demonstrates the ability to automate system audits, combining multiple checks into a single repeatable command, which is a core skill in system administration and security operations.

<img width="368" height="24" alt="nano security-baseline sh" src="https://github.com/user-attachments/assets/b6047776-8d64-4e17-970c-8c751b3c273b" />

<img width="860" height="555" alt="security base-line script" src="https://github.com/user-attachments/assets/0341f76d-e696-433c-8a7a-0a57cbc922f7" />

Key checks include:
- SSH configuration (Port, KeyAuth, DisableRootLogin, etc.)
- SSH service status  
- UFW firewall rules  
- Automatic updates  
- Fail2ban status  
- AppArmor profiles  

### Script Execution
```
./security-baseline.sh
```

<img width="561" height="787" alt="run security-baseline script" src="https://github.com/user-attachments/assets/727d9e13-83a7-4ae3-9a62-25bfb7cf10e5" />

All checks passed, confirming the system is securely configured.

## Remote Monitoring Script (`monitor-server.sh`)

This script collects live system performance metrics from the server via SSH and runs on the workstation.

Remote monitoring enables the workstation to collect server metrics without requiring console access, making it suitable for real-world scenarios such as headless servers or cloud deployments.
### Script Contents

<img width="736" height="640" alt="monitor-server script" src="https://github.com/user-attachments/assets/9ca9eaff-345b-46b9-b03c-87e000ce8344" />


### Metrics Collected
- CPU Usage  
- Memory Usage  
- Disk Usage  
- System Uptime  
- Load Average  

### Script Execution
```
./monitor-server.sh
```

<img width="671" height="468" alt="run monitor-server script" src="https://github.com/user-attachments/assets/011c8a73-c923-48cc-959e-e18e80b9c283" />

## Reflection
This week’s work helped deepen my understanding of Linux security modules. AppArmor required careful interpretation of loaded and enforced profiles, while Fail2ban needed verification of active jails and service status. Writing the baseline script reinforced my knowledge of all the configurations because it automated system auditing into a single tool. Overall, this week significantly improved my confidence in managing secure Linux environments.

---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
