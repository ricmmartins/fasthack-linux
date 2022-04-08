




### Control Operators

35. Echo **it worked** when **touch test** works, and echo **it failed** when the **touch** failed. All on one command line as a normal user (not root). Test this line in your home directory and in `/bin/` 
36. Execute **sleep 60** in background (do no wait for it to finish)
37. Write a command line that executes **rm ~/file1**. Your command line should print '**success**' if file is removed, and print '**failed**' if there was a problem.
38. When you type passwd, which file is executed?
39. What kind of file is that?

### Standard file permissions

40. As normal user, create a directory `~/permissions`. Create a file owned by yourself in there.
41. Copy a file owned by root from `/etc/` to your permissions dir, who owns this file now?
42. As root, create a file in the users `~/permissions` directory.
43. As normal user, look at who owns this file created by root.
44. Change the ownership of all files in `~/permissions` to yourself.
45. Make sure you have all rights to files within `~`, and others can only read

### Process Management

46. View the list of your server processes
47. How many processes are running on your server
48. View the list of processes in tree format
49. Identify if the omsagent process is running
50. Identify the process id of the omsagent

### Group and user management

51. Create the groups: marketing, finance, apps and production
52. Create the users below with the given characteristics:
    1. login: anna, main group: marketing
    2. login: mary, main group: finance
    3. login: peter, main group: apps
    4. login: rick, main group: production
53. Create passwords for all users

### Scripting

54. Create a script that looks up the name of the current distribution in the `/etc/os-release` file and prints it to the screen
55. Create a script that reads the usernames from `/etc/passwd` and prints the ones with shell ending in sh
56. Create a script that adds two integers requested from the user

-----------
[Answers](https://github.com/ricmmartins/fasthack-linux-answers/blob/main/challenges/lab-firststeps.md)
