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
  - [Server Not Reachable](#-incident-2-high-memory-usage)
  - [Disk Space Exhaustion](#-incident-3-disk-space-exhaustion)
  - [Account Locked](#-incident-4-user-unable-to-login-(account-locked))
  - [File Permission Denied](#-incident-2-file-permission-denied)
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
| **Memory Monitoring** | `free`, `htop`                               |
| **Disk Monitoring**  | `df`, `du`, `journalctl --disk-usage`                  |
| **Log Analysis**    | `journalctl -xe`, `journalctl --since`, `journalctl -u`|
| **Stress Tools**    | `stress`, `fallocate`                                  |
| **Resolution**      | `pkill`, `rm` |

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

### 🚨 Incident 2: User Cannot SSH

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms**     | Client tries to SSH, but gets result saying "Connection Refused"        |
| **Simulation**   | `ufw delete allow 22`                                                   |
| **Detection**    | `ss -tulpn`, `systemctl status ssh`, `ufw status`                       |
| **Root Cause**   | Port 22 is listening, but it is not allowed by UFW                      |
| **Resolution**   | `ufw allow 22`, allows default ssh port                                 |
| **Validation**   | `ssh user@IP` ,client successfully logs in to the server                |

### 🚨 Incident 3: Disk Space Exhaustion

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms**     | Disk usage reaching 100%, application failures, log write errors        |
| **Simulation**   | `fallocate -l 5G bigfile`                                               |
| **Detection**    | `df -h`, `du -sh *`                                                     |
| **Log Analysis** | `journalctl --disk-usage`                                               |
| **Resolution**   | `rm bigfile` and `journalctl --vacuum-time=2d`                          |
| **Validation**   | `df -h` confirmed disk space recovered                                  |

### 🚨 Incident 4: User Unable to Login (Account Locked)

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms** | Valid user receives "Permission denied" or "Account locked" during SSH  |
| **Simulation** | `sudo passwd -l sami`                                                   |
| **Detection** | `passwd -S sami`, `faillog -u sami`, `journalctl -u ssh`                |
| **Root Cause** | User account status marked as "L" (Locked) in shadow password file      |
| **Resolution** | `sudo passwd -u sami`                                                   |
| **Validation** | `passwd -S sami` shows "P" (Password set) and user successfully logs in |

---

### 🚨 Incident 5: File Permission Denied

| Aspect           | Details                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Symptoms** | User receives "Permission denied" error when reading or executing a file |
| **Simulation** | `sudo chmod 600 /opt/secure.txt` and `sudo chown root:root /opt/secure.txt` |
| **Detection** | `ls -l /opt/secure.txt`, `id sami`, `namei -l /opt/secure.txt`          |
| **Root Cause** | File ownership and permissions restricted to root only                  |
| **Resolution** | `sudo chmod 644 /opt/secure.txt`                                  |
| **Validation** | `cat /opt/secure.txt` executes successfully as user sami                |

---

## 📋 Log Analysis

System logs were analyzed using `journalctl` to identify errors and confirm incident timelines.

```bash
journalctl -xe                          # View recent logs with details
journalctl --since "10 minutes ago"     # Time-based filtering
journalctl -u ssh                       # Service-specific logs
```
---

# 📚 Key Learnings

✅ Linux system performance monitoring using native tools  
✅ End-to-end incident detection and response workflow  
✅ Root cause analysis using system logs and process inspection  
✅ Production-style troubleshooting and validation techniques  
✅ Importance of proactive monitoring and preventive measures  

# 🛡️ Preventive Measures

- Implement system monitoring alerts for CPU, memory, and disk thresholds
- Define and enforce resource usage limits per process/user
- Enable automatic log rotation and archival
- Schedule regular disk clean-up and log vacuuming
- Use cron jobs for periodic health checks

# 🚀 Future Improvements

- Integrate monitoring tools like Prometheus + Grafana or Nagios
- Automate alerting using shell scripts and cron jobs
- Extend simulations to network-related incidents (high traffic, connection drops)
- Containerize the simulation environment using Docker for reproducibility
- Implement centralized logging with rsyslog or Loki

# 👨‍💻 Author

**Mohammed Sami Nadaf**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue?logo=linkedin)](https://www.linkedin.com/in/mohammed-sami-nadaf-0b81a91b8)  
📧 **Email:** samilesnarnadaf7@gmail.com  

**Skills:** Linux | System Administration | DevOps Fundamentals | Troubleshooting | Shell Scripting

---

> ⚠️ **Disclaimer:** This project was conducted in a controlled virtual environment for educational purposes. Similar commands and diagnostics can be applied in real production systems with appropriate caution and change control procedures.