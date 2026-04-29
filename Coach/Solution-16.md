# Challenge 16 - systemd & Service Management - Coach's Guide
[< Previous Solution](./Solution-15.md) - **[Home](./README.md)** - [Next Solution >](./Solution-17.md)

## Notes & Guidance

1. List all active services

`student@vm01:~$ systemctl list-units --type=service --state=active`

```bash
  UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
  cron.service                       loaded active running Regular background program processing daemon
  dbus.service                       loaded active running D-Bus System Message Bus
  getty@tty1.service                 loaded active running Getty on tty1
  networkd-dispatcher.service        loaded active running Dispatcher daemon for systemd-networkd
  rsyslog.service                    loaded active running System Logging Service
  ssh.service                        loaded active running OpenBSD Secure Shell server
  systemd-journald.service           loaded active running Journal Service
  systemd-logind.service             loaded active running User Login Management
  systemd-networkd.service           loaded active running Network Configuration
  systemd-resolved.service           loaded active running Network Name Resolution
  systemd-udevd.service              loaded active running Rule-based Manager for Device Events and Files
  ...
```

2. Check the status of the SSH service

`student@vm01:~$ systemctl status ssh`

```bash
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 10:00:00 UTC; 2h ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 700 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 750 (sshd)
      Tasks: 1 (limit: 4657)
     Memory: 5.2M
        CPU: 120ms
     CGroup: /system.slice/ssh.service
             └─750 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
```

> On Ubuntu 24.04, the SSH service is named `ssh` (not `sshd` as on some other distributions).

3. Check if nginx is installed and running

`student@vm01:~$ systemctl status nginx`

If nginx is not installed, you will see:

```bash
Unit nginx.service could not be found.
```

Install it:

`student@vm01:~$ sudo apt install -y nginx`

Then check again:

`student@vm01:~$ systemctl status nginx`

```bash
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 12:00:00 UTC; 10s ago
       Docs: man:nginx(8)
    Process: 1234 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1235 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1236 (nginx)
      Tasks: 3 (limit: 4657)
     Memory: 4.8M
        CPU: 50ms
     CGroup: /system.slice/nginx.service
             ├─1236 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
             ├─1237 "nginx: worker process"
             └─1238 "nginx: worker process"
```

4. Stop the nginx service and verify

`student@vm01:~$ sudo systemctl stop nginx`

`student@vm01:~$ systemctl status nginx`

```bash
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Mon 2025-01-01 12:05:00 UTC; 5s ago
    Process: 1235 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1236 (code=exited, status=0/SUCCESS)
        CPU: 50ms
```

> Note the status changed from `active (running)` to `inactive (dead)`.

5. Start nginx again

`student@vm01:~$ sudo systemctl start nginx`

`student@vm01:~$ systemctl is-active nginx`

```bash
active
```

6. Restart nginx

`student@vm01:~$ sudo systemctl restart nginx`

`student@vm01:~$ systemctl is-active nginx`

```bash
active
```

7. Disable nginx from starting at boot

`student@vm01:~$ sudo systemctl disable nginx`

```bash
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install disable nginx
Removed "/etc/systemd/system/multi-user.target.wants/nginx.service".
```

`student@vm01:~$ systemctl is-enabled nginx`

```bash
disabled
```

8. Re-enable nginx at boot

`student@vm01:~$ sudo systemctl enable nginx`

```bash
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable nginx
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
```

`student@vm01:~$ systemctl is-enabled nginx`

```bash
enabled
```

9. View the last 20 lines of nginx logs

`student@vm01:~$ journalctl -u nginx --no-pager -n 20`

```bash
Jan 01 12:00:00 vm01 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Jan 01 12:00:00 vm01 nginx[1234]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
Jan 01 12:00:00 vm01 nginx[1234]: nginx: configuration file /etc/nginx/nginx.conf test is successful
Jan 01 12:00:00 vm01 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
```

10. View all logs from the last hour

`student@vm01:~$ journalctl --since "1 hour ago" --no-pager | tail -30`

> This will display the most recent 30 lines of all system log entries from the last hour. Output will vary depending on system activity.

11. Create a custom systemd service

`student@vm01:~$ sudo tee /etc/systemd/system/hello.service << 'EOF'`

```bash
[Unit]
Description=Hello World Service
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/echo "Hello from systemd!"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
EOF
```

`student@vm01:~$ sudo systemctl daemon-reload`

`student@vm01:~$ sudo systemctl start hello`

`student@vm01:~$ sudo systemctl status hello`

```bash
● hello.service - Hello World Service
     Loaded: loaded (/etc/systemd/system/hello.service; disabled; preset: enabled)
     Active: active (exited) since Mon 2025-01-01 12:30:00 UTC; 5s ago
    Process: 2000 ExecStart=/usr/bin/echo Hello from systemd! (code=exited, status=0/SUCCESS)
   Main PID: 2000 (code=exited, status=0/SUCCESS)
        CPU: 2ms
```

> The status shows `active (exited)` because the service type is `oneshot` with `RemainAfterExit=yes`. This means the service ran once and completed, but systemd considers it "active" because it should remain in that state.

`student@vm01:~$ journalctl -u hello --no-pager`

```bash
Jan 01 12:30:00 vm01 systemd[1]: Starting hello.service - Hello World Service...
Jan 01 12:30:00 vm01 echo[2000]: Hello from systemd!
Jan 01 12:30:00 vm01 systemd[1]: Finished hello.service - Hello World Service.
```

> The "Hello from systemd!" message is visible in the journal output, confirming the service ran successfully.
