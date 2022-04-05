# Getting help

This chapter will explain the use of man pages (also called manual pages) on your Unix or Linux computer. 

You will learn the man command together with related commands like whereis, whatis and mandb.

Most Unix files and commands have pretty good man pages to explain their use. Man pages also come in handy when you are using multiple flavours of Unix or several Linux distributions since options and parameters sometimes vary.

1.1. man $command

Type man followed by a command (for which you want help) and start reading. Press q to 
quit the manpage. Some man pages contain examples (near the end).

```
user@server:~$ man whois
Reformatting whois(1), please wait...
```

1.2. man $configfile

Most configuration files have their own manual.

```
user@server:~$ man syslog.conf
Reformatting syslog.conf(5), please wait...
```

1.3. man $daemon

This is also true for most daemons (background programs) on your system..

1.4. man -k (apropos)

man -k (or apropos) shows a list of man pages containing a string.

1.5. whatis

To see just the description of a manual page, use whatis followed by a string.

1.6. whereis

The location of a manpage can be revealed with whereis.

This file is directly readable by man.
paul@laika:~$ man /usr/share/man/man1/whois.1.gz
paul@laika:~$ man whois
Reformatting whois(1), please wait...
paul@laika:~$ man syslog.conf
Reformatting syslog.conf(5), please wait...
paul@laika:~$ man syslogd
Reformatting syslogd(8), please wait...
paul@laika:~$ man -k syslog
lm-syslog-setup (8) - configure laptop mode to switch syslog.conf ... 
logger (1) - a shell command interface to the syslog(3) ... 
syslog-facility (8) - Setup and remove LOCALx facility for sysklogd 
syslog.conf (5) - syslogd(8) configuration file
syslogd (8) - Linux system logging utilities. 
syslogd-listfiles (8) - list system logfiles
paul@u810:~$ whatis route
route (8) - show / manipulate the IP routing table
paul@laika:~$ whereis -m whois
whois: /usr/share/man/man1/whois.1.gz
1.7. man sections
By now you will have noticed the numbers between the round brackets. man man will 
explain to you that these are section numbers. Executable programs and shell commands 
reside in section one.
1.8. man $section $file
Therefor, when referring to the man page of the passwd command, you will see it written 
as passwd(1); when referring to the passwd file, you will see it written as passwd(5). The 
screenshot explains how to open the man page in the correct section.
1.9. man man
If you want to know more about man, then Read The Fantastic Manual (RTFM).
Unfortunately, manual pages do not have the answer to everything...
1.10. mandb
Should you be convinced that a man page exists, but you can't access it, then try running
mandb on Debian/Mint.
Or run makewhatis on CentOS/Redhat.
[root@centos65 ~]# apropos scsi 
scsi: nothing appropriate 
[root@centos65 ~]# makewhatis
[root@centos65 ~]# apropos scsi
hpsa (4) - HP Smart Array SCSI driver
lsscsi (8) - list SCSI devices (or hosts) and their attributes
sd (4) - Driver for SCSI Disk Drives
st (4) - SCSI tape device
