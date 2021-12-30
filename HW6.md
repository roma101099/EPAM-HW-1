# Homework 6
# Task 1:
## 1.1. SSH to remotehost using username and password provided to you in Slack. Log out from remotehost.
```bash
[roma2@localhost .ssh]$ ssh Roman_Sokolovskiy@18.221.144.175
The authenticity of host '18.221.144.175 (18.221.144.175)' can't be established.
ECDSA key fingerprint is SHA256:Lqk214fPCrlvcsnoj1NGVS+Puxr7lGuEncIdALeLt78.
ECDSA key fingerprint is MD5:01:a1:c8:32:41:5c:9b:4b:0a:cc:f0:4b:7e:66:2b:38.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '18.221.144.175' (ECDSA) to the list of known hosts.
Roman_Sokolovskiy@18.221.144.175's password:
Last login: Thu Dec 23 18:57:58 2021 from 95-29-44-156.broadband.corbina.ru

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
[Roman_Sokolovskiy@ip-172-31-33-155 ~]$ logout
Connection to 18.221.144.175 closed.
```
## 1.2. Generate new SSH key-pair on your localhost with name "hw-5" (keys should be created in ~/.ssh folder).
```bash
[roma2@localhost .ssh]$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/roma2/.ssh/id_rsa): hw-5
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in hw-5.
Your public key has been saved in hw-5.pub.
The key fingerprint is:
SHA256:AKii7cW9f5y1Ssv81wOBJ+XGmE25KVMhwF7MjTPpyms roma2@localhost.localdomain
The key's randomart image is:
+---[RSA 2048]----+
|   ..   ..+.+.o  |
|  .  .   . O.*   |
| .    . . o & o  |
|o      . . O X   |
|o. . .  S . * .  |
|. . o .  o  ..   |
| . .   . .oo ... |
|  .   .  E+.. ...|
|       .o.=o..  .|
+----[SHA256]-----+
[roma2@localhost .ssh]$ ls
hw-5  hw-5.pub  known_hosts

```
## 1.3. Set up key-based authentication, so that you can SSH to remotehost without password.

```bash
[roma2@localhost ~]$ ssh-copy-id -i ~/.ssh/hw-5.pub Roman_Sokolovskiy@18.221.
4.175/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/roma2/.ssh/hw-5.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: ERROR: ssh: Could not resolve hostname 18.221.: Name or service not known
[roma2@localhost ~]$ ssh-copy-id -i ~/.ssh/hw-5.pub Roman_Sokolovskiy@18.221.144.175
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/roma2/.ssh/hw-5.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
Roman_Sokolovskiy@18.221.144.175's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'Roman_Sokolovskiy@18.221.144.175'"
and check to make sure that only the key(s) you wanted were added.
```
 
 ## 1.4. SSH to remotehost without password. Log out from remotehost.
```bash
[roma2@localhost ~]$ ssh -i /home/roma2/.ssh/hw-5 Roman_Sokolovskiy@18.221.1
44.175
Enter passphrase for key '/home/roma2/.ssh/hw-5':
Last login: Thu Dec 23 19:33:31 2021 from 95-29-44-156.broadband.corbina.ru

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
[Roman_Sokolovskiy@ip-172-31-33-155 ~]$ logout
Connection to 18.221.144.175 closed.

```
 ## 1.5. Create SSH config file, so that you can SSH to remotehost simply running ssh remotehost command. As a result, provide output of command cat ~/.ssh/config.

```bash
[roma2@localhost .ssh]$ vi config
[roma2@localhost .ssh]$ cat config
Host remotehost
        Hostname 18.221.144.175
        User Roman_Sokolovskiy
        IdentityFile ~/.ssh/hw-5
[roma2@localhost .ssh]$ sudo chmod 644 config
[sudo] пароль для roma2:
[roma2@localhost .ssh]$ ssh remotehost
Enter passphrase for key '/home/roma2/.ssh/hw-5':
Last login: Thu Dec 23 19:41:58 2021 from 95-29-44-156.broadband.corbina.ru

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
```
 ## 1.6. Using command line utility (curl or telnet) verify that there are some webserver running on port 80 of webserver. Notice that webserver has a private network IP, so you can access it only from the same network (when you are on remotehost that runs in the same private network). Log out from remotehost.

```bash
[Roman_Sokolovskiy@ip-172-31-33-155 ~]$ curl 172.31.45.237:80
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"><html><head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
                <title>Apache HTTP Server Test Page powered by CentOS</title>
                <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

    <!-- Bootstrap -->
    <link href="/noindex/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="noindex/css/open-sans.css" type="text/css" />

<style type="text/css"><!--

body {
  font-family: "Open Sans", Helvetica, sans-serif;
  font-weight: 100;
  color: #ccc;
  background: rgba(10, 24, 55, 1);
  font-size: 16px;
}

h2, h3, h4 {
  font-weight: 200;
}

h2 {
  font-size: 28px;
}

.jumbotron {
  margin-bottom: 0;
  color: #333;
  background: rgb(212,212,221); /* Old browsers */
  background: radial-gradient(ellipse at center top, rgba(255,255,255,1) 0%,rgba(174,174,183,1) 100%); /* W3C */
}

.jumbotron h1 {
  font-size: 128px;
  font-weight: 700;
  color: white;
  text-shadow: 0px 2px 0px #abc,
               0px 4px 10px rgba(0,0,0,0.15),
               0px 5px 2px rgba(0,0,0,0.1),
               0px 6px 30px rgba(0,0,0,0.1);
}

.jumbotron p {
  font-size: 28px;
  font-weight: 100;
}

.main {
   background: white;
   color: #234;
   border-top: 1px solid rgba(0,0,0,0.12);
   padding-top: 30px;
   padding-bottom: 40px;
}

.footer {
   border-top: 1px solid rgba(255,255,255,0.2);
   padding-top: 30px;
}

    --></style>
</head>
<body>
  <div class="jumbotron text-center">
    <div class="container">
          <h1>Hello!</h1>
                <p class="lead">You are here because you're probably a DevOps courses member. In that case you should open <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"> THIS LINK </a></p>
                </div>
  </div>
</body></html>
```
## 1.7. Using SSH setup port forwarding, so that you can reach webserver from your localhost (choose any free local port you like).

```bash
[roma2@localhost ~]$ ssh -f -N -L 1984:172.31.45.237:80 remotehost
Enter passphrase for key '/home/roma2/.ssh/hw-5':
``` 
## 1.8 Like in 1.6, but on localhost using command line utility verify that localhost and port you have specified act like webserver, returning same result as in 1.6.

```bash
[roma2@localhost ~]$ curl http://localhost:1984
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"><html><head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
                <title>Apache HTTP Server Test Page powered by CentOS</title>
                <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

    <!-- Bootstrap -->
    <link href="/noindex/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="noindex/css/open-sans.css" type="text/css" />

<style type="text/css"><!--

body {
  font-family: "Open Sans", Helvetica, sans-serif;
  font-weight: 100;
  color: #ccc;
  background: rgba(10, 24, 55, 1);
  font-size: 16px;
}

h2, h3, h4 {
  font-weight: 200;
}

h2 {
  font-size: 28px;
}

.jumbotron {
  margin-bottom: 0;
  color: #333;
  background: rgb(212,212,221); /* Old browsers */
  background: radial-gradient(ellipse at center top, rgba(255,255,255,1) 0%,rgba(174,174,183,1) 100%); /* W3C */
}

.jumbotron h1 {
  font-size: 128px;
  font-weight: 700;
  color: white;
  text-shadow: 0px 2px 0px #abc,
               0px 4px 10px rgba(0,0,0,0.15),
               0px 5px 2px rgba(0,0,0,0.1),
               0px 6px 30px rgba(0,0,0,0.1);
}

.jumbotron p {
  font-size: 28px;
  font-weight: 100;
}

.main {
   background: white;
   color: #234;
   border-top: 1px solid rgba(0,0,0,0.12);
   padding-top: 30px;
   padding-bottom: 40px;
}

.footer {
   border-top: 1px solid rgba(255,255,255,0.2);
   padding-top: 30px;
}

    --></style>
</head>
<body>
  <div class="jumbotron text-center">
    <div class="container">
          <h1>Hello!</h1>
                <p class="lead">You are here because you're probably a DevOps courses member. In that case you should open <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"> THIS LINK </a></p>
                </div>
  </div>
</body></html>
``` 
## Task 2:
## 2.1. Imagine your localhost has been relocated to Havana. Change the time zone on the localhost to Havana and verify the time zone has been changed properly (may be multiple commands).

```bash
[roma2@localhost ~]$ timedatectl list-timezones | grep Havana
America/Havana
[roma2@localhost ~]$ timedatectl list-timezones | grep Havana
America/Havana
[roma2@localhost ~]$ date
Ср дек 22 01:15:22 MSK 2021
[roma2@localhost ~]$ timedatectl set-timezone America/Havana
==== AUTHENTICATING FOR org.freedesktop.timedate1.set-timezone ===
Чтобы настроить часовой пояс, необходимо пройти аутентификацию.
Authenticating as: roma2
Password:
==== AUTHENTICATION COMPLETE ===
[roma2@localhost ~]$ ls -l /etc/localtime
lrwxrwxrwx. 1 root root 36 дек 21 17:16 /etc/localtime -> ../usr/share/zoneinfo/America/Havana
[roma2@localhost ~]$ date
Вт дек 21 17:16:47 CST 2021
[roma2@localhost ~]$ timedatectl status
      Local time: Вт 2021-12-21 17:17:05 CST
  Universal time: Вт 2021-12-21 22:17:05 UTC
        RTC time: Вт 2021-12-21 22:04:48
       Time zone: America/Havana (CST, -0500)
     NTP enabled: yes
NTP synchronized: no
 RTC in local TZ: no
      DST active: no
 Last DST change: DST ended at
                  Вс 2021-11-07 00:59:59 CDT
                  Вс 2021-11-07 00:00:00 CST
 Next DST change: DST begins (the clock jumps one hour forward) at
                  Сб 2022-03-12 23:59:59 CST
                  Вс 2022-03-13 01:00:00 CDT
``` 
## 2.2. Find all systemd journal messages on localhost, that were recorded in the last 50 minutes and originate from a system service started with user id 81 (single command).

```bash

[roma2@localhost ~]$ journalctl _UID=81 --since "50 minutes ago"
-- Logs begin at Вт 2021-12-21 10:33:28 CST, end at Вт 2021-12-21 17:17:05 C
дек 21 17:16:00 localhost.localdomain dbus[652]: [system] Activating via sys
дек 21 17:16:00 localhost.localdomain dbus[652]: [system] Successfully activ
дек 21 17:17:05 localhost.localdomain dbus[652]: [system] Activating via sys
дек 21 17:17:05 localhost.localdomain dbus[652]: [system] Successfully activ
lines 1-5/5 (END)
``` 
## 2.3. Configure rsyslogd by adding a rule to the newly created configuration file /etc/rsyslog.d/auth-errors.conf to log all security and authentication messages with the priority alert and higher to the /var/log/auth-errors file. Test the newly added log directive with the logger command (multiple commands).
```bash

[roma2@localhost rsyslog.d]$ sudo vi auth-errors.conf
[roma2@localhost rsyslog.d]$ service rsyslog restart
Redirecting to /bin/systemctl restart rsyslog.service
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Для управления системными службами и юнитами, необходимо пройти аутентификацию.
Authenticating as: roma2
Password:
==== AUTHENTICATION COMPLETE ===
[roma2@localhost rsyslog.d]$ logger -p authpriv.alert log
[roma2@localhost rsyslog.d]$ tail -5 /var/log/auth-errors
Dec 21 18:12:53 localhost roma2: log
``` 
