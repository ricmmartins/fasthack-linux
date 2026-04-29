# Challenge 20 - Linux Troubleshooting (Capstone)

[< Previous Challenge](./Challenge-19.md) - **[Home](../README.md)**

## Description

This capstone challenge combines everything you've learned. You'll work through three realistic troubleshooting scenarios that test your ability to diagnose and fix issues using the tools from all previous challenges. Each scenario starts with a symptom — your job is to investigate, identify the root cause, and fix it.

## Scenario A — "The Web Server Is Down"

Your team reports that the web server is unreachable. Diagnose and fix the issue.

**Setup** (run these commands to create the broken state):

```bash
sudo systemctl stop nginx
sudo ufw deny 80/tcp 2>/dev/null
```

**Tasks:**

1. Verify the symptom: `curl -s -o /dev/null -w "%{http_code}" http://localhost:80` (should fail or return nothing)
2. Check if nginx is running: `systemctl status nginx`
3. Check if port 80 is listening: `sudo ss -tulnp | grep :80`
4. Start nginx: `sudo systemctl start nginx`
5. Test again — still blocked? Check the firewall: `sudo ufw status`
6. Allow port 80: `sudo ufw allow 80/tcp`
7. Verify the fix: `curl -s -o /dev/null -w "%{http_code}" http://localhost:80` (should return 200)

## Scenario B — "Disk Space Alert"

Monitoring reports the /tmp partition is filling up. Investigate and clean up.

**Setup:**

```bash
dd if=/dev/zero of=/tmp/bigfile bs=1M count=100 2>/dev/null
mkdir -p /tmp/oldlogs
for i in $(seq 1 50); do dd if=/dev/zero of=/tmp/oldlogs/app-$i.log bs=1M count=1 2>/dev/null; done
```

**Tasks:**

1. Check disk usage: `df -h`
2. Find what's consuming space in /tmp: `du -sh /tmp/* 2>/dev/null | sort -rh | head -10`
3. Find files larger than 10MB in /tmp: `find /tmp -size +10M -exec ls -lh {} \; 2>/dev/null`
4. Find old log files (created during setup): `find /tmp/oldlogs -name "*.log" -type f | wc -l`
5. Clean up: Remove the big file and old logs:

```bash
rm /tmp/bigfile
rm -rf /tmp/oldlogs
```

6. Verify disk space recovered: `df -h`

## Scenario C — "High CPU Mystery"

A process is consuming excessive CPU. Find and stop it.

**Setup:**

```bash
nohup bash -c 'while true; do echo "busy" > /dev/null; done' &
```

**Tasks:**

1. Check system load: `uptime`
2. Identify the top CPU consumers: `top -b -n 1 | head -20` or `ps aux --sort=-%cpu | head -10`
3. Find the runaway bash process and its PID
4. Check what the process is doing: `cat /proc/<PID>/cmdline | tr '\0' ' '`
5. Kill the process: `kill <PID>`
6. If it doesn't stop: `kill -9 <PID>`
7. Verify CPU usage is back to normal: `uptime` (load should start dropping)
8. Also check memory usage: `free -h`

## Success Criteria

1. **Scenario A:** Web server is running and accessible on port 80
2. **Scenario B:** Identified and removed the large files; disk space recovered
3. **Scenario C:** Found and killed the runaway process; CPU load is decreasing

## Reset Instructions

If you need to retry any scenario, re-run the corresponding setup commands above.

## Learning Resources

- [Linux troubleshooting guide](https://www.brendangregg.com/linuxperf.html)
- [systemctl documentation](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
- [How to find large files](https://linuxhandbook.com/find-large-files-linux/)
- [Linux process management](https://tldp.org/LDP/tlk/kernel/processes.html)

## Bridge to Kubernetes

In Kubernetes, troubleshooting follows similar patterns: `kubectl describe pod` is like `systemctl status`, `kubectl logs` is like `journalctl`, `kubectl top pod` is like `top`, and `kubectl exec` lets you run these same Linux tools inside containers. The diagnostic mindset is identical.
