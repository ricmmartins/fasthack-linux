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

1. Create a Physical Volume (```PV```) with the disk added
2. Check that the ```PV``` is created
3. Create a Volume Group (```VG```) using the created PV
4. Verify that the VG is created
5. Create a Logical Volume (```LV```) using half the disk
6. Create an ```LV``` using 10% of the disk
7. Verify that ```LV```s are created
8. Format both ```LV```s as ```ext4```
9. Mount the ```LV```s in the directories created earlier in ```/mnt```
10. Resize the smallest ```LV``` to take up another 20% of the disk
11. Check:
    1. That the ```LV``` has been resized
    2. If there was reflection in the file system
12. Resize the file system

------------
[Answers](https://github.com/ricmmartins/fasthack-linux-answers/blob/main/challenges/lab01-disks.md)
