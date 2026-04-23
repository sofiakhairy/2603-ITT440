# Parallelized Network Service Auditor and Vulnerability Scoring Engine

**Name:** Sofia Hani Binti Khairy Shamel

**Student ID:** 2024443178

**Group:** M3CDCS2554B

<br>

## 1. Introduction
Network auditing is a critical cybersecurity component for identifying vulnerabilities, yet traditional sequential discovery becomes a significant bottleneck at massive scales (millions of data points). This project presents a high-performance auditing application designed to evaluate three distinct execution paradigms—Sequential, Concurrent, and Parallel. By testing these paradigms against a 2,000,000-task workload, this project provides empirical data on architectural efficiency and scalability in forensic security discovery.

<br>

## 2. Problem Statement

<br>

## 3. Objectives 🎯
* Implement Multi-Paradigm Auditing: Develop a unified engine capable of executing Sequential, Concurrent, and Parallel workloads.
* Scalability Engineering: Utilize batch-processing to handle 2,000,000 data points without exceeding system memory limits.
* Architectural Analysis: Quantify the performance trade-offs between I/O-bound (threading) and CPU-bound (multiprocessing) execution models.
* Forensic Integrity: Maintain an immutable file-based audit trail (audit_results.txt) for all findings.

<br>

## 4. Setup & Environment 💻
| Category | Details |
| :--- | :--- |
| **Attacker OS** | Kali Linux (Virtual Machine) |
| **Target Environment** | Localhost (127.0.0.1) - High-volume simulation |
| **Processor** | Intel Core i5 |
| **Memory (RAM)** | 8GB |
| **Language** | Python 3.10 |
| **Network** | VirtualBox NAT |

<br>

## 5. Technical Methodology
* Batch-Processing Architecture: To prevent system-level process termination (zsh: killed), the engine segments 2,000,000 tasks into 50,000-task batches. This ensures memory stability (O(1) complexity).
* Execution Paradigms:
   * Sequential: Baseline iteration.
   * Concurrent (ThreadPoolExecutor): Utilizes lightweight threads for I/O multiplexing.
   * Parallel (multiprocessing.Pool): Distributes audit logic across CPU cores.
* Forensic Logging: All successful service discoveries are piped to audit_results.txt for post-scan analysis.

<br>

## 6. Program
<br>

## 7. Key Findings and Result Analysis
**Paradigm Convergence:** At local-loopback speeds, Sequential and Parallel paradigms show near-identical performance.
**Concurrent Overhead:** The higher time for Concurrent mode (threading) in this specific local environment is attributed to the overhead of managing 100+ thread context switches per batch.
**Scalability:** The batch-processing model successfully processed 2 million tasks with a stable memory footprint, proving the engine's reliability for large-scale forensic audit simulations.

<br>

## 7. Discussion
The analysis validates that architectural choice must be context-aware. While Concurrent (Threading) excels at masking high-latency external network wait-times, it introduces significant management overhead when processing rapid, local-loopback tasks. Conversely, Parallel (Multiprocessing) effectively utilizes multiple CPU cores for the high-volume workload, matching the performance of the Sequential baseline while proving the engine is scalable to much larger datasets. This project demonstrates that a robust security auditor must be Adaptive, dynamically selecting the execution paradigm based on the target environment’s latency profile. 

<br>

## 8. Conclusion
This project successfully architected a scalable, high-volume auditor capable of processing 2 million audit tasks. By demonstrating the trade-offs between Sequential, Concurrent, and Parallel architectures, this assignment confirms that modern forensic tools must prioritize memory efficiency and architectural flexibility to be effective in high-throughput environments. 

<br>

## 9. User Guide

<br>

## 10. References
* Python Software Foundation, "concurrent.futures — Launching parallel tasks," 2026.
* A. Grama et al., Introduction to Parallel Computing, 2nd ed. Addison-Wesley, 2003.
