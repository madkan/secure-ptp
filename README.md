# Securing Precision Time Protocol (PTP)
## ECE635 Project

## Team Members

- Madhurya Kandamuru
- Adithi Viswanath
- Arya Parameshwara

## Motivation

Precision Time Protocol (PTP) is a network protocol that synchronizes clocks across a network with high precision, supporting sub-microsecond accuracy with suitable hardware and network conditions. This precision is essential for safety-critical control applications, where security is a priority.

PTP relies on timestamp acquisition, network drivers, clock adjustment, and scheduling. These components can be manipulated by a compromised operating system, undermining the integrity of time synchronization. This security gap motivates our project. We aim to study, explore, and implement trusted execution environment (TEE) mechanisms to make selected PTP operations more secure.

## Design Goals

Develop and evaluate a prototype for securing selected Precision Time Protocol (PTP) operations on an embedded Linux platform using OP-TEE.

1. Establish PTP synchronization between two Ethernet-connected devices and characterize network delay, clock offset, and relative clock drift.
2. Define a threat model covering selected malicious operating-system actions, including timestamp manipulation, unauthorized clock adjustments, and replay of timing data.
3. Implement an OP-TEE-based protection mechanism for selected timing operations, with clearly documented trusted components and timestamp-source assumptions.
4. Evaluate the baseline and protected implementations under normal operation and controlled attacks.
5. Quantify synchronization error, attack detection or rejection, and the execution overhead introduced by the protection mechanism.

## Deliverables

1. A reproducible two-endpoint PTP testbed, including hardware connections, software versions, and setup instructions.
2. A baseline PTP implementation and measurements of estimated network delay, clock offset, and relative clock drift.
3. A documented threat model and reproducible experiments demonstrating selected timing attacks.
4. An OP-TEE trusted application and associated Linux application implementing the selected protection mechanism.
5. Comparative results for baseline and protected operation, including synchronization error, attack detection or rejection, and performance overhead.
6. Source code, configuration files, experiment scripts, and measurement logs.
7. A final report and demonstration explaining the architecture, results, limitations, and possible extensions.

## System Blocks

| Component | Function |
| --- | --- |
| **PTP Master** | Generates and transmits synchronization messages to the slave device. |
| **PTP Slave** | Receives timing messages and adjusts its local clock to synchronize with the master. |
| **Ethernet Interface** | Provides communication between endpoints and supports timestamp acquisition. |
| **Linux PTP Software** | Runs PTP services, handles network communication, and manages clock synchronization. |
| **OP-TEE Trusted Application** | Performs selected security-sensitive operations, such as message validation, replay detection, and authorization checks for clock adjustments. |
| **Linux–TEE Interface** | Uses the OP-TEE Client API to communicate between the normal-world application and the trusted application. |
| **Attack Simulation Module** | Introduces controlled timestamp manipulation, unauthorized clock adjustments, and replay attacks. |
| **Monitoring and Logging** | Records clock offset, path delay, drift, attack outcomes, and execution overhead. |

## Hardware Requirements

| Hardware | Purpose |
| --- | --- |
| **Raspberry Pi** | Initial platform for understanding PTP, collecting baseline measurements, and implementing attacks. |
| **STM32 Development Board** | Planned platform for OP-TEE experiments. |
| **Laptop with Linux** | Development, reference-clock operation, experiment orchestration, and results analysis. |
| **Ethernet Cable** | Wired connection between the laptop and embedded device. |

## Software Requirements

| Software | Purpose |
| --- | --- |
| **Linux / Raspberry Pi OS** | Environment for initial synchronization and attack experiments. |
| **OpenSTLinux / OP-TEE** | Linux and trusted execution environment for the STM implementation. |
| **LinuxPTP** | PTP synchronization. |
| **C/C++ and ARM Build Tools** | Development of attacks, the Linux client, and the trusted application. |
| **Python** | Experiment automation, data analysis, and results visualization. |
| **Wireshark / tcpdump** | Inspection and capture of PTP traffic. |
| **Git** | Source code version control and documentation. |

## Team Members and Responsibilities

### Member 1 — Setup and Networking

- Set up and configure the Raspberry Pi and STM boards and establish PTP synchronization.
- Collect packet captures and maintain a reproducible experimental setup.

### Member 2 — Software and Algorithm Design

- Implement timing attacks and develop the OP-TEE-based protected timing implementation.
- Design and implement algorithms for checking timing consistency and detecting selected attacks.

### Member 3 — Research and Security Evaluation

- Study the reference papers and define attack scenarios and evaluation metrics.
- Develop experiment automation and analysis scripts to compare timing accuracy and attack detection.

We will adjust responsibilities as the project progresses to ensure the workload is shared as equitably as possible.

## Project Timeline

| Milestone | Timeline | Planned Work |
| --- | --- | --- |
| **Initial Project Proposal** | Week 4 | Define project motivation, objectives, high-level system architecture, hardware/software requirements, and team responsibilities. |
| **Midterm Review** | Week 8 | Set up Raspberry Pi, conduct initial PTP experiments, and collect logs to estimate network delay, clock offset, and relative clock drift. |
| **Final Review** | Week 13 | Obtain an STM32 development board with OP-TEE support, implement a protected timing service, repeat selected attacks, compare results with the unprotected implementation, and present findings. |

## References

[1] A. Nasrullah and F. M. Anwar, “Trusted Timing Services with TimeGuard,” in *IEEE Real-Time and Embedded Technology and Applications Symposium (RTAS)*, 2024.

[2] F. M. Anwar, L. Garcia, X. Han, and M. Srivastava, “Securing Time in Untrusted Operating Systems with TimeSeal,” in *IEEE Real-Time Systems Symposium (RTSS)*, 2019.

[3] A. Nasrullah, M. A. Soomro, and F. M. Anwar, “SeTi: Secure Time for Virtualized Systems,” in *Annual Computer Security Applications Conference (ACSAC)*, 2025.

[4] A. Finkenzeller, O. Butowski, E. Regnath, M. Hamad, and S. Steinhorst, “PTPsec: Securing the Precision Time Protocol Against Time Delay Attacks Using Cyclic Path Asymmetry Analysis,” in *IEEE INFOCOM*, 2024.