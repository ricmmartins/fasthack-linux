# Challenge 15 - Networking Fundamentals

[< Previous Challenge](./Challenge-14.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-16.md)

## Description

Networking is the backbone of modern infrastructure. Understanding how Linux handles network interfaces, routing, and DNS is essential for troubleshooting and managing servers. This challenge introduces core networking tools available on every Linux system.

## Tasks

1. List all network interfaces and their IP addresses using `ip addr show`
2. Display only IPv4 addresses using `ip -4 addr show`
3. Show the link-layer status of all interfaces using `ip link show`
4. Display the routing table using `ip route show`. Identify the default gateway.
5. Check DNS configuration using `resolvectl status`. Also view `/etc/resolv.conf` and note it may show a stub resolver (127.0.0.53) — the actual DNS servers are managed by systemd-resolved.
6. Install DNS utilities: `sudo apt install -y dnsutils` — then resolve a domain using `dig google.com` and `nslookup google.com`
7. Install traceroute: `sudo apt install -y traceroute` — then trace the route to google.com
8. Test connectivity to google.com with `ping -c 4 google.com`
9. Use `curl -I https://google.com` to view HTTP response headers
10. Show all listening TCP and UDP ports with `sudo ss -tulnp`. Identify which process is using port 22.

## Success Criteria

1. You can display IP addresses for all network interfaces
2. You can identify the default gateway
3. DNS resolution works with both dig and nslookup
4. You can trace network routes
5. You can identify all listening ports and their associated processes

## Learning Resources

- [ip command cheat sheet](https://access.redhat.com/sites/default/files/attachments/rh_ip_command_cheatsheet_1214_jcs_print.pdf)
- [Linux networking commands](https://www.redhat.com/en/blog/linux-network-commands)
- [Ubuntu networking documentation](https://ubuntu.com/server/docs/about-networking)
- [systemd-resolved](https://www.freedesktop.org/software/systemd/man/latest/systemd-resolved.service.html)

## Bridge to Kubernetes

In Kubernetes, networking is fundamental — Pods communicate over virtual networks, Services provide stable endpoints, and CoreDNS handles cluster DNS resolution. Mastering Linux networking tools helps you debug Kubernetes networking issues with `kubectl exec` into pods.
