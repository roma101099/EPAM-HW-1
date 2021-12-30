# Homework №8

### 1. Imagine you was asked to add new partition to your host for backup purposes. To simulate appearance of new physical disk in your server, please create new disk in Virtual Box (5 GB) and attach it to your virtual machine.
### Also imagine your system started experiencing RAM leak in one of the applications, thus while developers try to debug and fix it, you need to mitigate OutOfMemory errors; you will do it by adding some swap space.

```bash
[roma2@localhost ~]$ lsblk -o NAME,HCTL,SIZE,MOUNTPOINT | grep -i "sd"
sda             2:0:0:0       8G
├─sda1                        1G /boot
└─sda2                        7G
sdb             3:0:0:0      10G
```

#### /dev/sdc - 5GB disk, that you just attached to the VM (in your case it may appear as /dev/sdb, /dev/sdc or other, it doesn't matter)
#### 1.1. Create a 2GB   !!! GPT !!!   partition on /dev/sdc of type "Linux filesystem" (means all the following partitions created in the following steps on /dev/sdc will be GPT as well)

```bash
[roma2@localhost ~]$ sudo fdisk /dev/sdb -l
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.

Disk /dev/sdb: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt
Disk identifier: 4A25C4CD-F50A-47CA-BDA4-883362BA8D8B
[roma2@localhost ~]$ sudo gdisk /dev/sdb
```

#### 1.2. Create a 512MB partition on /dev/sdc of type "Linux swap"

```bash
[roma2@localhost ~]$ sudo gdisk /dev/sdb
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): n
Partition number (1-128, default 1):
First sector (34-20971486, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-20971486, default = 20971486) or {+-}size{KMGTP}: +512M
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): 8200
Changed type of partition to 'Linux swap'

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.
[roma2@localhost ~]$ sudo gdisk /dev/sdb
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): p
Disk /dev/sdb: 20971520 sectors, 10.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 4A25C4CD-F50A-47CA-BDA4-883362BA8D8B
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 20971486
Partitions will be aligned on 2048-sector boundaries
Total free space is 19922877 sectors (9.5 GiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   8200  Linux swap
```

#### 1.3. Format the 2GB partition with an XFS file system

```bash
[roma2@localhost ~]$ sudo mkfs.xfs -f -L XFS /dev/sdb1
meta-data=/dev/sdb1              isize=512    agcount=4, agsize=32768 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=131072, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=855, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

#### 1.4. Initialize 512MB partition as swap space

```bash
[roma2@localhost ~]$ sudo mkswap /dev/sdb2
Setting up swapspace version 1, size = 524284 KiB
без метки, UUID=b9de790a-cf75-4f94-be49-2130483dd484
[roma2@localhost ~]$ sudo swapon /dev/sdb2
```

#### 1.5. Configure the newly created XFS file system to persistently mount at /backup

```bash
[roma2@localhost ~]$ sudo mkswap /dev/sdb2
Setting up swapspace version 1, size = 524284 KiB
без метки, UUID=b9de790a-cf75-4f94-be49-2130483dd484
[roma2@localhost ~]$ sudo swapon /dev/sdb2
[roma2@localhost ~]$ sudo blkid
/dev/sda1: UUID="02aacf73-7c63-43af-8273-8d9d5d1604f7" TYPE="xfs"
/dev/sda2: UUID="sqPSpF-AaZt-uk8z-t9sm-2dod-s23V-rhHzdj" TYPE="LVM2_member"
/dev/sdb1: LABEL="XFS" UUID="f94eacb8-ebf9-4610-a378-5d8106a571e6" TYPE="xfs" PARTLABEL="Linux swap" PARTUUID="c75ad1dc-968d-411c-a5cf-466c780b8a14"
/dev/sdb2: UUID="b9de790a-cf75-4f94-be49-2130483dd484" TYPE="swap" PARTUUID="ee6753a6-2947-4de5-b978-99198519a2db"
/dev/mapper/centos-root: UUID="33636eb0-8536-4a6a-a7d1-1ed2f0d5eccd" TYPE="xfs"
/dev/mapper/centos-swap: UUID="087aa174-f558-468d-8976-de5c719bece0" TYPE="swap"
#
# /etc/fstab
# Created by anaconda on Sun Nov 28 23:14:47 2021
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
/dev/mapper/centos-root /                       xfs     defaults        0 0
UUID=b4841cad-7301-444c-a240-fb87f7b1f3c6 /boot                   xfs     default$
/dev/mapper/centos-swap swap                    swap    defaults        0 0
/dev/sdb1               /backup                 xfs     defaults        0 0
```

#### 1.6. Configure the newly created swap space to be enabled at boot

```bash
[roma2@localhost ~]$ sudo vi /etc/fstab
[roma2@localhost ~]$ cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Sun Nov 28 16:26:15 2021
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
/dev/mapper/centos-root /                       xfs     defaults        0 0
UUID=02aacf73-7c63-43af-8273-8d9d5d1604f7 /boot                   xfs     defaults        0 0
/dev/mapper/centos-swap swap                    swap    defaults        0 0
#added
/dev/sdb2               swap                    swap    defaults        0 0

```

#### 1.7. Reboot your host and verify that /dev/sdc1 is mounted at /backup and that your swap partition  (/dev/sdc2) is enabled

```bash
[roma2@localhost ~]$ reboot
[roma2@localhost ~]$ df
Файловая система        1K-блоков Использовано Доступно Использовано% Cмонтировано в
devtmpfs                  1928216            0  1928216            0% /dev
tmpfs                     1940200            0  1940200            0% /dev/shm
tmpfs                     1940200         8748  1931452            1% /run
tmpfs                     1940200            0  1940200            0% /sys/fs/cgroup
/dev/mapper/centos-root   6486016      1601500  4884516           25% /
/dev/sda1                 1038336       153588   884748           15% /boot
tmpfs                      388044            0   388044            0% /run/user/1000
[roma2@localhost ~]$ cat /proc/swaps
Filename                                Type            Size    Used    Priority
/dev/sdb2                               partition       524284  0       -2
/dev/dm-1                               partition       839676  0       -3
```

### 2. LVM. Imagine you're running out of space on your root device. As we found out during the lesson default CentOS installation should already have LVM, means you can easily extend size of your root device. So what are you waiting for? Just do it!
#### 2.1. Create 2GB partition on /dev/sdc of type "Linux LVM"

```bash
[roma2@localhost ~]$ sudo fdisk /dev/sdb
[sudo] пароль для roma2:
WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Команда (m для справки): n
Номер раздела (3-128, default 3):
First sector (34-20971486, default 2099200):
Last sector, +sectors or +size{K,M,G,T,P} (2099200-20971486, default 20971486): +2G
Created partition 3


Команда (m для справки): t
Номер раздела (1-3, default 3):
Partition type (type L to list all types): 31
Changed type of partition 'Linux filesystem' to 'Linux LVM'

Команда (m для справки): p

Disk /dev/sdb: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt
Disk identifier: 4A25C4CD-F50A-47CA-BDA4-883362BA8D8B


#         Start          End    Size  Type            Name
 1         2048      1050623    512M  Linux swap      Linux swap
 2      1050624      2099199    512M  Linux filesyste
 3      2099200      6293503      2G  Linux LVM
 
Команда (m для справки): w
Таблица разделов была изменена!

Вызывается ioctl() для перечитывания таблицы разделов.

WARNING: Re-reading the partition table failed with error 16: Устройство или ресурс занято.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
Синхронизируются диски.
[roma2@localhost ~]$ sudo partprobe
```
#### 2.2. Initialize the partition as a physical volume (PV)
```bash
[roma2@localhost ~]$ sudo pvcreate /dev/sdb3
  Physical volume "/dev/sdb3" successfully created.
```
#### 2.3. Extend the volume group (VG) of your root device using your newly created PV
```bash
[roma2@localhost ~]$ df /root
Файловая система        1K-блоков Использовано Доступно Использовано% Cмонтировано в
/dev/mapper/centos-root   6486016      1598372  4887644           25% /
[roma2@localhost ~]$ sudo vgextend centos /dev/sdb3
  Volume group "centos" successfully extended
```
#### 2.4. Extend your root logical volume (LV) by 1GB, leaving other 1GB unassigned
```bash
[roma2@localhost ~]$ df -h
Файловая система        Размер Использовано  Дост Использовано% Cмонтировано в
devtmpfs                  1,9G            0  1,9G            0% /dev
tmpfs                     1,9G            0  1,9G            0% /dev/shm
tmpfs                     1,9G         8,6M  1,9G            1% /run
tmpfs                     1,9G            0  1,9G            0% /sys/fs/cgroup
/dev/mapper/centos-root   6,2G         1,6G  4,7G           25% /
/dev/sda1                1014M         150M  865M           15% /boot
tmpfs                     379M            0  379M            0% /run/user/1000
[roma2@localhost ~]$ sudo lvextend -L+1G /dev/centos/root
  Size of logical volume centos/root changed from <6,20 GiB (1586 extents) to <7,20 GiB (1842 extents).
  Logical volume centos/root successfully resized.
```
#### 2.5. Check current disk space usage of your root device
```bash
[roma2@localhost ~]$ sudo lvdisplay
  --- Logical volume ---
  LV Path                /dev/centos/swap
  LV Name                swap
  VG Name                centos
  LV UUID                ysa3qr-0B69-2Fi8-25Bc-Lmn3-B6wv-dgXNql
  LV Write Access        read/write
  LV Creation host, time localhost, 2021-11-28 08:26:13 -0500
  LV Status              available
  # open                 2
  LV Size                820,00 MiB
  Current LE             205
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:1

  --- Logical volume ---
  LV Path                /dev/centos/root
  LV Name                root
  VG Name                centos
  LV UUID                KRLUM7-Dxzu-JAbr-WT6Q-hUdo-rum9-QzYdVL
  LV Write Access        read/write
  LV Creation host, time localhost, 2021-11-28 08:26:13 -0500
  LV Status              available
  # open                 1
  LV Size                <7,20 GiB
  Current LE             1842
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
```
#### 2.6. Extend your root device filesystem to be able to use additional free space of root LV
```bash
[roma2@localhost ~]$ sudo xfs_growfs /dev/centos/root
meta-data=/dev/mapper/centos-root isize=512    agcount=4, agsize=406016 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0 spinodes=0
data     =                       bsize=4096   blocks=1624064, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal               bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 1624064 to 1886208
[roma2@localhost ~]$ df -h
Файловая система        Размер Использовано  Дост Использовано% Cмонтировано в
devtmpfs                  1,9G            0  1,9G            0% /dev
tmpfs                     1,9G            0  1,9G            0% /dev/shm
tmpfs                     1,9G         8,6M  1,9G            1% /run
tmpfs                     1,9G            0  1,9G            0% /sys/fs/cgroup
/dev/mapper/centos-root   7,2G         1,6G  5,7G           22% /
/dev/sda1                1014M         150M  865M           15% /boot
tmpfs                     379M            0  379M            0% /run/user/1000
```
#### 2.7. Verify that after reboot your root device is still 1GB bigger than at 2.5.
```bash
[roma2@localhost ~]$ reboot
[roma2@localhost ~]$ df -h
Файловая система        Размер Использовано  Дост Использовано% Cмонтировано в
devtmpfs                  1,9G            0  1,9G            0% /dev
tmpfs                     1,9G            0  1,9G            0% /dev/shm
tmpfs                     1,9G         8,6M  1,9G            1% /run
tmpfs                     1,9G            0  1,9G            0% /sys/fs/cgroup
/dev/mapper/centos-root   7,2G         1,6G  5,7G           22% /
/dev/sda1                1014M         150M  865M           15% /boot
tmpfs                     379M            0  379M            0% /run/user/1000
```
