# Homework 5
# EX1 Processes
## 1. Run a sleep command three times at different intervals
```bash
[roma2@localhost ~]$ sleep 1984 &
[1] 1561
[roma2@localhost ~]$ sleep 2018 &
[2] 1562
[roma2@localhost ~]$ sleep 1999 &
[3] 1563
```
## 2. Send a SIGSTOP signal to all of them in three different ways.
```
[roma2@localhost ~]$ kill -20 1561

[1]+  Stopped                 sleep 1984
[roma2@localhost ~]$ kill -SIGSTOP 2362

[2]+  Stopped                 sleep 2018
[roma2@localhost ~]$ fg %3
sleep 1999
^Z
[3]+  Stopped                 sleep 1999
```

## 3. Check their statuses with a job command
```bash
[roma2@localhost ~]$ jobs
[1]   Stopped                 sleep 1984
[2]-  Stopped                 sleep 2018
[3]+  Stopped                 sleep 1999
```
## 4. Terminate one of them. (Any)
```bash
[roma2@localhost ~]$ kill -18 %1
[roma2@localhost ~]$ kill %1
[roma2@localhost ~]$ jobs
[1]   Завершено      sleep 1984
[2]-  Stopped                 sleep 2018
[3]+  Stopped                 sleep 1999
5. To other send a SIGCONT in two different ways
[roma2@localhost ~]$ kill -SIGCONT %2
[roma2@localhost ~]$ kill -18 1562
[roma2@localhost ~]$ jobs
[2]-  Running                 sleep 2018 &
[3]+  Stopped                 sleep 1999 &
```
## 6. Kill one by PID and the second one by job ID
```bash
[roma2@localhost ~]$ kill 1562
[roma2@localhost ~]$ kill %3
[2]-  Terminated              sleep 2018
[3]+  Terminated              sleep 1000000
```
# EX2 systemd
## 1. Write two daemons: one should be a simple daemon and do sleep 10 after a start and then do echo 1 > /tmp/homework, the second one should be oneshot and do echo 2 > /tmp/homework without any sleep
```bash
[roma2@localhost ~]$ vi 1systemd.sh
[roma2@localhost ~]$ vi 2systemd.sh
[roma2@localhost ~]$ sudo vi /etc/systemd/system/1systemd.service
[roma2@localhost ~]$ cat /etc/systemd/system/1systemd.service
[Uinx]
Description=First daemon
[Service]
ExecStart=/home/roma/1systemd.sh
[Unix]
Description=Second daemon
[Service]
Type=oneshot
ExecStart=/home/roma2/2systemd.sh
```
## 2. Make the second depended on the first one (should start only after the first)
```
[roma2@localhost ~]$ sudo vi /etc/systemd/system/2systemd.service
[roma2@localhost ~]$ cat /etc/systemd/system/2systemd.service
[Unix]
Description=Second daemon
Requires=1systemd.service
After=1systemd.service
[Service]
Type=oneshot
ExecStart=/home/roma2/2systemd.sh
```

## 3. Write a timer for the second one and configure it to run on 01.01.2019 at 00:00
```bash
[roma2@localhost ~]$ sudo vi /etc/systemd/system/2systemd.timer
[roma2@localhost ~]$ cat /etc/systemd/system/2systemd.timer
[Unix]
Description=Timer fo the 2systemd.service
[Service]
OnCalendar=2019-01-01 00:00
Persistent=true
```
## 4. Start all daemons and timer, check their statuses, timer list and /tmp/homework
```bash
[roma2@localhost ~]$ sudo systemctl start 1systemd.service
[roma2@localhost ~]$ sudo systemctl start 2systemd.service
[roma2@localhost ~]$ sudo systemctl start 2systemd.timer
[roma2@localhost ~]$ sudo systemctl status 1systemd.service
   1systemd.service
   Loaded: loaded (/etc/systemd/system/1systemd.service; static; vendor preset: disabled)
   Active: inactive (dead)

Dec 17  23:12:23 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:12:23 localhost.localdomain systemd[1]: Started 1systemd.service.
Dec 17  23:15:25 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:16:59 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:16:59 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:16:59 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:18:24 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Dec 17  23:18:24 localhost.localdomain systemd[1]: Started 1systemd.service.
Dec 17  23:18:49 localhost.localdomain systemd[1]: [/etc/systemd/system/1systemd.service:1] Unknown section 'Unix'. ...ing.
Hint: Some lines were ellipsized, use -l to show in full.

[roma2@localhost ~]$ sudo systemctl status 2systemd.service
● 2systemd.service
   Loaded: loaded (/etc/systemd/system/2systemd.service; static; vendor preset: disabled)
   Active: inactive (dead)

Dec 17  23:14:52 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:17:16 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:17:16 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:17:19 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:17:19 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:17:19 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:18:31 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Dec 17  23:18:31 localhost.localdomain systemd[1]: Starting 2systemd.service...
Dec 17  23:18:31 localhost.localdomain systemd[1]: Started 2systemd.service.
Dec 17  23:18:35 localhost.localdomain systemd[1]: [/etc/systemd/system/2systemd.service:1] Unknown section 'Unix'....ing.
Hint: Some lines were ellipsized, use -l to show in full.

[roma2@localhost ~]$ sudo systemctl status 2systemd.timer
● 2systemd.timer
   Loaded: loaded (/etc/systemd/system/2systemd.timer; static; vendor preset: disabled)
   Active: active (elapsed) since Fri 2021-12-17  23:18:35 MSK; 26s ago

Dec 17  23:18:35 localhost.localdomain systemd[1]: Started 2systemd.timer.
[roma2@localhost ~]$ sudo systemctl list-timers --all
NEXT                         LEFT     LAST                         PASSED       UNIT                         ACTIVATES
n/a                          n/a      Fri 2021-12-17  23:14:52 MSK  4min 52s ago 2systemd.timer                2systemd.ser
Fri 2021-12-17 23:04:29 MSK  23h left Fri 2021-12-17  23:04:29 MSK  15min ago    systemd-tmpfiles-clean.timer systemd-tmp
n/a                          n/a      n/a                          n/a          systemd-readahead-done.timer systemd-rea

3 timers listed.

[1]+  Stopped                 sudo systemctl list-timers --all

[roma2@localhost ~]$ cat /tmp/homework
1

```
## 5. Stop all daemons and timer
```bash
[roma2@localhost ~]$ sudo systemctl stop 1systemd.service
[roma2@localhost ~]$ sudo systemctl stop 2systemd.service
Warning: Stopping 2systemd.service, but it can still be activated by:
  2systemd.timer
[roma2@localhost ~]$ sudo systemctl stop 2systemd.timer
```

# EX3 cron/anacron
## 1. Create an anacron job which executes a script with echo Hello > /opt/hello and runs every 2 days
bash ```
[roma2@localhost ~]$ vi hello.sh
[roma2@localhost ~]$ cat hello.sh
#!/bin/bash

echo Hello > /opt/hello

[roma2@localhost ~]$ sudo grep -i hello.anacron /etc/anacrontab
2       0       hello.anacron           /bin/bash /home/roma2/hello.sh

```

## 2. Create a cron job which executes the same command (will be better to create a script for this) and runs it in 1 minute after system boot.
bash ```
[roma2@localhost ~]$ sudo crontab -e
@reboot root sleep 60 && /home/roma2/hello.sh
```

## 3. Restart your virtual machine and check previous job proper execution
```bash
[roma2@localhost ~]$ sudo shutdown
[root@localhost opt]# cat /opt/hello
Hello
```

# EX4 lsof
## 1. Run a sleep command, redirect stdout and stderr into two different files (both of them will be empty).
bash ```
[roma2@localhost ~]$ sleep 1984 1>output 2>errors &
[1] 1546

```

## 2. Find with the lsof command which files this process uses, also find from which file it gain stdin.
bash ```
[roma2@localhost ~]$ lsof -p 1546
COMMAND  PID  USER   FD   TYPE DEVICE  SIZE/OFF     NODE NAME
sleep   1546 roma2  cwd    DIR  253,0      4096  5094868 /home/roma2
sleep   1546 roma2  rtd    DIR  253,0      4096       64 /
sleep   1546 roma2  txt    REG  253,0     33128 13009620 /usr/bin/sleep
sleep   1546 roma2  mem    REG  253,0 106172832 12584427 /usr/lib/locale/locale-archive
sleep   1546 roma2  mem    REG  253,0   2156272    34873 /usr/lib64/libc-2.17.so
sleep   1546 roma2  mem    REG  253,0    163312    34866 /usr/lib64/ld-2.17.so
sleep   1546 roma2    0u   CHR  136,0       0t0        3 /dev/pts/0
sleep   1546 roma2    1w   REG  253,0         0  5094874 /home/roma2/output
sleep   1546 roma2    2w   REG  253,0         0  4205931 /home/roma2/errors
```

## 3. List all ESTABLISHED TCP connections ONLY with lsof
```bash
lsof -i TCP -s TCP:ESTABLISHED
```
