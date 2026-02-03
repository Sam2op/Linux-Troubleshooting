# 🐧 Linux Server Monitoring & Incident Simulation

![Linux](https://img.shields.io/badge/Linux-Ubuntu%2022.04%20LTS-E95420?logo=ubuntu&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?logo=gnu-bash&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success)
![Project](https://img.shields.io/badge/Project-System%20Administration-blueviolet)

## 📌 Project Overview

This hands-on project simulates real-world **Linux production incidents** to demonstrate system monitoring, troubleshooting, and incident resolution skills. A Linux server environment was intentionally configured to generate high CPU, memory, and disk usage scenarios. Each incident was analyzed using standard Linux monitoring and logging tools, followed by documented root cause analysis and resolution steps.

> **Focus:** Practical system administration, incident response, and production-style debugging.

---

## 📖 Table of Contents
- [Objectives](#🎯-objectives)
- [Environment](#🖥️-environment)
- [Tools & Commands](#🛠️-tools--commands-used)
- [Incident Simulations](#🔴-incident-simulations)
  - [High CPU Utilization](#-incident-1-high-cpu-utilization)
  - [High Memory Usage](#-incident-2-high-memory-usage)
  - [Disk Space Exhaustion](#-incident-3-disk-space-exhaustion)
- [Log Analysis](#📋-log-analysis)
- [Key Learnings](#📚-key-learnings)
- [Preventive Measures](#🛡️-preventive-measures)
- [Resume Highlights](#📄-resume-highlights)
- [Future Improvements](#🚀-future-improvements)
- [Author](#👨‍💻-author)

---

## 🎯 Objectives

- Understand Linux system performance metrics
- Simulate common production incidents
- Perform root cause analysis using system logs
- Practice incident resolution and validation
- Document incidents in a professional format

---

## 🖥️ Environment

| Component       | Details                     |
|-----------------|-----------------------------|
| **OS**          | Ubuntu Server 22.04 LTS     |
| **Platform**    | VirtualBox / WSL / Cloud VM |
| **User**        | Non-root (sudo access)      |
| **Focus**       | Production-like debugging   |

---

## 🛠️ Tools & Commands Used

| Category       | Tools/Commands                                          |
|----------------|---------------------------------------------------------|
| **CPU Monitoring**  | `top`, `htop`, `uptime`, `ps`                          |
| **Memory Monitoring** | `free`, `vmstat`, `htop`                               |
| **Disk Monitoring**  | `df`, `du`, `journalctl --disk-usage`                  |
| **Log Analysis**    | `journalctl -xe`, `journalctl --since`, `journalctl -u`|
| **Stress Tools**    | `stress`, `fallocate`                                  |
| **Resolution**      | `pkill`, `sync`, `rm`, `echo 3 > /proc/sys/vm/drop_caches` |

---

## 🔴 Incident Simulations

### 🚨 Incident 1: High CPU Utilization

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms**     | Increased system load, slow command execution, high load average        |
| **Simulation**   | `stress --cpu 4 --timeout 300`                                          |
| **Detection**    | `top`, `htop`, `uptime`                                                 |
| **Root Cause**   | `ps aux --sort=-%cpu | head` identified `stress` processes            |
| **Resolution**   | `pkill stress`                                                          |
| **Validation**   | `uptime` showed load average returning to normal                        |

### 🚨 Incident 2: High Memory Usage

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms**     | Low available memory, performance degradation, swap usage increase      |
| **Simulation**   | `stress --vm 2 --vm-bytes 1G --timeout 300`                             |
| **Detection**    | `free -h`, `htop`, `vmstat 2`                                           |
| **Root Cause**   | Stress processes consuming excessive memory                             |
| **Resolution**   | `pkill stress` followed by `sync && echo 3 | sudo tee /proc/sys/vm/drop_caches` |
| **Validation**   | `free -h` showed memory returning to baseline                           |

### 🚨 Incident 3: Disk Space Exhaustion

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms**     | Disk usage reaching 100%, application failures, log write errors        |
| **Simulation**   | `fallocate -l 5G bigfile`                                               |
| **Detection**    | `df -h`, `du -sh *`                                                     |
| **Log Analysis** | `journalctl --disk-usage`                                               |
| **Resolution**   | `rm bigfile` and `journalctl --vacuum-time=2d`                          |
| **Validation**   | `df -h` confirmed disk space recovered                                  |

---

## 📋 Log Analysis

System logs were analyzed using `journalctl` to identify errors and confirm incident timelines.

```bash
journalctl -xe                          # View recent logs with details
journalctl --since "10 minutes ago"     # Time-based filtering
journalctl -u ssh                       # Service-specific logs