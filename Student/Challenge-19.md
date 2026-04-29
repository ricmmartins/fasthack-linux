# Challenge 19 - Firewall Configuration with UFW

[< Previous Challenge](./Challenge-18.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-20.md)

## Description

A firewall is your first line of defense for any server exposed to a network. Ubuntu includes UFW (Uncomplicated Firewall), a user-friendly interface for managing iptables rules. This challenge teaches you how to control network access to your server.

**IMPORTANT SAFETY NOTE:** Before enabling the firewall, ALWAYS allow SSH access first to avoid locking yourself out. If you changed the SSH port in Challenge 13, use that port (e.g., 2222) instead of the default 22.

Also note: If you are running in a cloud environment, the cloud provider's firewall (Security Groups, NSGs, etc.) operates independently from UFW. Both must allow traffic for it to reach your server. UFW manages the host-level firewall only.

If you completed Challenge 14 (Docker), be aware that Docker modifies iptables rules directly and may bypass UFW for container-published ports. For this challenge, test UFW against host services (like nginx) rather than Docker containers.

## Tasks

1. Check the current firewall status: `sudo ufw status verbose`
2. Before enabling, allow SSH access (CRITICAL — do this first!):
   - If using default SSH port: `sudo ufw allow 22/tcp`
   - If you changed SSH port in Challenge 13: `sudo ufw allow 2222/tcp`
3. Enable the firewall: `sudo ufw enable`
4. Check status again: `sudo ufw status verbose` — you should see SSH allowed
5. Allow HTTP and HTTPS: `sudo ufw allow 80/tcp` and `sudo ufw allow 443/tcp`
6. Allow access from a specific subnet (use your local network): `sudo ufw allow from 10.0.0.0/8 to any port 3306` (example: MySQL from internal network only)
7. Deny a specific port: `sudo ufw deny 8080/tcp`
8. Enable rate limiting on SSH to protect against brute force: First delete the existing SSH rule and add a limited one:

```bash
sudo ufw delete allow 22/tcp
sudo ufw limit 22/tcp
```

(Use port 2222 if that's your SSH port)

9. View all rules with numbers: `sudo ufw status numbered`
10. Delete a rule by number: `sudo ufw delete <number>` (delete the 8080 deny rule)
11. View UFW logs: `sudo ufw logging on` then check `sudo journalctl -u ufw --no-pager | tail -20` or `grep -i ufw /var/log/syslog | tail -10`

## Success Criteria

1. Firewall is active and SSH access is preserved
2. HTTP and HTTPS ports are open
3. You can allow access from specific subnets
4. SSH rate limiting is configured
5. You can add and remove rules by number

## Learning Resources

- [Ubuntu UFW documentation](https://ubuntu.com/server/docs/firewalls)
- [UFW man page](https://manpages.ubuntu.com/manpages/noble/man8/ufw.8.html)
- [UFW Essentials](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

## Bridge to Kubernetes

In Kubernetes, NetworkPolicies control pod-to-pod traffic, functioning as a cluster-level firewall. The concepts are similar — allow/deny rules based on ports and source/destination — but applied to Pods and Namespaces instead of IP addresses.
