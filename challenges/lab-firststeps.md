
# First Steps on the command line

## Requirements

* N/A

## Objectives

### Working with directories

1. Display your current directory
2. Go to the parent directory of the current directory
3. Go to the root directory
4. List the contents of the root directory
5. List a long listing of the root directory
6. Stay where you are, and list the contents of ~
7.  List all the files (including hidden files) in your home directory
8. Create in one command the directories ~/dir1/dir2/dir3 (dir3 is a subdirectory from dir2, and dir2 is a subdirectory from dir1)
9. List recursively the content of your ~ 

###  Working with files

10. Display the type of file of /bin/cat, /etc/passwd and /usr/bin/passwd
11. Download [azure-linux.svg](https://docs.microsoft.com/en-us/learn/achievements/azure-linux.svg)  and [azure-ops-guide.pdf](https://docsmsftpdfs.blob.core.windows.net/guides/azure/azure-ops-guide.pdf) 
12. Display the type of file of azure-linux.svg and azure-ops-guide.pdf
13. Rename vmlinux.png to vmlinux.pdf 
14. Display the type of file of azure-linux.pdf and azure-ops-guide.pdf
15. Create a directory ~/touched and enter it.
16. Create the files today.txt and yesterday.txt in touched.
17. Check the creation date and time:
18. Change the date on yesterday.txt to match yesterday's date
19. Check the creation date and time again: 
20. Create a directory called ~/testbackup and copy all files from ~/touched into it.
21. Use one command to remove the directory ~/testbackup and all files into it.
22. Create a directory ~/etcbackup and copy all *.conf files from /etc into it. Did you include all subdirectories of /etc ?

### File contents

23. Display the first 12 lines of /etc/services
24. Display the last line of /etc/passwd
25. Use cat to create a file named count.txt that looks like this
26. Use cp to make a backup of this file to cnt.txt
27. Use cat to make a backup of this file to catcnt.txt
28. Display catcnt.txt, but with all lines in reverse order (the last line first)
29. Use more to display /etc/services
30. Use ls to find the biggest file in /etc

### Control Operators

31. Echo **it worked** when **touch test** works, and echo **it failed** when the **touch** failed. All on one command line as a normal user (not root). Test this line in your home directory and in /bin/ 
32. Execute **sleep 60** in background (do no wait for it to finish)
33. Write a command line that executes **rm ~/file1**. Your command line should print '**success**' if file is removed, and print '**failed**' if there was a problem.
34. When you type passwd, which file is executed?
35. What kind of file is that?
-----------
[Answers](https://github.com/ricmmartins/fasthack-linux-answers/blob/main/challenges/lab-firststeps.md)
