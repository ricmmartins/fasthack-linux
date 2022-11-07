# Challenge 13 - Protecting a Server

[< Previous Challenge](./Challenge-12.md) - **[Home](../README.md)**

## Description

In a server, especially those directly exposed to the Internet such as web servers are very common to receive thousand of authentication attempts. If you check your /var/log/auth.log file, you will attest to this. 

99.999% of those logins fail. They are based on silly dictionary attacks, which (unfortunately) work in some % of the cases. Are you sure that your password and the passwords of all the users on your system are strong enough to survive such an attack? This is why the usage of SSH Keys is a better alternative than the user/password approach. 

The idea behind Fail2ban is very simple: temporarily or permanently ban an IP that performed multiple undesired actions, such as unsuccessful authentication, access to a restricted area, etc. Originally it was developed to catch illegal SSH login attempts, but later on, it grew up into an easily customizable toolkit for speedy reaction on some events (such as detected failed login attempts) recorded in the log files.

- Install the package fail2ban
- Validate the configuration file /etc/fail2ban/jail.conf
- Make sure it's working as expected


## Success Criteria

1. Ensure the distribution lists are updated
2. Ensure the installation of fail2ban package
3. Make sure that Fail2Ban will start automatically during the VM boot
4. Ensure Fail2Ban is enabled to protect the SSH service

## Learning resoures

- [How Fail2Ban Works to Protect Services on a Linux Server]([https://linuxjourney.com/lesson/software-distribution](https://www.digitalocean.com/community/tutorials/how-fail2ban-works-to-protect-services-on-a-linux-server))
- [Using Fail2ban to Secure Your Server]([https://www.tecmint.com/linux-package-management/](https://www.linode.com/docs/guides/using-fail2ban-to-secure-your-server-a-tutorial/))
- [How to Install and Configure Fail2ban on Ubuntu 20.04]([https://www.linode.com/docs/guides/linux-package-management-overview/](https://linuxize.com/post/install-configure-fail2ban-on-ubuntu-20-04/))
