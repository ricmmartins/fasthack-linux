# Linux basic concepts

## All files are case sensitive

Files on Linux are case sensitive. This means that MYLOG.txt is different from mylog.txt.

This example shows the difference between two files, one with upper case S, the other with lower case s.

```bash
student@vm1:~/Linux$ ls summer.txt  Summer.txt
student@vm1:~/Linux$ cat summer.txt It is hot.
student@vm1:~/Linux$ cat Summer.txt It is very hot!
```

## Everything is a file

In Linux everything is considered a file. This includes hardware devices, processes, directories, regular files, sockets, links, and so on. Also, the file system is usually divided into data blocks and inodes. With that said, you can think of inodes as the foundation of the Linux file system. To explain it more clearly, an Inode is a data structure that stores metadata about every file on your system. Is a file data structure that stores information about any Linux file except its name and data.

Information contained in an Inode:

* File size;
* Device on which the file is stored;
* User and group IDs associated with the file;
* Permissions required to access the file;
* Creating, reading and writing timestamps;
* Data location (but not the file path).

In addition, Inodes are also independent of file names. So this means you can copy a single file, rename it and still have it point to the same Inode as the original.

