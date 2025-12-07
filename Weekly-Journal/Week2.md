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

## Performance Testing Plan – Remote Monitoring & Testing Approach [1]
This performance testing plan outlines how remote monitoring and network performance measurements were conducted between the Ubuntu Server and Xubuntu Workstation. The goal is to validate connectivity, measure throughput, and ensure the system performs reliably under typical operational conditions.

### Remote Monitoring Methodology

1. **Remote SSH Administration**  
   The workstation connects to the server using SSH. This allows running commands, viewing logs, and monitoring system performance without needing to use the VirtualBox console directly.

2. **System Resource Monitoring**  
   Tools such as `top`, `vmstat`, and `iostat` are used to observe CPU load, memory consumption, and disk activity during tests.

3. **Network Monitoring**  
   Commands such as `ss`, `netstat`, and `ip -s link` help check active connections and network statistics while the performance tests are running.

4. **Log Inspection**  
   Logs such as `/var/log/auth.log` and `/var/log/syslog` are reviewed to confirm secure access and detect any abnormal activity during performance testing.

### Performance Testing Approach

1. **Connectivity Test (ping)**  
   `ping <server-ip>` is used to verify stable ICMP connectivity between the workstation and server over the host-only network.

2. **Port Availability Check (nc / netcat)**  
   `nc -vz <server-ip> 5201` confirms that the iperf3 service is reachable before running bandwidth tests.

3. **Network Throughput Testing (iperf3)**  
   Run `iperf3 -s` on the server.  
   Run `iperf3 -c <server-ip>` on the workstation.  
   This measures upload bandwidth and verifies stable data transfer between both machines.

4. **Result Interpretation**  
   Test results such as bitrate, total transferred data, and retransmissions are reviewed to ensure stable performance. These results can be correlated with CPU and memory usage observed through monitoring tools.


## Creating an Administrative User
To avoid using the root account and improve system security, I created a new user with administrative privileges.

<img width="1275" height="335" alt="Create  a new user" src="https://github.com/user-attachments/assets/a462e88d-4c82-41c4-a7aa-08914ff35ea4" />

After creating the user, I added it to the sudo group to grant administrative rights.

<img width="1279" height="97" alt="Adding admin to sudo" src="https://github.com/user-attachments/assets/d6e18e80-d2f9-496d-8889-a483745d7b68" />


## Updating the Server
Before making changes, I updated the server packages to ensure the system is running the latest security patches.

<img width="1273" height="259" alt="Update Server" src="https://github.com/user-attachments/assets/3ab2bdef-2e59-4e85-aff1-d2911422a3b5" />


## Generating SSH Key Pair
On the workstation, I generated an SSH key pair to enable secure and password-less login to the server.

<img width="1206" height="531" alt="Generate SSH key" src="https://github.com/user-attachments/assets/a828dd21-4e98-45a0-b77a-5f95f39e0b46" />

Then, I copied the public key to the server.

<img width="1203" height="238" alt="Public key successfully copied" src="https://github.com/user-attachments/assets/418a7fd2-1f55-4a1d-809a-fb2a5fddd8fe" />

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


## Firewall Configuration with UFW
To control incoming connections, I enabled and configured UFW on the server. SSH port 22 was allowed and unnecessary ports were denied.

<img width="531" height="322" alt="Firewall Configure UFW" src="https://github.com/user-attachments/assets/cacf87fc-abdd-4f84-b2ca-d09fba4c8dcd" />


## Testing SSH Login
Finally, I verified that SSH login works using the newly created admin user and key-based authentication.

<img width="1201" height="771" alt="Test Login " src="https://github.com/user-attachments/assets/ad32a414-d49d-4e1f-9917-c1e6bcb5570b" />

## Security Configuration Checklist

| Security Feature | Status | Evidence |
|------------------|--------|----------|
| New admin user created | ✔ | User creation screenshot |
| User added to sudo group | ✔ | sudo group screenshot |
| SSH root login disabled | ✔ | sshd_config |
| SSH key-based login enabled | ✔ | key generation + login screenshot |
| Password login disabled | ✔ | sshd_config |
| Firewall enabled | ✔ | UFW screenshot |
| Only port 22 allowed | ✔ | UFW screenshot |
| System updated | ✔ | update screenshot |

- The workstation stores the private key locally.  
- The server receives only the public key.  
- Even if someone learns the username, they cannot log in without the private key.  
- This is significantly more secure than password-based authentication.  

## Threat Model – Security Risks and Mitigation Strategies [2]

| Threat | Description | Impact | Mitigation Strategy |
|--------|-------------|--------|----------------------|
| Unauthorized SSH access | Attackers may attempt brute-force SSH login or exploit weak credentials. | System compromise and possible privilege escalation. | Disable root login, restrict login to a dedicated admin user, use SSH key authentication instead of passwords. |
| Firewall misconfiguration | Unnecessary open ports expose additional services to network attacks. | Increased attack surface, potential exploitation of exposed services. | Enable UFW, block all non-essential ports, and allow only required ones such as SSH (port 22). |
| Outdated system packages | Old software may contain unpatched vulnerabilities listed in public CVE databases. | Exploitation leading to system takeover or data leakage. | Apply regular updates (`apt update && apt upgrade`) and ensure security patches are installed promptly. |


## Reflection
During this week, I encountered several challenges, especially with SSH key-based authentication. At first, I was repeatedly unable to connect, receiving timeout errors and “address already in use” issues when testing with `iperf3`. I also struggled with SSH configuration lines such as enabling and disabling `PasswordAuthentication` and properly restarting the SSH service. Additionally, I learned about managing multiple network adapters in VirtualBox and ensuring the correct interface was being used for communication. By troubleshooting with commands like `lsof`, `ufw status`, and checking host-only adapter IP ranges, I gained a much deeper understanding of Linux remote access, virtual networking, and system administration.  

 ## Reference
[1] V. B. P. Pawar and S. A. Kasbe, “Performance and Information Security Evaluation with Firewalls,” ResearchGate, 2025. [Online]. Available: https://www.researchgate.net/publication/262157151_Performance_and_Information_Security_Evaluation_with_Firewalls [Accessed: Nov. 22, 2025]

[2] S. H. Ansar, M. Umar, and M. A. Shami, “Fortifying Linux Server and Implementing a Zero Trust Architecture,” MDPI, vol. 10, no. 7, pp. 1–12, 2025. [Online]. Available: https://www.mdpi.com/2673-4591/107/1/99 [Accessed: Nov. 22, 2025]

---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
