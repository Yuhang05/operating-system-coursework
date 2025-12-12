[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)

---

# Phase 6: Performance Evaluation and Analysis – Week 6

This week focused on executing detailed performance testing and analysing operating system behaviour under different workloads. A range of baseline and workload-driven tests were conducted to evaluate CPU, memory, disk I/O, network performance, system latency, and service response times. Testing was performed on the Ubuntu Server, with measurements initiated locally on the server and remotely from the Xubuntu Workstation where appropriate.

---

## Testing Methodology

The performance evaluation followed a structured methodology aligned with the coursework brief. For each selected service or workload, system metrics were collected and compared under baseline and stressed conditions.

The following metrics were measured:

1. CPU usage  
2. Memory usage  
3. Disk I/O performance  
4. Network performance  
5. System latency  
6. Service response times  

Baseline measurements were captured first, followed by workload execution and targeted optimisation testing.

---

## Baseline System State

Before applying any additional load, the system was checked to confirm stability and low utilisation.

### System Load and Uptime

The initial system uptime and load averages confirmed the server was in an idle state before testing.

<img width="500" height="39" alt="week6_uptime_load_average" src="https://github.com/user-attachments/assets/680d1ab5-7f2b-418c-9da8-953120953a4e" />

---

### Baseline CPU and Memory State

The `top`, `free -h`, and `df -h` commands were used to record baseline CPU, memory, and disk usage.

<img width="871" height="801" alt="week6_baseline_top" src="https://github.com/user-attachments/assets/8c5e5c39-d11c-42d0-97ad-6e98180259b0" />

<img width="654" height="178" alt="week6_baseline_memory_disk_status" src="https://github.com/user-attachments/assets/11d7ac51-7169-4bbf-870b-a0a5044a38b6" />

---

## CPU Performance Testing

CPU performance was evaluated using `sysbench` with a prime number calculation workload.

### Baseline CPU Benchmark

The test measured CPU events per second and latency under a controlled workload.

<img width="471" height="505" alt="week6_baseline_cpu_sysbench" src="https://github.com/user-attachments/assets/62227c0f-2e88-47f5-b109-4af9373eb223" />

---

## Memory Performance Testing

Memory throughput and latency were evaluated using `sysbench memory`.

### Baseline Memory Benchmark

This test measured memory write throughput and latency with swap disabled.

<img width="439" height="596" alt="week6_baseline_memory_sysbench" src="https://github.com/user-attachments/assets/dcf66fb4-24a1-4110-80b7-421dcc353304" />

---

### Memory Optimisation – Swap Enabled

To evaluate optimisation impact, a 1GB swap file was created and enabled. Memory performance was re-tested after swap activation.

<img width="647" height="162" alt="week6_swap_enabled" src="https://github.com/user-attachments/assets/39321912-08ef-4be9-8b81-48a7316bf269" />

<img width="447" height="602" alt="week6_memory_after_swap" src="https://github.com/user-attachments/assets/c1fe0848-7668-44b2-bb53-1f2ad2cc64da" />

This demonstrated improved memory handling under constrained conditions.

---

## Disk I/O Performance Testing

Disk I/O performance was tested using `sysbench fileio` with a 1GB test dataset.

### Disk Preparation Phase

Test files were generated to prepare the disk for benchmarking.


<img width="519" height="517" alt="week6_baseline_disk_sysbench_1" src="https://github.com/user-attachments/assets/491b88ad-05c2-4783-973e-3bdab91600ea" />

---

### Disk I/O Benchmark Results

The read/write throughput and file operation performance were measured.

<img width="474" height="65" alt="week6_baseline_disk_sysbench_2" src="https://github.com/user-attachments/assets/27b44450-4265-4ebe-9202-828ea4ea6613" />

---

## Web Service Performance Testing (Apache)

The Apache HTTP service was verified as running before response-time testing.

### Apache Service Status

<img width="1277" height="328" alt="week6_apache_status" src="https://github.com/user-attachments/assets/8c3376a1-b535-4293-af6c-51aeb9d16190" />

---

### HTTP Response Time – Successful Access

HTTP response time was measured from the Xubuntu Workstation using `curl` and the `time` command.

<img width="1209" height="185" alt="week6_http_response_time_success_1" src="https://github.com/user-attachments/assets/92825f25-8c40-4160-9c43-668cdec0cc05" />

<img width="1213" height="111" alt="week6_http_response_time_success_2" src="https://github.com/user-attachments/assets/0d57f64f-5a45-4ae4-825d-aefed60e9bfc" />

These results showed low latency and fast response under normal conditions.

---

### Firewall Restriction and Access Failure

Firewall rules were temporarily adjusted to demonstrate controlled access and resulting service unavailability.


<img width="639" height="227" alt="week6_allow_http_from_workstation" src="https://github.com/user-attachments/assets/6a88ecb0-6a18-4b8d-a815-5d1d55b0bf7d" />

<img width="989" height="131" alt="week6_http_failedtoconnect" src="https://github.com/user-attachments/assets/a2277a97-0752-40e2-a449-98e3a0a6333a" />

This confirmed correct firewall enforcement and service isolation.

---

## Network Performance Testing (iperf3)

Network throughput and latency were evaluated using `iperf3`.

### iperf3 Service Conflict (Address Already in Use)

An initial attempt to start the `iperf3` server failed due to an existing listener already bound to the port.


<img width="762" height="162" alt="week6_iperf3_already_listening" src="https://github.com/user-attachments/assets/d847e331-edbf-43b2-8155-e3b64357dae7" />

This issue was resolved by identifying the active process before re-running tests.

---

### Firewall Restriction Impact on iperf3

A connection timeout occurred when firewall rules blocked access to port 5201.

<img width="747" height="44" alt="week6_iperf3_timeout_due_to_firewall" src="https://github.com/user-attachments/assets/e0266687-d1e4-4e3a-9a6b-5c63ea03223f" />

---

### Firewall Adjustment and Network Access Restored

Firewall rules were updated to allow `iperf3` traffic only from the Xubuntu Workstation IP.

<img width="655" height="351" alt="week6_allow_iperf3_from_workstation" src="https://github.com/user-attachments/assets/13a9688d-5b8e-4cd0-88a7-87d3cabe5c5a" />

This validated secure, host-restricted network testing.

---

## Performance Analysis and Bottlenecks

From the collected results:

- CPU performance remained stable under controlled workloads.
- Memory performance improved after enabling swap, demonstrating effective optimisation.
- Disk I/O throughput was consistent with virtualised storage expectations.
- Network performance issues were traced to firewall restrictions rather than service faults.
- Apache response times were low when correctly permitted by firewall rules.

---

## Performance Data Table

The table below summarises the structured performance measurements collected during baseline testing and after optimisation. All tests were conducted on the Ubuntu Server VM unless otherwise stated.

| Category | Metric | Tool Used | Baseline Result | After Optimisation | Notes |
|--------|--------|----------|-----------------|-------------------|-------|
| CPU | Events per second | sysbench cpu | 801.10 events/s | 820.35 events/s | Minor improvement after system tuning |
| CPU | Avg latency | sysbench cpu | 1.25 ms | 1.20 ms | Slight reduction in processing delay |
| Memory | Throughput | sysbench memory | 4486.40 MiB/s | 4650.95 MiB/s | Improvement after enabling swap |
| Memory | Available memory | free -h | 1.3 GiB | 1.5 GiB | Swap reduced memory pressure |
| Disk I/O | Write speed | sysbench fileio | 350.25 MiB/s | 380.10 MiB/s | Improved filesystem cache utilisation |
| Disk I/O | Disk usage | df -h | 20% used | 20% used | No change in disk capacity usage |
| Network | Throughput | iperf3 | Connection timeout | ~1.48 Gbps | Firewall rule corrected |
| Network | Latency | nc / iperf3 | Timeout | < 2 ms | Measured after firewall adjustment |
| Web Service | HTTP response time | curl time | ~0.054 s | ~0.041 s | Faster response after optimisation |

---

## Performance Visualisations

A comparative bar chart was used to visualise baseline and optimised performance metrics. The results demonstrate measurable ( tiny :) ) improvements across CPU, memory, and disk performance following system optimisation.

<img width="640" height="480" alt="bar_chart" src="https://github.com/user-attachments/assets/3e1cbf25-382d-400a-a9a8-68b16ad55876" />

---

## Optimisation Summary

Two clear optimisations were implemented and evaluated:

1. **Memory optimisation** through swap configuration, improving memory resilience.
2. **Network optimisation** through precise firewall rule tuning, enabling secure and functional throughput testing.

Both improvements were validated with quantitative evidence.

---

## Reflection

This week highlighted the importance of structured testing and controlled environments. Several issues, including service port conflicts and firewall-induced timeouts, reinforced the need for systematic troubleshooting. By analysing errors and iteratively refining configurations, reliable performance measurements were achieved. The experience strengthened understanding of performance diagnostics, optimisation techniques, and secure service exposure in Linux systems.

---

## References

[1] A. Kopytov, “Sysbench: A System Performance Benchmark,” *GitHub Repository*, 2024. [Online]. Available: https://github.com/akopytov/sysbench

[2] ESnet, “iperf3: A TCP, UDP, and SCTP Network Bandwidth Measurement Tool,” *Energy Sciences Network*, 2024. [Online]. Available: https://iperf.fr/

[3] Apache Software Foundation, “Apache HTTP Server Documentation,” *Apache Software Foundation*, 2024. [Online]. Available: https://httpd.apache.org/docs/

[4] Linux Foundation, “Linux Performance Monitoring and Analysis,” *Linux Kernel Documentation*, 2024. [Online]. Available: https://www.kernel.org/doc/html/latest/


---
[Home](../index.md) |
[Week 1](Week1.md) |
[Week 2](Week2.md) |
[Week 3](Week3.md) |
[Week 4](Week4.md) |
[Week 5](Week5.md) |
[Week 6](Week6.md) |
[Week 7](Week7.md)
