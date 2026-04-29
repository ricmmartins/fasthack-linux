# Challenge 16 - systemd & Service Management

[< Previous Challenge](./Challenge-15.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-17.md)

## Description

systemd is the init system and service manager for modern Linux distributions. It controls how services start, stop, and are managed throughout the system lifecycle. Understanding systemd is crucial for any Linux administrator — it's how you manage everything from web servers to databases to custom applications.

## Tasks

1. List all active services: `systemctl list-units --type=service --state=active`
2. Check the status of the SSH service: `systemctl status ssh`
3. Check if nginx is installed and running: `systemctl status nginx`. If not installed, install it first with `sudo apt install -y nginx`
4. Stop the nginx service: `sudo systemctl stop nginx` — then verify it stopped
5. Start nginx again: `sudo systemctl start nginx` — verify it's running
6. Restart nginx (stop+start in one command): `sudo systemctl restart nginx`
7. Disable nginx from starting at boot: `sudo systemctl disable nginx` — verify with `systemctl is-enabled nginx`
8. Re-enable nginx at boot: `sudo systemctl enable nginx`
9. View the last 20 lines of nginx logs: `journalctl -u nginx --no-pager -n 20`
10. View all logs from the last hour: `journalctl --since "1 hour ago" --no-pager | tail -30`
11. Create a custom systemd service: Create a file `/etc/systemd/system/hello.service` with this content:

```
[Unit]
Description=Hello World Service
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/echo "Hello from systemd!"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Then reload systemd with `sudo systemctl daemon-reload`, start the service, and check its status and logs.

## Success Criteria

1. You can list, start, stop, restart, enable, and disable services
2. You can check the status and logs of any service
3. You can filter journal logs by service and time
4. Your custom hello.service runs successfully

## Learning Resources

- [systemd documentation](https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html)
- [Ubuntu systemd service guide](https://ubuntu.com/server/docs/managing-services-with-systemd)
- [journalctl manual](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)
- [How to create a systemd service](https://linuxhandbook.com/create-systemd-services/)

## Bridge to Kubernetes

Kubernetes components like kubelet and containerd run as systemd services. When troubleshooting a Kubernetes node, `systemctl status kubelet` and `journalctl -u kubelet` are your first diagnostic tools.
