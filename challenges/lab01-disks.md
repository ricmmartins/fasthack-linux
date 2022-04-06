# Disks, Partitions and File Systems

## Requirements

* Create two data disks
* Add to the Virtual Machine

## Objectives

1. Identify the new disk added to the machine
2. Edit the disk partition table:
    1. Add a new partition
    2. List and identify in the S.O. the partition created
    3. Erase partition
    4. Check in S.O. that the partition has been removed
    5. Add two new partitions with type 83
    6. Check in S.O. that the partitions were created
3. Create a file system on each of the partitions created
4. Create a directory for each of the partitions inside the /mnt directory
5. Mount each of the partitions in the respective directory
6. Verify that the partitions are mounted correctly in OS.
7. Write files inside one of the partitions
8. Unmount the partitions
9. Remove existing partitions

## LVM

* Create a Physical Volume (```PV```) with the disk added
* Check that the ```PV``` is created
* Create a Volume Group (```VG```) using the created PV
* Verify that the VG is created
* Create a Logical Volume (```LV```) using half the disk
* Create an ```LV``` using 10% of the disk
* Verify that ```LV```s are created
* Format both ```LV```s as ```ext4```
* Mount the ```LV```s in the directories created earlier in ```/mnt```
* Resize the smallest ```LV``` to take up another 20% of the disk
* Check:
 * That the ```LV``` has been resized
 * If there was reflection in the file system
* Resize the file system

------------
[Answers](https://github.com/ricmmartins/fasthack-linux-answers/blob/main/challenges/lab01-disks.md)
