# 🐧 Linux Server Monitoring & Incident Simulation

## Project Overview

This project simulates real-world Linux production incidents and demonstrates system monitoring, troubleshooting, and incident resolution skills.

A Linux server environment was configured to intentionally generate high CPU, memory, and disk usage scenarios. Each incident was analyzed using standard Linux monitoring and logging tools, followed by documented root cause analysis and resolution steps.

The project focuses on hands-on system administration, incident response, and production-style debugging rather than theoretical learning.

---

## Objectives

- Understand Linux system performance metrics  
- Simulate common production incidents  
- Perform root cause analysis using system logs  
- Practice incident resolution and validation  
- Document incidents in a professional format  

---

## Environment

- **OS:** Ubuntu Server 22.04 LTS  
- **Platform:** VirtualBox / WSL / Cloud VM  
- **User:** Non-root user with sudo access  

---

## Tools & Commands Used

- top, htop  
- free, vmstat  
- df, du  
- journalctl  
- stress  
- uptime, ps  

---

## Incident Simulations

---

### 🔴 Incident 1: High CPU Utilization

#### Symptoms

- Increased system load  
- Slow command execution  
- High load average  

#### Simulation

```bash
stress --cpu 4 --timeout 300
