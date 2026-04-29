# What The Hack - Linux Fundamentals - Coach Guide

## Introduction

Welcome to the coach's guide for the Linux Fundamentals Hackathon. Here you will find links to specific guidance for coaches for each of the challenges.

> **NOTE:** If you are a hackathon participant, this is the answer guide. Don't cheat yourself by looking at these during the hack! Go learn something. :)

## Coach's Guides

| # | Solution | Description |
|---|----------|-------------|
| 01 | **[Create a Linux Virtual Machine](Solution-01.md)** | Set up an Ubuntu Linux environment — cloud VM, local VM, or WSL2 |
| 02 | **[Handling Directories](Solution-02.md)** | Common directory operations |
| 03 | **[Handling Files](Solution-03.md)** | File manipulation: create, rename, find, and remove files |
| 04 | **[File Contents](Solution-04.md)** | File content manipulation |
| 05 | **[Standard File Permissions](Solution-05.md)** | Linux file permissions and ownership |
| 06 | **[Process Management](Solution-06.md)** | Checking running processes and identifying PIDs |
| 07 | **[Group and User Management](Solution-07.md)** | User and group creation |
| 08 | **[Scripting](Solution-08.md)** | Basic shell scripting |
| 09 | **[Disks, Partitions and File Systems](Solution-09.md)** | fdisk, mkfs, and mount |
| 10 | **[Logical Volume Manager](Solution-10.md)** | pvcreate, vgcreate, lvcreate |
| 11 | **[Package Management](Solution-11.md)** | Package installation and management |
| 12 | **[Setting up a Webserver](Solution-12.md)** | Nginx + PHP-FPM web application deployment |
| 13 | **[Protecting a Server](Solution-13.md)** | Fail2Ban and SSH hardening |
| 14 | **[Running Containers](Solution-14.md)** | Docker containers and image building |

## Coach Prerequisites

This hack has prerequisites that a coach is responsible for understanding and/or setting up BEFORE hosting an event.

### Student Resources

Before the hack, it is the Coach's responsibility to ensure students can access the contents of the `/Student/resources` folder.

## Environment Requirements

Students need access to a Linux environment. The following options are supported:

- **Cloud VM**: Azure, AWS, GCP, or any cloud provider — create an Ubuntu 24.04 LTS VM
- **Local VM**: VirtualBox, UTM, Hyper-V, or VMware with Ubuntu 24.04 LTS
- **WSL2**: Windows Subsystem for Linux (Ubuntu)
- **Existing server**: Any Ubuntu/Debian-based Linux system

For Challenge 09 and 10 (Disks/LVM), students will need the ability to attach an additional disk to their VM. This is straightforward on cloud providers and local VM tools, but not supported on WSL2.

For the optional advanced challenge in Challenge 12 (SSL), students will need:
- A public IP attached to the virtual machine
- Access to the public IP from the internet
- A domain name with DNS management access (optional, for proper SSL)

## Estimated Timing

| Challenge | Time |
|-----------|------|
| 01 - Create a Linux VM | 15-30 min |
| 02 - Handling Directories | 15-20 min |
| 03 - Handling Files | 20-30 min |
| 04 - File Contents | 15-20 min |
| 05 - Standard File Permissions | 20-30 min |
| 06 - Process Management | 15-20 min |
| 07 - Group and User Management | 20-30 min |
| 08 - Scripting | 30-45 min |
| 09 - Disks, Partitions and File Systems | 30-45 min |
| 10 - Logical Volume Manager | 30-45 min |
| 11 - Package Management | 15-20 min |
| 12 - Setting up a Webserver | 30-45 min |
| 13 - Protecting a Server | 30-45 min |
| 14 - Running Containers | 30-45 min |
| **Total** | **~5-7 hours** |

## Repository Contents

- `./Coach` — Coach's guide and solution files
- `./Student` — Student's challenge guide
- `./Student/resources` — Resource files, sample code, and reference materials