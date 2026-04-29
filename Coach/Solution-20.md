# Challenge 20 - Linux Troubleshooting (Capstone) - Coach's Guide
[< Previous Solution](./Solution-19.md) - **[Home](./README.md)**

## Notes & Guidance

This capstone has three independent scenarios. Students should work through them in order. Each scenario has a setup phase that intentionally creates a broken state, followed by a diagnostic and repair phase.

---

## Scenario A — "The Web Server Is Down"

### Setup (creates the broken state)

```bash
sudo systemctl stop nginx
sudo ufw deny 80/tcp 2>/dev/null
```

> If UFW is not active, the `ufw deny` command will still add the rule but it won't take effect until UFW is enabled. The primary issue is that nginx is stopped.

### Walkthrough

1. Verify the symptom

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
000
```

> A return code of `000` means curl couldn't connect at all — the server isn't listening.

2. Check if nginx is running

`student@vm01:~$ systemctl status nginx`

```bash
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Mon 2025-01-01 12:00:00 UTC; 2min ago
```

> **Root cause #1 identified:** nginx is `inactive (dead)`.

3. Check if port 80 is listening

`student@vm01:~$ sudo ss -tulnp | grep :80`

> No output — confirming nothing is listening on port 80.

4. Start nginx

`student@vm01:~$ sudo systemctl start nginx`

`student@vm01:~$ systemctl status nginx`

```bash
● nginx.service - A high performance web server and a reverse proxy server
     Active: active (running) since Mon 2025-01-01 12:05:00 UTC; 2s ago
```

5. Test again

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
200
```

> If UFW is active and has a deny rule for port 80, localhost connections may still work (UFW typically allows loopback traffic). However, remote connections would fail.

6. Check and fix the firewall (if UFW is active)

`student@vm01:~$ sudo ufw status`

```bash
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     LIMIT IN    Anywhere
80/tcp                     DENY IN     Anywhere
...
```

`student@vm01:~$ sudo ufw delete deny 80/tcp`

```bash
Rule deleted
Rule deleted (v6)
```

`student@vm01:~$ sudo ufw allow 80/tcp`

```bash
Rule added
Rule added (v6)
```

7. Final verification

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
200
```

> Both issues are now resolved: nginx is running and the firewall allows port 80.

---

## Scenario B — "Disk Space Alert"

### Setup (creates the test files)

```bash
dd if=/dev/zero of=/tmp/bigfile bs=1M count=100 2>/dev/null
mkdir -p /tmp/oldlogs
for i in $(seq 1 50); do dd if=/dev/zero of=/tmp/oldlogs/app-$i.log bs=1M count=1 2>/dev/null; done
```

> This creates a 100MB file and 50 x 1MB log files (150MB total).

### Walkthrough

1. Check disk usage

`student@vm01:~$ df -h`

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G   5.2G   24G  18% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           393M  1.1M  392M   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sda15      105M  6.1M   99M   6% /boot/efi
tmpfs           393M   12K  393M   1% /run/user/1000
```

> The exact figures will vary. The student should note the current usage level.

2. Find what's consuming space in /tmp

`student@vm01:~$ du -sh /tmp/* 2>/dev/null | sort -rh | head -10`

```bash
100M    /tmp/bigfile
50M     /tmp/oldlogs
4.0K    /tmp/practice.log
4.0K    /tmp/mycron
...
```

> **Root cause identified:** `/tmp/bigfile` (100MB) and `/tmp/oldlogs/` (50MB) are consuming the most space.

3. Find files larger than 10MB

`student@vm01:~$ find /tmp -size +10M -exec ls -lh {} \; 2>/dev/null`

```bash
-rw-rw-r-- 1 student student 100M Jan  1 12:00 /tmp/bigfile
```

4. Count old log files

`student@vm01:~$ find /tmp/oldlogs -name "*.log" -type f | wc -l`

```bash
50
```

5. Clean up

`student@vm01:~$ rm /tmp/bigfile`

`student@vm01:~$ rm -rf /tmp/oldlogs`

6. Verify disk space recovered

`student@vm01:~$ df -h`

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G   5.1G   24G  18% /
...
```

> The used space should have decreased by approximately 150MB.

---

## Scenario C — "High CPU Mystery"

### Setup (creates the runaway process)

```bash
nohup bash -c 'while true; do echo "busy" > /dev/null; done' &
```

> This creates an infinite loop in a bash process that will consume nearly 100% of one CPU core.

### Walkthrough

1. Check system load

`student@vm01:~$ uptime`

```bash
 12:10:00 up  2:10,  1 user,  load average: 1.05, 0.78, 0.42
```

> A load average above 1.0 on a single-core machine (or above the number of CPU cores) indicates CPU pressure. The 1-minute average (first number) will be highest since the process was just started.

2. Identify the top CPU consumers

`student@vm01:~$ ps aux --sort=-%cpu | head -10`

```bash
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
student     2500 99.0  0.1   7488  3456 pts/0    R    12:08   2:15 bash -c while true; do echo "busy" > /dev/null; done
root           1  0.1  0.5 168936 11584 ?        Ss   10:00   0:05 /sbin/init
root         610  0.0  0.3  25332  7168 ?        Ss   10:00   0:01 /lib/systemd/systemd-resolved
student     1800  0.0  0.2  10568  5376 pts/0    Ss   11:00   0:00 -bash
...
```

> **Root cause identified:** PID 2500 is a bash process running at 99% CPU with the command `while true; do echo "busy" > /dev/null; done`.

Alternatively, using `top`:

`student@vm01:~$ top -b -n 1 | head -20`

```bash
top - 12:10:00 up 2:10,  1 user,  load average: 1.05, 0.78, 0.42
Tasks: 105 total,   2 running, 103 sleeping,   0 stopped,   0 zombie
%Cpu(s): 50.2 us,  0.3 sy,  0.0 ni, 49.3 id,  0.0 wa,  0.0 hi,  0.2 si,  0.0 st
MiB Mem :   1963.2 total,    923.4 free,    512.8 used,    527.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1315.6 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2500 student   20   0    7488   3456   3200 R  99.0   0.2   2:15.23 bash
      1 root      20   0  168936  11584   8448 S   0.1   0.6   0:05.12 systemd
    610 root      20   0   25332   7168   6400 S   0.0   0.4   0:01.34 systemd-resolve
```

3. Find the runaway bash process and its PID

> From the output above, PID `2500` is the culprit (the actual PID will vary on each system).

4. Check what the process is doing

`student@vm01:~$ cat /proc/2500/cmdline | tr '\0' ' '`

```bash
bash -c while true; do echo "busy" > /dev/null; done
```

> This confirms the process is running the infinite loop. The `tr '\0' ' '` converts null bytes (which separate arguments in `/proc/*/cmdline`) into spaces for readability.

5. Kill the process

`student@vm01:~$ kill 2500`

6. If it doesn't stop, force kill it

`student@vm01:~$ kill -9 2500`

> `kill` sends SIGTERM (signal 15) which asks the process to exit gracefully. `kill -9` sends SIGKILL which terminates it immediately. For this infinite loop, `kill` (SIGTERM) should work since the bash process will handle it.

7. Verify CPU usage is back to normal

`student@vm01:~$ uptime`

```bash
 12:12:00 up  2:12,  1 user,  load average: 0.65, 0.72, 0.45
```

> The 1-minute load average should start dropping. It may take a few minutes for all three load averages to normalize since they are exponential moving averages (1-minute, 5-minute, 15-minute).

8. Check memory usage

`student@vm01:~$ free -h`

```bash
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       512Mi       923Mi       1.0Mi       527Mi       1.3Gi
Swap:             0B          0B          0B
```

> Memory should be fine — the runaway process was CPU-intensive, not memory-intensive. The `available` column is the best indicator of usable memory (it includes reclaimable cache).
