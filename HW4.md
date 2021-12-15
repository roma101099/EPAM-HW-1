# Homework 4
## ex 1
```bash
[roma2@localhost ~]$ sudo groupadd -g 4000 sales
[roma2@localhost ~]$ sudo vi 4_1users.txt
[roma2@localhost ~]$ cat 4_1users.txt
bob::1010:4000:Linuxraining:/home/bob:/bin/bash
alice::1011:4000:Linuxraining:/home/alice:/bin/bash
eve::1012:4000:Linuxraining:/home/eve:/bin/bash
[roma2@localhost ~]$ sudo chmod 0600 4_1users.txt
[roma2@localhost ~]$ sudo newusers 4_1users.txt
[roma2@localhost ~]$ cat /etc/passwd | grep -E "bob|alice|eve"
bob:x:1010:4000:Linuxraining:/home/bob:/bin/bash
alice:x:1011:4000:Linuxraining:/home/alice:/bin/bash
eve:x:1012:4000:Linuxraining:/home/eve:/bin/bash

[roma2@localhost ~]$ id 1010
uid=1010(bob) gid=4000(sales) группы=4000(sales)
[roma2@localhost ~]$ id 1011
uid=1011(alice) gid=4000(sales) группы=4000(sales)
[roma2@localhost ~]$ id 1012
uid=1012(eve) gid=4000(sales) группы=4000(sales)
[roma2@localhost ~]$ passwd bob
[roma2@localhost ~]$ passwd alice
[roma2@localhost ~]$ passwd eve
[roma2@localhost etc]$ cat login.defs | grep "PASS_MAX_DAYS"
#       PASS_MAX_DAYS   Maximum number of days a password may be used.
PASS_MAX_DAYS   99999
[roma2@localhost etc]$ sudo vi login.defs
[roma2@localhost etc]$ cat login.defs | grep "PASS_MAX_DAYS"
#       PASS_MAX_DAYS   Maximum number of days a password may be used.
PASS_MAX_DAYS   30
[roma2@localhost etc]$ sudo chage -E `date -d "90 days" +"%Y-%m-%d"` bob
[roma2@localhost etc]$ sudo chage -E `date -d "90 days" +"%Y-%m-%d"` alice
[roma2@localhost etc]$ sudo chage -E `date -d "90 days" +"%Y-%m-%d"` eve
[roma2@localhost etc]$ sudo chage -M 15 bob
[roma2@localhost etc]$ sudo chage -d 0 bob
[roma2@localhost etc]$ sudo chage -d 0 alice
[roma2@localhost etc]$ sudo chage -d 0 eve
```

## ex 2
```bash
[roma2@localhost etc]$ sudo groupadd students
[roma2@localhost etc]$ sudo useradd -g students glen
[roma2@localhost etc]$ sudo useradd -g students antony
[roma2@localhost etc]$ sudo useradd -g students lesly
[roma2@localhost etc]$ sudo mkdir /home/students
[roma2@localhost etc]$ sudo chown -R :students /home/students
[roma2@localhost etc]$ sudo chmod -R 2770 /home/students
```

## ex 3
```bash
[roma2@localhost etc]$ sudo mkdir /share /share/cases
[roma2@localhost etc]$ sudo touch /share/cases/murders.txt /share/cases/moriarty.txt
[roma2@localhost etc]$ tree /share
/share
└── cases
    ├── moriarty.txt
    └── murders.txt

1 directory, 2 files

[roma2@localhost etc]$ sudo groupadd bakerstreet
[roma2@localhost etc]$ sudo useradd -g bakerstreet holmes
[roma2@localhost etc]$ sudo useradd -g bakerstreet watson
[roma2@localhost etc]$ sudo passwd holmes
[roma2@localhost etc]$ sudo passwd watson

[roma2@localhost etc]$ sudo groupadd scotlandyard
[roma2@localhost etc]$ sudo useradd -g scotlandyard lestrade
[roma2@localhost etc]$ sudo useradd -g scotlandyard gregson
[roma2@localhost etc]$ sudo useradd -g scotlandyard jones
[roma2@localhost etc]$ sudo passwd lestrade
[roma2@localhost etc]$ sudo passwd gregson
[roma2@localhost etc]$ sudo passwd jones

[roma2@localhost etc]$ sudo chown -R :bakerstreet /share/cases
[roma2@localhost etc]$ sudo setfacl -m g:bakerstreet:rwx /share/cases
[roma2@localhost etc]$ sudo setfacl -m g:scotlandyard:rwx /share/cases
[roma2@localhost etc]$ sudo setfacl -m u:jones:r-x /share/cases
[roma2@localhost etc]$ sudo setfacl -m o::--- /share/cases/
[roma2@localhost etc]$ getfacl /share/cases
getfacl: Removing leading '/' from absolute path names
# file: share/cases
# owner: root
# group: bakerstreet
user::rwx
user:jones:r-x
group::r-x
group:bakerstreet:rwx
group:scotlandyard:rwx
mask::rwx
other::---

[roma2@localhost ~]$ su - holmes
[holmes@localhost ~]$ cd /share/cases
[holmes@localhost ~]$ vi moriarty.txt
[holmes@localhost cases]$ cat moriarty.txt
9 3/4

[roma2@localhost ~]$ su - lestrade
[lestrade@localhost ~]$ cd /share/cases/
[lestrade@localhost cases]$ cat moriarty.txt
9 3/4
[lestrade@localhost cases]$vi moriarty.txt
[lestrade@localhost cases]$ cat moriarty.txt
9 3/4 9 3/4

[roma2@localhost ~]$ su - jones
[jones@localhost ~]$ cd /share/cases/
[jones@localhost cases]$ cat moriarty.txt
9 3/4 9 3/4
[jones@localhost cases]$ touch Zoo.txt
touch: cannot touch ‘Zoo.txt’: Permission denied
```
