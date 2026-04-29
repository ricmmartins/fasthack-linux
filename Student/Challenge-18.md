# Challenge 18 - Task Scheduling with Cron

[< Previous Challenge](./Challenge-17.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-19.md)

## Description

Automating repetitive tasks is a core skill for any system administrator. Linux provides cron, a time-based job scheduler that runs commands at specified intervals. From log cleanup to database backups to health checks, cron is the workhorse of Linux automation.

## Tasks

1. Check if cron is running: `systemctl status cron`
2. View the current user's crontab: `crontab -l` (should show "no crontab for student" if empty)
3. Understand cron syntax — the five fields: `minute hour day-of-month month day-of-week`
   Example: `30 2 * * *` = "Every day at 2:30 AM"
4. Create a simple scheduled task using a file-based approach:

```bash
echo '*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log' > /tmp/mycron
crontab /tmp/mycron
crontab -l
```

5. Wait 5 minutes and verify the cron job executed: `cat /tmp/cron-test.log`
6. Create a cleanup script and schedule it:

```bash
cat > /tmp/cleanup.sh << 'EOF'
#!/bin/bash
find /tmp -name "*.log" -mtime +7 -delete 2>/dev/null
echo "Cleanup ran at $(date)" >> /var/log/cleanup.log
EOF
chmod +x /tmp/cleanup.sh
```

Then add it to cron to run daily at midnight:

```bash
echo '0 0 * * * /tmp/cleanup.sh' >> /tmp/mycron
crontab /tmp/mycron
```

7. View system-wide cron jobs: `ls -la /etc/cron.d/ /etc/cron.daily/ /etc/cron.hourly/`
8. Install and use `at` for a one-time task:

```bash
sudo apt install -y at
echo "echo 'One-time task ran at $(date)' >> /tmp/at-test.log" | at now + 1 minute
atq
```

9. After the `at` job runs, verify: `cat /tmp/at-test.log`
10. Clean up — remove your crontab: `crontab -r`

## Success Criteria

1. You can create, list, and remove cron jobs
2. Your scheduled task runs at the expected interval
3. You understand the five-field cron syntax
4. You can schedule one-time tasks with `at`
5. You know where system cron jobs live

## Learning Resources

- [crontab man page](https://man7.org/linux/man-pages/man5/crontab.5.html)
- [Crontab Guru — cron expression editor](https://crontab.guru/)
- [Ubuntu cron guide](https://help.ubuntu.com/community/CronHowto)
- [at command](https://man7.org/linux/man-pages/man1/at.1.html)

## Bridge to Kubernetes

Kubernetes has a CronJob resource that works like Linux cron — same five-field schedule syntax. If you can write a crontab entry, you can write a Kubernetes CronJob spec. The key difference is that Kubernetes CronJobs run in Pods rather than directly on the host.
