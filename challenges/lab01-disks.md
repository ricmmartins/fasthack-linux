# Disks, Partitions and File Systems

## Requirements

* Create two data disks
* Add to the Virtual Machine

## Objectives

* Identify the new disk added to the machine
* Edit the disk partition table:
  * Add a new partition
  * List and identify in the S.O. the partition created
  * Erase partition
  * Check in S.O. that the partition has been removed
  * Add two new partitions with type 83
  * Check in S.O. that the partitions were created
* Create a file system on each of the partitions created
* Create a directory for each of the partitions inside the /mnt directory
* Mount each of the partitions in the respective directory
* Verify that the partitions are mounted correctly in OS.
* Write files inside one of the partitions
* Unmount the partitions
* Remove existing partitions

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
