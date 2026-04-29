# Challenge 19 - Firewall Configuration with UFW - Coach's Guide
[< Previous Solution](./Solution-18.md) - **[Home](./README.md)** - [Next Solution >](./Solution-20.md)

## Notes & Guidance

> **Recovery note:** If a student gets locked out of their VM after enabling UFW without allowing SSH, they should access the VM via a cloud console (serial console in most cloud providers) or local display and run `sudo ufw disable` to restore access.

1. Check the current firewall status

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: inactive
```

> By default, UFW is installed but not enabled on Ubuntu 24.04.

2. Allow SSH access before enabling the firewall

`student@vm01:~$ sudo ufw allow 22/tcp`

```bash
Rules updated
Rules updated (v6)
```

> **CRITICAL:** This must be done before step 3. If the student changed the SSH port in Challenge 13 (e.g., to 2222), they must use `sudo ufw allow 2222/tcp` instead.

3. Enable the firewall

`student@vm01:~$ sudo ufw enable`

```bash
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```

4. Check status after enabling

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

> The default policy is `deny (incoming)` — all incoming traffic is blocked unless explicitly allowed. Outgoing traffic is allowed by default.

5. Allow HTTP and HTTPS

`student@vm01:~$ sudo ufw allow 80/tcp`

```bash
Rule added
Rule added (v6)
```

`student@vm01:~$ sudo ufw allow 443/tcp`

```bash
Rule added
Rule added (v6)
```

6. Allow access from a specific subnet

`student@vm01:~$ sudo ufw allow from 10.0.0.0/8 to any port 3306`

```bash
Rule added
```

> This allows MySQL connections (port 3306) only from the 10.0.0.0/8 private network. Note that this rule only creates an IPv4 rule (not v6) because the source is an IPv4 CIDR block.

7. Deny a specific port

`student@vm01:~$ sudo ufw deny 8080/tcp`

```bash
Rule added
Rule added (v6)
```

8. Enable rate limiting on SSH

`student@vm01:~$ sudo ufw delete allow 22/tcp`

```bash
Rule deleted
Rule deleted (v6)
```

`student@vm01:~$ sudo ufw limit 22/tcp`

```bash
Rule added
Rule added (v6)
```

> The `limit` rule allows connections but blocks an IP address that attempts more than 6 connections within 30 seconds. This protects against brute-force SSH attacks.

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW IN    Anywhere
443/tcp                    ALLOW IN    Anywhere
3306                       ALLOW IN    10.0.0.0/8
8080/tcp                   DENY IN     Anywhere
22/tcp                     LIMIT IN    Anywhere
80/tcp (v6)                ALLOW IN    Anywhere (v6)
443/tcp (v6)               ALLOW IN    Anywhere (v6)
8080/tcp (v6)              DENY IN     Anywhere (v6)
22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

9. View all rules with numbers

`student@vm01:~$ sudo ufw status numbered`

```bash
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 80/tcp                     ALLOW IN    Anywhere
[ 2] 443/tcp                    ALLOW IN    Anywhere
[ 3] 3306                       ALLOW IN    10.0.0.0/8
[ 4] 8080/tcp                   DENY IN     Anywhere
[ 5] 22/tcp                     LIMIT IN    Anywhere
[ 6] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 7] 443/tcp (v6)               ALLOW IN    Anywhere (v6)
[ 8] 8080/tcp (v6)              DENY IN     Anywhere (v6)
[ 9] 22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

10. Delete a rule by number

To delete the 8080 deny rule (rule number 4 in the example above):

`student@vm01:~$ sudo ufw delete 4`

```bash
Deleting:
 deny 8080/tcp
Proceed with operation (y|n)? y
Rule deleted
```

> **Important:** After deleting a rule, the remaining rules are renumbered. If you need to delete the corresponding IPv6 rule as well, run `sudo ufw status numbered` again to find its new number, then delete it.

`student@vm01:~$ sudo ufw status numbered`

```bash
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 80/tcp                     ALLOW IN    Anywhere
[ 2] 443/tcp                    ALLOW IN    Anywhere
[ 3] 3306                       ALLOW IN    10.0.0.0/8
[ 4] 22/tcp                     LIMIT IN    Anywhere
[ 5] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 6] 443/tcp (v6)               ALLOW IN    Anywhere (v6)
[ 7] 8080/tcp (v6)              DENY IN     Anywhere (v6)
[ 8] 22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

Now delete the IPv6 8080 rule (now rule 7):

`student@vm01:~$ sudo ufw delete 7`

```bash
Deleting:
 deny 8080/tcp
Proceed with operation (y|n)? y
Rule deleted (v6)
```

11. Enable and view UFW logs

`student@vm01:~$ sudo ufw logging on`

```bash
Logging enabled
```

`student@vm01:~$ grep -i ufw /var/log/syslog | tail -10`

```bash
Jan  1 12:30:00 vm01 kernel: [UFW BLOCK] IN=eth0 OUT= MAC=... SRC=192.168.1.100 DST=10.0.0.4 LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=12345 DF PROTO=TCP SPT=54321 DPT=8080 WINDOW=64240 RES=0x00 SYN URGP=0
```

> If `/var/log/syslog` doesn't exist (rsyslog not installed), use `journalctl` instead:

`student@vm01:~$ sudo journalctl --no-pager | grep -i ufw | tail -10`

> UFW log entries show `[UFW BLOCK]` or `[UFW ALLOW]` along with source/destination IP, port, and protocol. These logs are invaluable for troubleshooting connectivity issues.
