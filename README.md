[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: LUO Liwen
### Student Id: 21072501
### Email: lluoas@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).
    > Name of measurement tool: Phoronix Test Suite  
    >
    > (1) CPU Performance
    > | Aspect | Details |
    > | ---- | ---- |
    > | Test Selection | pts/compress - 7zip |
    > | Parameter and Explanation | Compression Rating. A higher compression rating implies that the CPU can perform compression tasks more rapidly and efficiently, which is directly related to its processing power and algorithm - handling capabilities. |
    > | Values Obtained from Result | Measured in MIPS (Million Instructions Per Second). It represents the number of millions of instructions that a CPU can execute per second, with a higher value indicating a faster processing speed. |
    > 
    > (2) Memory Performance
    > | Aspect | Details |
    > | ---- | ---- |
    > | Test Selection | pts/ramspeed |
    > | Parameter and Explanation | - Copy: Measures the speed at which data can be copied within the memory, a key metric for evaluating the memory's bandwidth.<br>- Integer: Focuses on the performance of integer - based operations in the memory, such as arithmetic calculations and data storage, reflecting the memory's ability to handle basic data processing. |
    > | Values Obtained from Result | Measured in MB/s (Megabytes Per Second). This metric shows how fast data can be read from or written to the memory, with a higher value indicating a faster data transfer rate. |

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | 3620 MIPS        | 11060.17 MB/s      |
    | `t2.medium`  |  10243 MIPS    | 20445.89 MB/s      
    | `c5d.large` |  7374 MIPS      | 13368.96 MB/s      |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    |  | vCPU | RAM (GiB) |
    | ---- | ---- | ---- |
    | t2.micro | 1 | 1 |
    | t2.medium | 2 | 4 |
    | c5d.large | 2 | 4 |  

    From t2.micro to t2.medium or from t2.micro to c5d.large, the performance is significantly improved by increasing vCPUs and RAM. This shows that when resources are insufficient, increasing resources can effectively improve the performance of EC2 instances.

    However, from t2.medium to c5d.large, vCPUs and RAM remain unchanged, the performance is reduced. This may be because c5d.large uses a different processor architecture or instance type optimization strategy, resulting in inferior performance under the same resources than t2.medium. In addition, memory bandwidth or other system-level factors may also affect performance.

    In this experiment, the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource, but the performance also depends on other factors, so it's hard to say whether the performance always increase as the number of vCPUs and memory resources increase.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) ping|
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |  4210 |0.178     |
    | `m5.large` - `m5.large`   |  4960 |   0.144  |
    | `c5n.large` - `c5n.large` |  4960 |  0.159   |
    | `t3.medium` - `c5n.large` |  2490 |  0.653   |
    | `m5.large` - `c5n.large`  |  2860 |   0.550  |
    | `m5.large` - `t3.medium`  |  4400 |    0.246 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

    In the same region, network performance between EC2 instances is better under the same instance type, while network performance between different instance types may decrease TCP bandwidth and increase RTT due to differences in hardware or network configuration.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 33.8  |  64.358  |
    | N. Virginia - N. Virginia | 4500  |   0.297  |
    | Oregon - Oregon           | 4620  | 0.174    |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

    The network performance of EC2 instances within the same region is better than that between different regions.