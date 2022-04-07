# Linux Commands Cheat Sheet 

The command line terminal in Linux is the operating system’s most powerful component. However, due to the sheer amount of commands available, it can be intimidating for newcomers. Even longtime users may forget a command every once in a while and that is why we have created this Linux cheat sheet commands guide.

In this tutorial, we’ll present you with a curated list of the most handy Linux commands. 

## Hardware information

| Command | Description |
|--------------|--------------
|`dmesg` | Show bootup messages |
| `cat /proc/cpuinfo` | See CPU information|
| `free -h` | Display free and used memory |
| `lshw` | List hardware configuration information |
| `lsblk` | See information about block devices |
| `lspci -tv`| Show PCI devices in a tree-like diagram | 
| `dmidecode` |Show hardware information from the BIOS |
| `hdparm -i /dev/disk` | Display disk data information |
| `hdparm -tT /dev/[device]` | Conduct a read-speed test on device/disk |
| `fsck [disk-or-partition-location]`| Run a disk check on an unmounted disk or partition | 

## Searching

| Command | Description |
|--------------|--------------
|`grep [pattern] [file_name]` | Search for a specific pattern in a file with grep |
| `grep -r [pattern] [directory_name]` | Recursively search for a pattern in a directory:|
| `locate [name]` | Find all files and directories related to a particular name: |
| `find [/folder/location] -name [a]` | List names that begin with a specified character [a] in a specified location [/folder/location] by using the find command: |
| `find [/folder/location] -size [+100M]` | See files larger than a specified size [+100M] in a folder: |

## File Commands

| Command | Description |
|--------------|--------------
|`ls` | List files in the directory|
| `ls -a` | List all files (shows hidden files)|
| `locate [name]` | Find all files and directories related to a particular name: |
| `pwd` | Show directory you are currently working in |
| `mkdir [directory]` | Create a new directory |
| `rm [file_name]` | Remove a file |
| `rm -r [directory_name]`| Remove a directory recursively|
|`rm -rf [directory_name]`|Recursively remove a directory without requiring confirmation|
|`cp [file_name1] [file_name2]`|Copy the contents of one file to another file|
|`cp -r [directory_name1] [directory_name2]`|Recursively copy the contents of one file to a second file|
|`mv [file_name1] [file_name2]`|Rename [file_name1] to [file_name2] with the command|
|`ln -s /path/to/[file_name] [link_name]`|Create a symbolic link to a file|

