# The Filesystem Herarchy Standard

Nearly all Linux distributions are compliant with a universal standard for filesystem directory structure known as the Filesystem Hierarchy Standard (FHS). The FHS defines a set of directories, each of which serve their own special function.

The forward slash (```/```) is used to indicate the root directory in the filesystem hierarchy defined by the FHS.

When a user logs in to the shell, they are brought to their own user directory, stored within ```/home/```. This is referred to as the user’s home directory. The FHS defines ```/home/``` as containing the home directories for regular users.

The root user has its own home directory specified by the FHS: ```/root/```. Note that ```/``` is referred to as the “root directory”, and that it is different from ```root/```, which is stored within ```/```.

Because the FHS is the default filesystem layout on Linux machines, and each directory within it is included to serve a specific purpose, it simplifies the process of organizing files by their function.


<img align="center" src="images/fhs.png"/>
