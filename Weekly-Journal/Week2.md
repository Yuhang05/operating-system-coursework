[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---
# System Administration and Secure Access Configuration – Week 2

## Introduction
This week focused on configuring secure remote access to the Ubuntu Server virtual machine and establishing proper system administration practices. I created a new administrative user, configured SSH key-based authentication, adjusted SSH daemon settings, and hardened the firewall using UFW. This ensures secure communication between the workstation and the server while following best security practices.

## Creating an Administrative User
To avoid using the root account and improve system security, I created a new user with administrative privileges.

<img width="1275" height="335" alt="Create  a new user" src="https://github.com/user-attachments/assets/a462e88d-4c82-41c4-a7aa-08914ff35ea4" />

After creating the user, I added it to the sudo group to grant administrative rights.

<img width="1279" height="97" alt="Adding admin to sudo" src="https://github.com/user-attachments/assets/d6e18e80-d2f9-496d-8889-a483745d7b68" />

---

## Updating the Server
Before making changes, I updated the server packages to ensure the system is running the latest security patches.

<img width="1273" height="259" alt="Update Server" src="https://github.com/user-attachments/assets/3ab2bdef-2e59-4e85-aff1-d2911422a3b5" />

---

## Generating SSH Key Pair
On the workstation, I generated an SSH key pair to enable secure and password-less login to the server.

<img width="1206" height="531" alt="Generate SSH key" src="https://github.com/user-attachments/assets/a828dd21-4e98-45a0-b77a-5f95f39e0b46" />

Then, I copied the public key to the server.

<img width="1203" height="238" alt="Public key successfully copied" src="https://github.com/user-attachments/assets/418a7fd2-1f55-4a1d-809a-fb2a5fddd8fe" />

---

## SSH Daemon Configuration
To enforce key-based authentication and improve security, I modified the SSH daemon configuration file (`/etc/ssh/sshd_config`).

### SSH Config Screenshot 1  
<img width="388" height="26" alt="sshd_config 1" src="https://github.com/user-attachments/assets/ce2fa869-1b96-422b-a9d0-a49b48055c80" />

### SSH Config Screenshot 2  
<img width="447" height="20" alt="sshd_config 2" src="https://github.com/user-attachments/assets/d39143f3-ffa9-4476-bc65-2d11a4985ff3" />

### SSH Config Screenshot 3  
<img width="470" height="18" alt="sshd_config 3" src="https://github.com/user-attachments/assets/a792634a-c4b8-4a6b-999c-8be7418c83c1" />

### SSH Config Screenshot 4  
<img width="479" height="25" alt="sshd_config 4" src="https://github.com/user-attachments/assets/6da44bc8-37cc-455e-9745-ece4e7055427" />

After modifying the SSH configuration, I disabled password authentication to ensure only key-based login is allowed.

<img width="1269" height="800" alt="none-password login" src="https://github.com/user-attachments/assets/f65695c0-5fa1-4b58-a8a1-32b38d06012b" />

---

## Firewall Configuration with UFW
To control incoming connections, I enabled and configured UFW on the server. SSH port 22 was allowed and unnecessary ports were denied.

<img width="531" height="322" alt="Firewall Configure UFW" src="https://github.com/user-attachments/assets/cacf87fc-abdd-4f84-b2ca-d09fba4c8dcd" />

---

## Testing SSH Login
Finally, I verified that SSH login works using the newly created admin user and key-based authentication.

<img width="1201" height="771" alt="Test Login " src="https://github.com/user-attachments/assets/ad32a414-d49d-4e1f-9917-c1e6bcb5570b" />

---

## Reflection
During this week, I encountered several challenges, especially with SSH key-based authentication. At first, I was repeatedly unable to connect, receiving timeout errors and “address already in use” issues when testing with `iperf3`. I also struggled with SSH configuration lines such as enabling and disabling `PasswordAuthentication` and properly restarting the SSH service. Additionally, I learned about managing multiple network adapters in VirtualBox and ensuring the correct interface was being used for communication. By troubleshooting with commands like `lsof`, `ufw status`, and checking host-only adapter IP ranges, I gained a much deeper understanding of Linux remote access, virtual networking, and system administration.  

---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
