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

## File descriptors, pipes and redirects

This section explains how the input and output directing features of the GNU/Linux system work. 

A command always generates output that can be incorporated by another command, which generates other output that can be incorporated by another command, and so on until the output of the commands appears in a specific location (on the screen or within a file).


### File Descriptors

Abstraction of an identification to access a file. When a process wants to manipulate a file, it will use a number that is a file descriptor that tells where that file is and how to access it.

There are 3 file descriptors that show how files can be accessed, they are:

* **Standard Input (stdin)**: Standard Input is a stream for text input, linked to the keyboard. It is named as **File Descriptor 0**.

* **Standard Output (stdout)**: The Standard Output is a stream for the normal output of programs. When a program runs successfully, it generates an output that is Standard Output, which is bound to the terminal or in a terminal window. All output generated by the commands is written to Standard Output which is called **File Descriptor 1**.

* **Standard Error (stderr)**: The Standard Error is also a text output stream, but used to display error messages.
When your command fails, it generates an error which is displayed by the Standard Error output, linked to the terminal and is called **File Descriptor 2**.

### Pipes 

Pipe allows you to join two or more commands executed in sequence.

Example:

```bash
ls -l /etc | less 
```

If more than two commands are used with redirection, we name the resulting operation a **Pipeline**.

```bash
ls -l /etc | sort -r | less
```

### Redirects

The redirection operator `>` can send the output of a command to a file, or read from a file.

* **Standard Output Redirection**

```bash
ls -i > inodes.txt
```
Outputs that are redirected to a file are not displayed on the standard output (screen or terminal), precisely because it was redirected to the file, except for standard errors.

```bash
> = create files
>> = add to end of file
```

* **Redirect Standard Input**

The command instead of reading information from a keyboard, it reads from a file. 

Redirect the file into a command

`cat < /etc/group > groups.txt` = The operator with less sign `<` it is an input redirection operator, that is, the contents of the file `/etc/groups/` will be read by the command `cat` and then it will be sent through the output redirection operator `>` to the file "groups.txt"

* **Standard Error Redirection**

To redirect the error message of a command to a file it is necessary to inform the File Descriptor 2 before the redirection operator `>`

Example:

`ls -zz 2> error.txt`

### The tee command

The “tee” command allows you to send the output of a command to a file and to the screen at the same time.

Syntax:

```bash
tee [options] files
```

Options:

```bash
-a = Append the files instead of overwriting it
```

Example:

```bash
ls -l | tee result.txt
```

Example 2:

```bash
ls -i | tee result2.txt | less
```