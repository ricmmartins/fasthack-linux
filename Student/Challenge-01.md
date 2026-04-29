# Challenge 01 - Create a Linux Virtual Machine

**[Home](../README.md)** - [Next Challenge >](./Challenge-02.md)

## Prerequisites

- Access to one of the following environments to run a Linux instance (see Description below).

## Description

To follow along you will need access to a server running a Linux-based operating system. This hackathon was validated using Ubuntu 24.04 ([LTS](https://ubuntu.com/about/release-cycle)), but the examples should work on any Ubuntu/Debian-based distribution. Choose any of the paths below to set up your environment:

### Option 1: Cloud VM (Azure, AWS, or GCP)

Create an Ubuntu 24.04 LTS virtual machine on your preferred cloud provider. During the creation process, ensure the usage of **student** for the username with root (sudo) privileges, just to make it easier during the challenges.

### Option 2: Local VM (VirtualBox, UTM, Hyper-V, or VMware)

Download the Ubuntu 24.04 LTS ISO and create a virtual machine locally. Use **student** as the username.

### Option 3: WSL2 on Windows

Install the Windows Subsystem for Linux with Ubuntu 24.04. Use **student** as the username.

### Option 4: Existing Server

If you already have access to an Ubuntu/Debian-based Linux server, you can use it directly. Create a **student** user with sudo privileges if one does not already exist.

### Disclaimer

Opening port 22 to the public internet is a bad practice. If you are using a cloud VM, we highly recommend restricting SSH access in your firewall or cloud security group to your home IP address only, rather than allowing access from all sources.

## Success Criteria

* Validate you were able to successfully create your Linux virtual machine (or set up your Linux environment)
* Confirm you can access it through SSH (or open a terminal session)

## Learning Resources

### Azure
* [Create a Linux virtual machine in the Azure portal](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
* [Create a Linux virtual machine with the Azure CLI](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli)
* [Connect to a Linux VM](https://learn.microsoft.com/en-us/azure/virtual-machines/linux-vm-connect?tabs=Linux)

### AWS
* [Launch a Linux Virtual Machine on AWS](https://aws.amazon.com/getting-started/launch-a-virtual-machine/)

### GCP
* [Create a Linux VM instance on Google Cloud](https://cloud.google.com/compute/docs/create-linux-vm-instance)

### Local VM / WSL2
* [Download Ubuntu Desktop/Server ISO](https://ubuntu.com/download)
* [VirtualBox Manual](https://www.virtualbox.org/manual/)
* [Install WSL on Windows](https://learn.microsoft.com/en-us/windows/wsl/install)

