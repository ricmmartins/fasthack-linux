# Desafio 09 - Discos, partições e sistemas de arquivos - Guia do Coach 

[< Solução Anterior](./Solution-08.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-10.md)

## Notas e Orientações
1. Identifique o novo disco adicionado à máquina

`student@vm01:~$ sudo fdisk -l | grep "^Disk"`

```bash
Disk /dev/loop0: 43.64 MiB, 45748224 bytes, 89352 sectors
Disk /dev/loop1: 61.92 MiB, 64901120 bytes, 126760 sectors
Disk /dev/loop2: 67.83 MiB, 71106560 bytes, 138880 sectors
Disk /dev/sda: 30 GiB, 32213303296 bytes, 62916608 sectors
Disk model: Virtual Disk
Disklabel type: gpt
Disk identifier: D9AF7253-EE93-498D-B696-43092C65B2DD
Disk /dev/sdb: 4 GiB, 4294967296 bytes, 8388608 sectors
Disk model: Virtual Disk
Disklabel type: dos
Disk identifier: 0x4e60c282
Disk /dev/sdc: 5 GiB, 5368709120 bytes, 10485760 sectors
Disk model: Virtual Disk
```

`student@vm01:~$ sudo dmesg | grep sdc`

```bash
[  150.665009] sd 1:0:0:0: [sdc] 10485760 512-byte logical blocks: (5.37 GB/5.00 GiB)
[  150.665012] sd 1:0:0:0: [sdc] 4096-byte physical blocks
[  150.665235] sd 1:0:0:0: [sdc] Write Protect is off
[  150.665237] sd 1:0:0:0: [sdc] Mode Sense: 0f 00 10 00
[  150.666843] sd 1:0:0:0: [sdc] Write cache: disabled, read cache: enabled, supports DPO and FUA
[  150.694433] sd 1:0:0:0: [sdc] Attached SCSI disk
```

2. Edite a tabela de partição do disco:

    `student@vm01:~$ sudo fdisk /dev/sdc`

    1. Adicione uma nova partição com 500MB
    
    ```bash
    Welcome to fdisk (util-linux 2.34).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x29026b65.

    Command (m for help): n
    Partition type
        p   primary (0 primary, 0 extended, 4 free)
        e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-10485759, default 2048):
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-10485759, default 10485759): +500M

    Created a new partition 1 of type 'Linux' and of size 500 MiB.

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```
    
    2. Liste e identifique no S.O. a partição criada

    `student@vm01:~$ ls -l /dev/sdc*`
    
    ```bash
    brw-rw---- 1 root disk 8, 32 Apr  6 15:09 /dev/sdc
    brw-rw---- 1 root disk 8, 33 Apr  6 15:09 /dev/sdc1
    ```
    
    3. Apague a partição

    `student@vm01:~$ sudo fdisk /dev/sdc`

    ```bash
    Welcome to fdisk (util-linux 2.34).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.


    Command (m for help): d
    Selected partition 1
    Partition 1 has been deleted.

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

    4. Verifique no S.O. que a partição foi removida

    `student@vm01:~$ ls -l /dev/sdc*`

    ```bash
    brw-rw---- 1 root disk 8, 32 Apr  6 15:12 /dev/sdc
    ```

    5. Adicione duas novas partições com uma partição Linux nativa (83), uma com 500MB e outra com 100MB

    `student@vm01:~$ sudo fdisk /dev/sdc`
    
    ```bash
    Welcome to fdisk (util-linux 2.34).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.


    Command (m for help): n
    Partition type
        p   primary (0 primary, 0 extended, 4 free)
        e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-10485759, default 2048):
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-10485759, default 10485759): +500M

    Created a new partition 1 of type 'Linux' and of size 500 MiB.

    Command (m for help): n
    Partition type
        p   primary (1 primary, 0 extended, 3 free)
        e   extended (container for logical partitions)
    Select (default p): p
    Partition number (2-4, default 2):
    First sector (1026048-10485759, default 1026048):
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (1026048-10485759, default 10485759): +100M
    
    Created a new partition 2 of type 'Linux' and of size 100 MiB.

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

    6. Verifique no S.O. que as partições foram criadas

    `student@vm01:~$ ls -l /dev/sdc*`
    
    ```bash
    brw-rw---- 1 root disk 8, 32 Apr  6 15:53 /dev/sdc
    brw-rw---- 1 root disk 8, 33 Apr  6 15:53 /dev/sdc1
    brw-rw---- 1 root disk 8, 34 Apr  6 15:53 /dev/sdc2
    ```
    
3. Crie um sistema de arquivos em cada uma das partições criadas

`student@vm01:~$ sudo mkfs.ext4 /dev/sdc1`

```bash
mke2fs 1.45.5 (07-Jan-2020)
Discarding device blocks: done
Creating filesystem with 128000 4k blocks and 128000 inodes
Filesystem UUID: 789bd630-3dc8-4356-9bd5-d96f3172f1d1
Superblock backups stored on blocks:
    32768, 98304

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

`student@vm01:~$ sudo mkfs.ext4 /dev/sdc2`

```bash
mke2fs 1.45.5 (07-Jan-2020)
Discarding device blocks: done
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```

4. Crie um diretório para cada uma das partições dentro do diretório `/mnt`

`student@vm01:~$ sudo mkdir /mnt/dir1`

`student@vm01:~$ sudo mkdir /mnt/dir2`


5. Monte cada uma das partições no respectivo diretório

`student@vm01:~$ sudo mount /dev/sdc1 /mnt/dir1`

`student@vm01:~$ sudo mount /dev/sdc2 /mnt/di2`


6. Verifique que as partições estão montadas corretamente no S.O.

`student@vm01:~$ sudo ls -l /mnt/dir*`

```bash
/mnt/dir1:
total 16
drwx------ 2 root root 16384 Apr  6 15:59 lost+found

/mnt/dir2:
total 16
drwx------ 2 root root 16384 Apr  6 15:59 lost+found
```

7. Escreva arquivos dentro de uma das partições

`student@vm01:~$ sudo touch /mnt/dir1/file1`

`student@vm01:~$ sudo touch /mnt/dir2/file1`

`student@vm01:~$ sudo ls -l /mnt/dir*`

```bash
/mnt/dir1:
total 16
-rw-r--r-- 1 root root     0 Apr  6 16:13 file1
drwx------ 2 root root 16384 Apr  6 15:59 lost+found

/mnt/dir2:
total 16
-rw-r--r-- 1 root root     0 Apr  6 16:13 file1
drwx------ 2 root root 16384 Apr  6 15:59 lost+found
```

8. Desmonte as partições

`student@vm01:~$ sudo umount /mnt/dir1`

`student@vm01:~$ sudo umount /mnt/dir2`

9. Remova as partições existentes

`student@vm01:~$ sudo fdisk /dev/sdc`

```bash
Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): d
Partition number (1,2, default 2): 1

Partition 1 has been deleted.

Command (m for help): d
Selected partition 2
Partition 2 has been deleted.

Command (m for help): w
The partition table has been altered.

The kernel still uses the old partitions. The new table will be used at the next reboot.
Syncing disks.
```