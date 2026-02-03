🐧 Linux Server Monitoring & Incident Simulation
Project Overview

This project simulates real-world Linux production incidents and demonstrates system monitoring, troubleshooting, and incident resolution skills. A Linux server environment was configured to intentionally generate high CPU, memory, and disk usage scenarios. Each incident was analyzed using standard Linux monitoring and logging tools, followed by documented root cause analysis and resolution steps.

The project focuses on hands-on system administration, incident response, and production-style debugging rather than theoretical learning.

Objectives

Understand Linux system performance metrics

Simulate common production incidents

Perform root cause analysis using system logs

Practice incident resolution and validation

Document incidents in a professional format

Environment

OS: Ubuntu Server 22.04 LTS

Platform: VirtualBox / WSL / Cloud VM

User: Non-root (sudo access)

Tools & Commands Used

top, htop

free, vmstat

df, du

journalctl

stress

uptime, ps

Incident Simulations
🔴 Incident 1: High CPU Utilization

Symptoms

Increased system load

Slow command execution

High load average

Simulation

stress --cpu 4 --timeout 300


Detection

top
htop
uptime


Root Cause Analysis

ps aux --sort=-%cpu | head


Resolution

pkill stress


Validation

uptime

🔴 Incident 2: High Memory Usage

Symptoms

Low available memory

Performance degradation

Swap usage increase

Simulation

stress --vm 2 --vm-bytes 1G --timeout 300


Detection

free -h
htop
vmstat 2


Root Cause Analysis

Stress process consuming excessive memory

Resolution

pkill stress
sync && echo 3 | sudo tee /proc/sys/vm/drop_caches

🔴 Incident 3: Disk Space Exhaustion

Symptoms

Disk usage reaching 100%

Application failures

Log write errors

Simulation

fallocate -l 5G bigfile


Detection

df -h
du -sh *


Log Analysis

journalctl --disk-usage


Resolution

rm bigfile
journalctl --vacuum-time=2d


Validation

df -h

Log Analysis

System logs were analyzed using journalctl to identify system errors and confirm incident timelines.

journalctl -xe
journalctl --since "10 minutes ago"
journalctl -u ssh

Key Learnings

Linux system performance monitoring

Incident detection and response workflow

Root cause analysis using system logs

Production-style troubleshooting techniques

Importance of monitoring and preventive measures

Preventive Measures

Implement system monitoring alerts

Define resource usage thresholds

Enable log rotation

Apply process and disk usage limits

Resume Highlights

Simulated Linux production incidents and performed root cause analysis using system logs and monitoring tools

Analyzed CPU, memory, and disk utilization using Linux performance commands

Documented incident resolution steps following production incident workflows

Future Improvements

Integrate monitoring tools like Prometheus or Nagios

Automate alerting using scripts or cron jobs

Extend simulations to network-related incidents

Author

Mohammed Sami Nadaf
Linux | System Administration | DevOps Fundamentals