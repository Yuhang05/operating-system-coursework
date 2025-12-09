[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---

# Initial System Configuration & Security Implementation – Week 4

## Introduction
This week focuses on deploying the Ubuntu Server securely and implementing foundational security controls.  
All administrative tasks were performed **remotely from the Xubuntu Workstation via SSH**, following the module requirement.

The tasks include:

- Secure SSH configuration with key-based authentication  
- Firewall restriction to allow SSH only from the workstation  
- Privilege management and user hardening  
- Configuration file documentation  
- Remote administration evidence  

---

## 1. Configure SSH with Key-Based Authentication

### 1.1 Generate SSH Key Pair on Workstation
I generated an ED25519 SSH key pair on the Xubuntu Workstation.

<img width="803" height="548" alt="Configure SSH key login" src="https://github.com/user-attachments/assets/3f9912e3-9d36-4b3d-8d4c-c8176c4d7621" />

### 1.2 Copy Public Key to Server
The public key was copied to the server using `ssh-copy-id`.

<img width="1176" height="199" alt="Copy the public key to the Server" src="https://github.com/user-attachments/assets/40d46276-11e6-420c-877a-c0df86b84b8e" />

### 1.3 Test Passwordless Login
A successful passwordless login confirms correct SSH key setup.

<img width="703" height="768" alt="Test passwordless login" src="https://github.com/user-attachments/assets/24aeb151-b3cb-4f81-ac07-18845d88e52e" />

---

## 2. Configure Firewall to Allow SSH ONLY from Workstation

### 2.1 Remove insecure "Allow Anywhere" SSH rules
Before locking down SSH, existing global allow rules were removed.

<img width="390" height="114" alt="delete all ports are anywhere" src="https://github.com/user-attachments/assets/fcc5bc05-952e-40a9-b5a6-f737238ce7b2" />

### 2.2 Allow SSH ONLY from workstation (192.168.56.104)
The workstation’s Host-Only IP is the only allowed SSH source.

<img width="805" height="40" alt="set only allows xubuntu workstation ip ssh " src="https://github.com/user-attachments/assets/4ea72e3a-50af-493d-91d6-458d82794fcd" />

### 2.3 Final Firewall Rule Verification
Only the workstation IP is allowed for SSH.

<img width="588" height="263" alt="check ufw status" src="https://github.com/user-attachments/assets/2de23f03-eb65-4da7-9376-28df2961f8d0" />

<img width="623" height="205" alt="only work station left in 22tcp" src="https://github.com/user-attachments/assets/04c8c28d-8f01-4e80-8c51-73736e442b11" />

---

## 3. User Privilege Management

### 3.1 Create Administrative User & Add to sudo Group
The non-root admin user (`adminuser`) was granted sudo privileges securely.

<img width="824" height="128" alt="Add adminuser to the sudo group" src="https://github.com/user-attachments/assets/d3445925-e913-442c-bbfd-576f4cb35258" />

---

## 4. SSH Configuration File Hardening

All modifications were made in:

### 4.1 Disable Root Login

<img width="239" height="29" alt="sshd_config permitrootlogin" src="https://github.com/user-attachments/assets/5a9a2004-308b-47c7-a50b-1f5aa1747b7b" />

### 4.2 Disable Password Authentication

<img width="275" height="27" alt="sshd_config password authur" src="https://github.com/user-attachments/assets/9812bea8-ff2b-4b73-9756-a26f6d0c0a3c" />

### 4.3 Enable Public Key Authentication

<img width="284" height="24" alt="sshd_config pubkey authur" src="https://github.com/user-attachments/assets/7121ac28-df3a-408f-94cf-e9a58e54955a" />

### 4.4 Restrict SSH to One User
Only `adminuser` is allowed to access SSH.

<img width="222" height="22" alt="sshd_config allowuser" src="https://github.com/user-attachments/assets/c63db999-c124-48fd-b985-89370b1c5b13" />

### 4.5 Validate Port Configuration

<img width="121" height="19" alt="sshd_config port number" src="https://github.com/user-attachments/assets/8b483e44-138e-439a-a708-940815d8e056" />

### 4.6 Full Configuration File Review
A combined review of key directives:

<img width="1202" height="239" alt="Modifying the SSH configuration file" src="https://github.com/user-attachments/assets/dfd72627-e8d9-4efe-b4ad-a3386d5ae0c4" />

---

## 5. Restart SSH Service and Confirm Status
After modifying configuration, SSH was restarted and status was checked.

<img width="888" height="434" alt="restart server and check status" src="https://github.com/user-attachments/assets/2b1330aa-2782-40ec-8aa4-7c6e81d0504e" />

---

## 6. SSH Access Evidence from Workstation

A clean and successful login from the workstation to the server.

<img width="881" height="717" alt="remote adminuser" src="https://github.com/user-attachments/assets/7a475bc6-02bc-4717-bfa0-133022cfb301" />

---

## 7. Security Validation Test: External Network Should Fail

SSH attempts from **outside the permitted workstation** were correctly blocked.

<img width="1049" height="287" alt="by other network ssh server time out" src="https://github.com/user-attachments/assets/b7523dc0-9fc2-4860-b200-494f62135f8f" />

---

## Summary
This week achieved a fully secured, remotely managed Ubuntu Server deployment. The implemented controls significantly reduce attack surface by enforcing:

- Key-based authentication  
- No root login  
- Limited user access  
- Strict firewall rules with IP whitelisting  
- Controlled SSH configuration with documented hardening

---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
