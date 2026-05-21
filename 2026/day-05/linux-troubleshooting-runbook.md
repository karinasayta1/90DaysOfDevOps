# Linux Troubleshooting Runbook – SSH Service

This runbook provides quick troubleshooting steps if the SSH service goes down.

---

## Environment Basics

### Command:

`uname -a`

**Output:**
Linux afroz 6.14.0-37-generic #37~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Thu Nov 20 10:25:38 UTC x86_64 x86_64 x86_64 GNU/Linux

**Observation:** Kernel version and architecture confirmed.

---

### Command:

`cat /etc/os-release`

**Output:**
PRETTY_NAME="Ubuntu 24.04.3 LTS"
VERSION="24.04.3 LTS (Noble Numbat)"

**Observation:** Confirms distribution and OS version.

---

## Filesystem Sanity

### Command:

`mkdir /tmp/runbook-demo`

**Observation:** Directory created successfully.

---

### Command:

`cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo`

**Observation:** File copied successfully. Filesystem is writable.

---

## CPU & Memory

### Command:

`ps -o pid,pcpu,pmem,comm -p $(pidof sshd)`

**Output:**
PID %CPU %MEM COMMAND
1415  0.0  0.0 sshd

**Observation:** SSH process running with negligible CPU and memory usage.

---

### Command:

`free -h`

**Output:**
Total: 7.7G, Used: 2.3G, Available: 5.4G

**Observation:** Sufficient memory available.

---

## Disk & IO

### Command:

`df -h`

**Output:**
/dev/sdb4 496G 15G 457G 3% /

**Observation:** Root partition has more than 90% free space.

---

### Command:

`iostat`

**Observation:**

* CPU idle ~84% (healthy)
* iowait ~3% (low)
* system ~2.9% (low)
* user ~9–10% (normal workload)

---

## Network

### Command:

`sudo ss -tulpn | grep sshd`

**Output:**
Port 22 is in LISTEN state

**Observation:** SSH is actively listening on port 22.

---

### Command:

`nc -zv localhost 22`

**Output:**
Connection succeeded

**Observation:** SSH connectivity confirmed.

---

## Logs

### Command:

`journalctl -u ssh -n 50`

**Observation:** No errors or warnings; normal authentication logs.

---

### Command:

`tail -n 50 /var/log/auth.log`

**Observation:** Recent login activity looks normal, no suspicious entries.

---

## Quick Review

* SSH service running normally
* CPU and memory usage low
* Disk space sufficient
* Port 22 is open and accessible
* Logs show no errors

---

## If This Worsens

1. Check logs again for errors:
   `journalctl -u ssh`

2. Monitor system resources:
   CPU / Memory / Disk

3. Restart SSH service:
   `systemctl restart ssh`

4. Verify port conflicts:
   Check if port 22 is used by another service

---
