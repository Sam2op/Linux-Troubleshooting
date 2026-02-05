# Incident: Disk Space Exhaustion

### Symptoms
- Disk usage at 100%
- Application failures
- Log write errors

### Detection Tools
- df
- du
- journalctl

### Root Cause
- Large file consumption
- Log accumulation

### Resolution
- Removed large file
- Cleaned logs

### Preventive Measures
- Disk monitoring
- Log rotation
- Regular cleanup