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

## Topics

| Topic        | Challenge|
|--------------|-----------|
| Juicy Apples | 1.99      |
| Bananas      | **1.89**  |

1. Getting help
2. Working with directories
3. Working with files
4. Working with file contents
5. The Linux file tree
6. Commands and arguments
7. Control operators
8. Shell variables
9. Shell embedding and options
10. Shell history
11. File globbing
12. I/O redirection
13. Filters
14. Basic Unix tools
15. Regular expressions
16. Scripting introduction
17. Scripting loops
18. Scripting parameters
19. More scripting
20. Introduction to users
21. User management
22. User passwords
23. User profiles
24. Groups
25. Standard file permissions
26. Advanced file permissions
27. Access control lists
28. File links


## Challenges

### 1. Working withg directories
### 2. Working with files
### 3. File contents
### 4. File system tree
### 5. Commands and arguments
### 6. Control operators
### 7. Shell variables
### 8. Shell embedding
### 9. Shell history
### 10. File globbing
### 11. Input/output redirection
### 12. Filters
### 13. Basic Unix tools
### 14. Introduction to scripting
### 15. Scripting tests and loops
### 16. Scripting parameters and options
### 17. More scripting
### 18. Introduction to users
### 19. User management
### 20. User passwords
### 21. User profiles
### 22. Groups
### 23. Standard file permissions
### 24. Advanced file permissions
### 25. File links

## Contributions
Contributions in the form of bug reports, feature requests and PRs are always welcome.

Please follow these steps before submitting a PR:

* Create an issue describing the bug or feature request.
* Clone the repository and create a topic branch.
* Make changes, adding new tests for new functionality.
* Submit a PR.

## License
See [LICENSE](LICENSE).
