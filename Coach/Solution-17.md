# Challenge 17 - Text Processing with sed, awk, and Pipes - Coach's Guide
[< Previous Solution](./Solution-16.md) - **[Home](./README.md)** - [Next Solution >](./Solution-18.md)

## Notes & Guidance

1. Create a sample log file for exercises

`student@vm01:~$ sudo cp /var/log/syslog /tmp/practice.log 2>/dev/null || journalctl --no-pager -n 200 > /tmp/practice.log`

> On Ubuntu 24.04, `/var/log/syslog` exists if rsyslog is installed. If not, the fallback uses `journalctl` to generate a practice log. Either source works for the exercises.

2. Use `cut` to extract the first three fields

`student@vm01:~$ cut -d' ' -f1-3 /tmp/practice.log | head -10`

```bash
Jan 01 10:00:00
Jan 01 10:00:01
Jan 01 10:00:01
Jan 01 10:00:02
Jan 01 10:00:03
Jan 01 10:00:05
Jan 01 10:00:05
Jan 01 10:00:10
Jan 01 10:00:10
Jan 01 10:00:15
```

> If using `journalctl` output, the format may differ slightly (e.g., `Jan 01 10:00:00` vs a longer timestamp). Adjust the field numbers if needed.

3. Find the top 10 most frequent words in column 5

`student@vm01:~$ awk '{print $5}' /tmp/practice.log | sort | uniq -c | sort -rn | head -10`

```bash
     45 systemd[1]:
     23 systemd-resolved[610]:
     18 sshd[750]:
     12 networkd-dispatcher[680]:
     10 cron[800]:
      8 systemd-logind[690]:
      5 kernel:
      3 dbus-daemon[620]:
      2 rsyslogd:
      1 snapd[900]:
```

> The output shows which processes generate the most log entries. This is useful for identifying noisy services.

4. Convert to uppercase with `tr`

`student@vm01:~$ head -5 /tmp/practice.log | tr '[:lower:]' '[:upper:]'`

```bash
JAN 01 10:00:00 VM01 SYSTEMD[1]: STARTED NETWORK NAME RESOLUTION.
JAN 01 10:00:01 VM01 SYSTEMD[1]: STARTED OPENBSD SECURE SHELL SERVER.
JAN 01 10:00:01 VM01 SSHD[750]: SERVER LISTENING ON 0.0.0.0 PORT 22.
JAN 01 10:00:02 VM01 SSHD[750]: SERVER LISTENING ON :: PORT 22.
JAN 01 10:00:03 VM01 SYSTEMD[1]: REACHED TARGET MULTI-USER SYSTEM.
```

5. Use `sed` to replace hostname with "REDACTED"

First, find your hostname:

`student@vm01:~$ hostname`

```bash
vm01
```

Then replace it:

`student@vm01:~$ sed 's/vm01/REDACTED/g' /tmp/practice.log > /tmp/redacted.log`

Verify:

`student@vm01:~$ head -3 /tmp/redacted.log`

```bash
Jan 01 10:00:00 REDACTED systemd[1]: Started Network Name Resolution.
Jan 01 10:00:01 REDACTED systemd[1]: Started OpenBSD Secure Shell server.
Jan 01 10:00:01 REDACTED sshd[750]: Server listening on 0.0.0.0 port 22.
```

> Replace `vm01` with the actual hostname of the student's machine.

6. Delete blank lines with `sed`

`student@vm01:~$ sed '/^$/d' /tmp/practice.log`

> This removes all empty lines. The regex `^$` matches lines with nothing between the start (`^`) and end (`$`). To see the effect, you can compare line counts:

```bash
wc -l /tmp/practice.log
sed '/^$/d' /tmp/practice.log | wc -l
```

7. Print lines longer than 80 characters with `awk`

`student@vm01:~$ awk 'length > 80' /tmp/practice.log | head -10`

> This will show only the longer log entries. Typical long lines include service descriptions, SSH authentication messages, or kernel messages.

8. Sum a numeric column with `awk`

`student@vm01:~$ echo -e "apples 5\nbananas 12\noranges 3\ngrapes 8" > /tmp/fruits.txt`

`student@vm01:~$ awk '{sum += $2} END {print "Total:", sum}' /tmp/fruits.txt`

```bash
Total: 28
```

> The `awk` program adds column 2 (`$2`) to a running `sum` variable for each line, then prints the total after processing all lines (`END` block). This pattern is extremely useful for summing values in reports, logs, or CSV files.

9. Find unique IP addresses in the log

`student@vm01:~$ grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' /tmp/practice.log | sort -u`

```bash
0.0.0.0
10.0.0.4
127.0.0.1
127.0.0.53
168.63.129.16
```

> The `-o` flag outputs only the matched portion (not the entire line), and `-E` enables extended regex. The regex `[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+` matches IPv4 address patterns. `sort -u` removes duplicates. Note: this regex is a simple pattern and may match version numbers or other dot-separated numbers — for production use, you'd add range validation.

10. Count .conf files under /etc

`student@vm01:~$ find /etc -name "*.conf" 2>/dev/null | wc -l`

```bash
87
```

> The exact count depends on installed packages. The `2>/dev/null` suppresses "Permission denied" errors for directories the student can't read. The `wc -l` counts the number of lines (one file per line) from `find`'s output.
