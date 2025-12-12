[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---

# Phase 7: Security Audit and System Evaluation (Week 7)

## Introduction
This week focused on conducting a comprehensive security audit and evaluating the overall system configuration of the Ubuntu Server. The audit aimed to identify potential security weaknesses, verify implemented security controls, and assess residual risks using industry-standard tools and best practices.

---

## Environment Overview
The audit was conducted from the Xubuntu Workstation using SSH-based remote administration. The target system was an Ubuntu Server configured with key-based SSH authentication, firewall restrictions, intrusion prevention mechanisms, and mandatory access control.

Screenshot evidence shows the initial SSH connection from the workstation to the server.

<img width="664" height="640" alt="week7_frist_ssh_to_server" src="https://github.com/user-attachments/assets/a3673faf-f4cd-43e6-8c8b-e9be8085f5c9" />

---

## Network Security Assessment (Nmap)

### Nmap Installation
Nmap was installed on the workstation to perform network-based security assessments.

<img width="779" height="135" alt="week7_installed_nmap" src="https://github.com/user-attachments/assets/949295f3-6283-4107-965a-98c0e00131d0" />

### TCP Connect Scan
A TCP connect scan was performed to identify accessible services using standard user privileges.

Command used:
`nmap -sT 192.168.56.103`

<img width="674" height="217" alt="week7_nmap_TCP-connect_scan" src="https://github.com/user-attachments/assets/e005cc75-981c-4a1b-acd7-d658e229c253" />

### TCP SYN Scan
A TCP SYN (half-open) scan was conducted using elevated privileges to obtain a more accurate view of exposed services.

Command used:
`sudo nmap -sS 192.168.56.103`

<img width="666" height="262" alt="week7_nmap_TCP-SYN_scan" src="https://github.com/user-attachments/assets/79abed47-8cc2-44f5-b9cc-3fcfe556506d" />

**Result:**  
Only expected ports (such as SSH) were accessible, confirming that the firewall configuration effectively limits network exposure.

---

## Access Control Verification

SSH hardening and firewall rules were reviewed to confirm secure remote access controls.  
The configuration enforces:
- Key-based authentication
- Disabled root login
- Firewall rules allowing SSH only from the workstation IP

<img width="1200" height="370" alt="week7_sshd_config_ufw_rule" src="https://github.com/user-attachments/assets/92a4beca-8d35-4de5-b81a-0abd9f89fa9a" />

This confirms that access control policies are correctly enforced.

---

## Service Audit and Justification

All running services on the server were reviewed to ensure that only necessary services are active.

<img width="788" height="560" alt="week7_running_service" src="https://github.com/user-attachments/assets/3aa60439-ddab-4ebf-aef9-ab4ff578aec0" />

**Service justification:**
- `sshd`: Required for secure remote administration
- `apache2`: Required for web service testing and performance evaluation
- `fail2ban`: Provides intrusion detection and SSH protection
- System services: Required for core operating system functionality

No unnecessary or unexpected services were identified.

---

## System Security Audit (Lynis)

### Lynis Installation
Lynis was installed to perform an in-depth system security audit.

<img width="1172" height="595" alt="week7_install_lynis" src="https://github.com/user-attachments/assets/eb1bafa6-2443-491c-9c4c-3bf85c886fbc" />

### Running Lynis Audit
A full system audit was executed using Lynis.

Command used:
`sudo lynis audit system`

<img width="816" height="395" alt="week7_run_lynis_audit_system" src="https://github.com/user-attachments/assets/5b952c5d-baec-44a7-833d-72efe90bc88a" />

### Lynis Scan Results
The audit produced security suggestions and hardening recommendations related to system configuration and service security.

<img width="785" height="722" alt="week7_part_of_lynis_scan" src="https://github.com/user-attachments/assets/e41b39c8-d846-4f2e-a1a8-c94cd4fc622a" />

<img width="809" height="717" alt="week7_finish_lynis_scan" src="https://github.com/user-attachments/assets/56eaed32-6842-4d22-94db-6575aafff564" />


**Outcome:**  
No critical vulnerabilities were detected. The system achieved a solid baseline security posture with minor recommendations for future hardening.

---

## System Update and Patch Status

The system was checked to ensure that all available security updates were applied.

<img width="703" height="194" alt="week7_check_for_update" src="https://github.com/user-attachments/assets/9f35d297-af7b-4245-a29e-3f39665a7547" />


This confirms that the server is maintained with current security patches.

---

## Residual Risk Assessment

Although the system is securely configured, the following residual risks remain:
- SSH remains exposed to the internal network (mitigated by firewall rules and key-based authentication)
- Web services could be targeted if misconfigured in the future
- Regular audits are required to maintain security posture

These risks are considered acceptable given the implemented controls.

---

## Summary

The Week 7 security audit verified that the server is securely configured and compliant with best practices. Network exposure is minimal, access controls are strictly enforced, and security monitoring mechanisms are active. The audit demonstrates a well-hardened system with clear documentation and justified service usage.



---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
