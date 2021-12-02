# Homework 1
## ex 1
```bash
[roma2@localhost ~]$ ls -a /usr/share/man/man?/*config*
/usr/share/man/man1/pkg-config.1.gz
/usr/share/man/man5/config.5ssl.gz
/usr/share/man/man5/config-util.5.gz
/usr/share/man/man5/selinux_config.5.gz
/usr/share/man/man5/ssh_config.5.gz
/usr/share/man/man5/sshd_config.5.gz
/usr/share/man/man5/x509v3_config.5ssl.gz
/usr/share/man/man8/authconfig.8.gz
/usr/share/man/man8/authconfig-tui.8.gz
/usr/share/man/man8/chkconfig.8.gz
/usr/share/man/man8/grub2-mkconfig.8.gz
/usr/share/man/man8/iprconfig.8.gz
/usr/share/man/man8/lvm-config.8.gz
/usr/share/man/man8/lvmconfig.8.gz
/usr/share/man/man8/lvm-dumpconfig.8.gz
/usr/share/man/man8/sg_get_config.8.gz
/usr/share/man/man8/sys-unconfig.8.gz

[roma2@localhost ~]$ ls -a /usr/share/man/man1/*system* /usr/share/man/man7/*system*
/usr/share/man/man1/systemctl.1.gz
/usr/share/man/man1/systemd.1.gz
/usr/share/man/man1/systemd-analyze.1.gz
/usr/share/man/man1/systemd-ask-password.1.gz
/usr/share/man/man1/systemd-bootchart.1.gz
/usr/share/man/man1/systemd-cat.1.gz
/usr/share/man/man1/systemd-cgls.1.gz
/usr/share/man/man1/systemd-cgtop.1.gz
/usr/share/man/man1/systemd-delta.1.gz
/usr/share/man/man1/systemd-detect-virt.1.gz
/usr/share/man/man1/systemd-escape.1.gz
/usr/share/man/man1/systemd-firstboot.1.gz
/usr/share/man/man1/systemd-firstboot.service.1.gz
/usr/share/man/man1/systemd-inhibit.1.gz
/usr/share/man/man1/systemd-machine-id-commit.1.gz
/usr/share/man/man1/systemd-machine-id-setup.1.gz
/usr/share/man/man1/systemd-notify.1.gz
/usr/share/man/man1/systemd-nspawn.1.gz
/usr/share/man/man1/systemd-path.1.gz
/usr/share/man/man1/systemd-run.1.gz
/usr/share/man/man1/systemd-tty-ask-password-agent.1.gz
/usr/share/man/man7/lvmsystemid.7.gz
/usr/share/man/man7/systemd.directives.7.gz
/usr/share/man/man7/systemd.generator.7.gz
/usr/share/man/man7/systemd.index.7.gz
/usr/share/man/man7/systemd.journal-fields.7.gz
/usr/share/man/man7/systemd.special.7.gz
/usr/share/man/man7/systemd.time.7.gz
```
## ex 2
```bash
[roma2@localhost ~]$ find /usr/share/man -type f -name "*help*"
/usr/share/man/man1/help.1.gz
/usr/share/man/man5/firewalld.helper.5.gz
/usr/share/man/man8/mkhomedir_helper.8.gz
/usr/share/man/man8/pwhistory_helper.8.gz
/usr/share/man/man8/ssh-pkcs11-helper.8.gz

[roma2@localhost ~]$ find /usr/share/man -type f -name "conf*"
/usr/share/man/man5/config.5ssl.gz
/usr/share/man/man5/config-util.5.gz

[roma2@localhost /]$ ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
[roma2@localhost /]$ touch Roman.txt
[roma2@localhost /]$ ls
bin   dev  home  lib64  mnt  proc       root  sbin  sys  usr
boot  etc  lib   media  opt  Roman.txt  run   srv   tmp  var
[roma2@localhost /]$ find . -name "Roman.txt" -exec rm -rf '{}' \; #-exec rm -rf is used not to be prompted to confirm deletion
[roma2@localhost /]$ ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
```
## ex 3
```bash
[roma2@localhost /]$ head -7 /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1

[roma2@localhost /]$ tail -2 /etc/fstab
UUID=02aacf73-7c63-43af-8273-8d9d5d1604f7 /boot                   xfs     defaults        0 0
/dev/mapper/centos-swap swap                    swap    defaults        0 0

[roma2@localhost /]$ head -500 /etc/yum.conf | wc -l
26
```
## ex 4
```bash
[roma2@localhost /]$ touch file_name{1..3}.md

[roma2@localhost /]$ ls
bin   etc            file_name3.md  lib64  opt   run   sys  var
boot  file_name1.md  home           media  proc  sbin  tmp
dev   file_name2.md  lib            mnt    root  srv   usr

[roma2@localhost /]$ mv file_name1{.md,.textdoc}
[roma2@localhost /]$ mv file_name2{.md,}
[roma2@localhost /]$ mv file_name3.md{,.latest}
[roma2@localhost /]$ mv filename1.{textdoc, txt}

[roma2@localhost /]$ ls
bin   etc             file_name3.md.latest  lib64  opt   run   sys  var
boot  file_name1.txt  home                  media  proc  sbin  tmp
dev   file_name2      lib                   mnt    root  srv   usr
```
## ex 5
```bash
[roma2@localhost /]$ cd /mnt

[roma2@localhost mnt]$ cd /home/roma2
[roma2@localhost mnt]$ cd ../home/roma2
[roma2@localhost mnt]$ cd ~
[roma2@localhost mnt]$ cd ~roma2
[roma2@localhost mnt]$ cd
[roma2@localhost mnt]$ cd -
```
## ex 6
```bash
[roma2@localhost ~]$ mkdir -p new in-process/tread{0..2} processed
[roma2@localhost ~]$ ls
in-process  new  processed
[roma2@localhost ~]$ cd in-process/
[roma2@localhost in-process]$ ls
tread0  tread1  tread2
[roma2@localhost ~]$ tree
├── in-process
│   ├── tread0
│   ├── tread1
│   └── tread2
├── new
└── processed
6 directories, 0 files
[roma2@localhost ~]$ touch new/data{00..99}

[roma2@localhost ~]$ cp new/data{00..33} in-process/tread0
[roma2@localhost ~]$ cp new/data{34..66} in-process/tread1
[roma2@localhost ~]$ cp new/data{67..99} in-process/tread2

[roma2@localhost ~]$ ls in-process/tread{0..2}
in-process/tread0:
data00  data04  data08  data12  data16  data20  data24  data28  data32
data01  data05  data09  data13  data17  data21  data25  data29  data33
data02  data06  data10  data14  data18  data22  data26  data30
data03  data07  data11  data15  data19  data23  data27  data31

in-process/tread1:
data34  data38  data42  data46  data50  data54  data58  data62  data66
data35  data39  data43  data47  data51  data55  data59  data63
data36  data40  data44  data48  data52  data56  data60  data64
data37  data41  data45  data49  data53  data57  data61  data65

in-process/tread2:
data67  data71  data75  data79  data83  data87  data91  data95  data99
data68  data72  data76  data80  data84  data88  data92  data96
data69  data73  data77  data81  data85  data89  data93  data97
data70  data74  data78  data82  data86  data90  data94  data98

[roma2@localhost ~]$ mv in-process/* processed/

[roma2@localhost ~]$ ls in-process/tread{0..2}
in-process/tread0:
data00  data04  data08  data12  data16  data20  data24  data28  data32
data01  data05  data09  data13  data17  data21  data25  data29  data33
data02  data06  data10  data14  data18  data22  data26  data30
data03  data07  data11  data15  data19  data23  data27  data31

in-process/tread1:
data34  data38  data42  data46  data50  data54  data58  data62  data66
data35  data39  data43  data47  data51  data55  data59  data63
data36  data40  data44  data48  data52  data56  data60  data64
data37  data41  data45  data49  data53  data57  data61  data65

in-process/tread2:
data67  data71  data75  data79  data83  data87  data91  data95  data99
data68  data72  data76  data80  data84  data88  data92  data96
data69  data73  data77  data81  data85  data89  data93  data97
data70  data74  data78  data82  data86  data90  data94  data98

#I wrote a bash script:

#!/bin/bash

wc1=$(find /home/roma2/new -type f | wc -l)
wc2=$(find /home/roma2/processed -type f | wc -l)

if [ $wc1 -eq $wc2 ]
	then
		echo "deleting files in new folder"
		rm -r /home/roma2/new/*
fi
```
## ex 7
```bash

[roma2@localhost ~]$ a=1 && b=3 && echo file{$a..$b} | xargs -I@ bash -c 'echo @'
file1 file2 file3
```
