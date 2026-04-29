# Challenge 18 - Task Scheduling with Cron - Coach's Guide
[< Previous Solution](./Solution-17.md) - **[Home](./README.md)** - [Next Solution >](./Solution-19.md)

## Notes & Guidance

1. Check if cron is running

`student@vm01:~$ systemctl status cron`

```bash
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 10:00:00 UTC; 3h ago
       Docs: man:cron(8)
   Main PID: 800 (cron)
      Tasks: 1 (limit: 4657)
     Memory: 428.0K
        CPU: 15ms
     CGroup: /system.slice/cron.service
             └─800 /usr/sbin/cron -f -P
```

> On Ubuntu 24.04, the cron service is called `cron` (not `crond` as on some other distributions).

2. View the current user's crontab

`student@vm01:~$ crontab -l`

```bash
no crontab for student
```

> This is expected if no cron jobs have been set up yet.

3. Understand cron syntax

The five fields are:

```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of week (0 - 7, where 0 and 7 are Sunday)
│ │ │ │ │
* * * * * command to execute
```

Common examples:
- `*/5 * * * *` — every 5 minutes
- `0 * * * *` — every hour at minute 0
- `30 2 * * *` — every day at 2:30 AM
- `0 0 * * 0` — every Sunday at midnight
- `0 9 1 * *` — first day of every month at 9:00 AM

4. Create a scheduled task

`student@vm01:~$ echo '*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log' > /tmp/mycron`

`student@vm01:~$ crontab /tmp/mycron`

```bash
crontab: installing new crontab
```

`student@vm01:~$ crontab -l`

```bash
*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log
```

5. Verify the cron job executed (after waiting 5 minutes)

`student@vm01:~$ cat /tmp/cron-test.log`

```bash
Cron is alive at Mon Jan  1 12:05:00 UTC 2025
Cron is alive at Mon Jan  1 12:10:00 UTC 2025
```

> If the file doesn't exist yet, the cron job hasn't fired. Wait until the next 5-minute boundary (e.g., :00, :05, :10, :15...).

6. Create a cleanup script and schedule it

`student@vm01:~$ cat > /tmp/cleanup.sh << 'EOF'`

```bash
#!/bin/bash
find /tmp -name "*.log" -mtime +7 -delete 2>/dev/null
echo "Cleanup ran at $(date)" >> /var/log/cleanup.log
EOF
```

`student@vm01:~$ chmod +x /tmp/cleanup.sh`

Add to cron:

`student@vm01:~$ echo '0 0 * * * /tmp/cleanup.sh' >> /tmp/mycron`

`student@vm01:~$ crontab /tmp/mycron`

```bash
crontab: installing new crontab
```

`student@vm01:~$ crontab -l`

```bash
*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log
0 0 * * * /tmp/cleanup.sh
```

> **Note:** The cleanup script writes to `/var/log/cleanup.log`, which requires root permissions. If running as a non-root user, the cron job will silently fail to write to that log. In a real scenario, you'd either run it via `sudo crontab -e` (root's crontab) or write to a user-accessible location.

7. View system-wide cron jobs

`student@vm01:~$ ls -la /etc/cron.d/ /etc/cron.daily/ /etc/cron.hourly/`

```bash
/etc/cron.d/:
total 20
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
-rw-r--r--  1 root root  201 Jan  1  2024 e2scrub_all

/etc/cron.daily/:
total 28
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
-rwxr-xr-x  1 root root  376 Jan  1  2024 apport
-rwxr-xr-x  1 root root 1478 Jan  1  2024 apt-compat
-rwxr-xr-x  1 root root  123 Jan  1  2024 dpkg
-rwxr-xr-x  1 root root  377 Jan  1  2024 logrotate

/etc/cron.hourly/:
total 8
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
```

> Scripts placed in `/etc/cron.daily/` are run once a day by the system. Similarly, `/etc/cron.hourly/`, `/etc/cron.weekly/`, and `/etc/cron.monthly/` exist for other intervals.

8. Install and use `at` for a one-time task

`student@vm01:~$ sudo apt install -y at`

`student@vm01:~$ echo "echo 'One-time task ran at $(date)' >> /tmp/at-test.log" | at now + 1 minute`

```bash
warning: commands will be executed using /bin/sh
job 1 at Mon Jan  1 12:31:00 2025
```

`student@vm01:~$ atq`

```bash
1       Mon Jan  1 12:31:00 2025 a student
```

> The `atq` command shows queued jobs. The job number (1), scheduled time, queue letter (a), and username are displayed.

9. Verify the `at` job ran (after waiting 1 minute)

`student@vm01:~$ cat /tmp/at-test.log`

```bash
One-time task ran at Mon Jan  1 12:31:00 UTC 2025
```

`student@vm01:~$ atq`

```bash
```

> After the job runs, `atq` will show an empty list — the job has been removed from the queue.

10. Clean up — remove your crontab

`student@vm01:~$ crontab -r`

`student@vm01:~$ crontab -l`

```bash
no crontab for student
```

> The `-r` flag removes the entire crontab for the current user. Use with care — there is no confirmation prompt.
