[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---

# Application Selection for Performance Testing – Week 3

## Introduction
This week focused on identifying and preparing suitable applications to generate different types of system workloads for performance benchmarking. The goal was to choose a representative tool for each major subsystem—CPU, RAM, Disk I/O, Network, and Server workload—and document their installation, expected behaviour, and monitoring strategy. These workloads will be used for detailed testing in Week 4.

## Application Selection Matrix

The following matrix shows the selected tools and the justification for each type of performance workload.

| Workload Type | Selected Tool | Justification |
|---------------|---------------|----------------|
| **CPU-intensive** | sysbench (CPU test) | Widely used benchmarking tool that stresses CPU cores using prime number calculations. Simple to automate and reliably produces high CPU load. |
| **RAM-intensive** | stress-ng (vm/stressors) | Capable of allocating and stressing memory in controlled blocks. Provides realistic RAM pressure and memory exhaustion scenarios. |
| **Disk I/O-intensive** | sysbench file I/O / dd | Allows sequential and random file operations, suitable for measuring disk throughput and latency. |
| **Network-intensive** | iperf3 | Industry-standard bandwidth testing tool capable of generating large TCP/UDP streams between VMs. |
| **Server workload** | Apache2 Web Server | Represents real-world HTTP workloads, enabling evaluation of combined CPU, memory, and network usage. |

## Installation Documentation (SSH-Based)

All applications were installed on the Ubuntu Server from the Xubuntu Workstation using SSH.  
Screenshots from each installation step are included below.


### Updating the Server
Before installing any applications, the server was updated:

<img width="1273" height="259" alt="Update Server" src="https://github.com/user-attachments/assets/33b984cb-293b-4d33-9a3b-c08d3e6e294d" />

### Installing sysbench (CPU Workload)

<img width="507" height="113" alt="Install CPU workload" src="https://github.com/user-attachments/assets/c91be554-bd7d-4260-a639-250e43a0a639" />

## Installing Memory Workload Tool (stress-ng)

<img width="532" height="128" alt="Install memory workload" src="https://github.com/user-attachments/assets/0df76508-fe9f-411b-a980-466d2a2f9f03" />

## Installing Network Load Tool (iperf3)

<img width="667" height="171" alt="Install networkload-iperf3" src="https://github.com/user-attachments/assets/9cb12d69-cb53-472e-bc36-60474f97914c" />

## Installing Web Server Workload Tool (Apache2)

<img width="511" height="123" alt="Install web server workload" src="https://github.com/user-attachments/assets/9c585b34-feb0-4ee0-9191-c6507ba00cc5" />

# Workload Execution

Below are the results of running each workload on the Ubuntu Server.  
**All screenshots were taken through the SSH terminal from the workstation**, to proving remote management.

## CPU Performance Test (sysbench CPU)

<img width="504" height="532" alt="Testing sysbench CPU" src="https://github.com/user-attachments/assets/be3cba1f-1949-4ef1-90ec-6428dc780986" />

## Memory Performance Test (stress-ng)

Example memory workload (1GB RAM stress):

<img width="563" height="145" alt="Testing memory workload" src="https://github.com/user-attachments/assets/71cfe28c-3092-4bc4-986a-03cf2061c7b3" />

## Disk I/O Performance Test (sysbench / dd)

Example command:

<img width="609" height="91" alt="Testing disk I O workload" src="https://github.com/user-attachments/assets/0f56c440-b09f-42db-89f8-d994a1446084" />

## Network Throughput Test (iperf3)

### Start iperf3 on Server in Listener Mode

<img width="636" height="363" alt="Server listening on 5201" src="https://github.com/user-attachments/assets/d44922f2-a504-44a8-8b37-2c4f690efe8b" />

### Run iperf3 Client from Workstation

<img width="798" height="442" alt="Accepted connection form 192 168 56 104" src="https://github.com/user-attachments/assets/e440e3ba-33ac-4cf5-bbe6-06698fd54dbb" />

## Apache Web Server Test

To validate the server workload:

Workstation accessed the server via browser.

<img width="709" height="228" alt="Testing web server -apache2" src="https://github.com/user-attachments/assets/f24131d8-86dc-4816-b0cc-21916638c8a9" />

# Expected Resource Profiles

| Application | CPU Usage | Memory Usage | Disk I/O | Network Usage | Description |
|-------------|-----------|--------------|----------|----------------|-------------|
| **sysbench CPU** | Very High | Low | None | None | Maxes out CPU cores using prime calculations. |
| **stress-ng memory** | Low | Very High | None | None | Allocates large blocks of RAM and stresses memory subsystem. |
| **dd / sysbench I/O** | Low–Medium | Low | Very High | None | Generates sequential disk writes, stressing disk throughput. |
| **iperf3** | Low | Low | None | Very High | Used to saturate available network bandwidth. |
| **Apache2** | Medium | Medium | Low–Medium | Medium | Real-world HTTP server workload. |

# Monitoring Strategy

The monitoring plan included system-level tools to observe performance impact during testing:

### CPU Monitoring
- `top` / `htop` – per-process CPU usage  
- `mpstat` – per-core utilization  

### Memory Monitoring
- `free -h` – total vs used RAM  
- `vmstat` – memory pressure and swapping  

### Disk Monitoring
- `iostat -x` – throughput and latency  
- `df -h` – disk usage before/after workload  

### Network Monitoring
- `ss -tuna` – active TCP/UDP sessions  
- `iperf3` client output – bandwidth and retransmissions  

### Web Server Monitoring
- `systemctl status apache2`  
- `journalctl -u apache2` – web access logs  

---

# Summary
This week successfully prepared all required workload applications for performance testing. All tools were installed via SSH, executed to verify functionality, and documented with screenshots. Expected resource profiles and monitoring procedures were also established, ensuring Week 4 testing can be carried out consistently and accurately.

---

# Reflection
During Week 3, I encountered several challenges, especially with iperf3 network testing. The workstation initially failed to connect because the server listener was running on the wrong session. After understanding how host-only networking works in VirtualBox and ensuring the correct process was active, the network test succeeded. This week greatly improved my understanding of workload generation, Linux monitoring commands, and how different subsystems respond to stress.

---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
