# FastHack - Mastering Linux 
FastHack Linux Edition - This FastHack will serves as an introduction to important command line concepts and skills to learn more about Linux.
<img align="right" src="images/linuxpenguin.png" width="250"/>

## Linux History 

Linux is a family of free and open-source operating systems based on the Linux kernel. Operating systems based on Linux are known as Linux distributions or distros. Examples include Debian, Ubuntu, Fedora, CentOS, Gentoo, Arch Linux, and many others.

The Linux kernel has been under active development since 1991, and has proven to be extremely versatile and adaptable. You can find computers that run Linux in a wide variety of contexts all over the world, from web servers to cell phones. Today, 90% of all cloud infrastructure and 74% of the world’s smartphones are powered by Linux.

To read more about Linux History, Linux Distributions and Linux Kernel, [click here](linux-history.md).


## Prerequisites

### A Linux Virtual Machine

To follow along you will need access to a server running a Linux-based operating system. Note that this fasthack was validated using a Linux server running Ubuntu 20.04 ([LTS](https://ubuntu.com/about/release-cycle)), but the examples given should work on any Linux distribution. See below the steps to follow to create your Linux Virtual Machine on Azure and choose that one with which you are more familiar.
* [Create a Linux virtual machine in the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
* [Create a Linux virtual machine with the Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli)
* [Create a Linux virtual machine in Azure with PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell)

### Access to a Terminal

The terms “terminal,” “shell,” and “command line interface” are often used interchangeably, but there are subtle differences between them:

* A terminal is an input and output environment that presents a text-only window running a shell.
* A shell is a program that exposes the computer’s operating system to a user or program. In Linux systems, the shell presented in a terminal is a command line interpreter.
* A command line interface is a user interface (managed by a command line interpreter program) which processes commands to a computer program and outputs the results.
When someone refers to one of these three terms in the context of Linux, they generally mean a terminal environment where you can run commands and see the results printed out to the terminal. 

Becoming a Linux expert requires you to be comfortable with using a terminal. Any administrative task, including file manipulation, package installation, and user management, can be accomplished through the terminal. The terminal is interactive: you specify commands to run and the terminal outputs the results of those commands. To execute any command, you type it into the prompt and press ENTER.

For our activites, is recommended to use the [Azure Cloud Shell](http://shell.azure.com/).

### Basic knowkedge on the Filesystem Hierarchy Standard

Some concepts around the Linux Filesystem Hierarchy Standard (FHS) are recommended, so you can [take a look here](fhs.md) to get more details about it.

## Topics & Challenges

| Topic        | Challenge|
|--------------|-----------|
| 1. Getting help | - |
| 2. Working with directories | Link  |
| 3. Working with files | Link  |
| 4. Working with file contents | Link  |
| 5. The Linux file tree | Link  |
| 6. Commands and arguments | Link  |
| 7. Control operators | Link  |
| 8. Shell variables | Link  |
| 9. Shell embedding and options  | Link  |
| 10. Shell history | Link  |
| 11. File globbing | Link  |
| 12. I/O redirection | Link  |
| 13. Filters | Link  |
| 14. Basic Unix tools | Link  |
| 15. Regular expressions | -  |
| 16. Scripting introduction | Link  |
| 17. Scripting loops | Link  |
| 18. Scripting parameters | Link  |
| 19. More scripting | Link  |
| 20. Introduction to users | Link  |
| 21. User management | Link  |
| 22. User passwords | Link  |
| 23. User profiles | Link  |
| 24. Groups | Link  |
| 25. Standard file permissions | Link  |
| 26. Advanced file permissions | Link  |
| 27. Access control lists | Link  |
| 28. File links | Link  | 


















## Contributions
Contributions in the form of bug reports, feature requests and PRs are always welcome.

Please follow these steps before submitting a PR:

* Create an issue describing the bug or feature request.
* Clone the repository and create a topic branch.
* Make changes, adding new tests for new functionality.
* Submit a PR.

## License
See [LICENSE](LICENSE).
