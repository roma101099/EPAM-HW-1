# Homework

## Repositories and Packages

#### 1. Download sysstat package.

```bash
[roma2@localhost ~]$ wget http://mirror.centos.org/centos/7/os/x86_64/Packages/sysstat-10.1.5-19.el7.x86_64.rpm
--2021-12-25 14:10:41--  http://mirror.centos.org/centos/7/os/x86_64/Packages/sysstat-10.1.5-19.el7.x86_64.rpm
Распознаётся mirror.centos.org (mirror.centos.org)... 141.105.67.224, 2a10:5fc0:0:1::5
Подключение к mirror.centos.org (mirror.centos.org)|141.105.67.224|:80... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа... 200 OK
Длина: 323020 (315K) [application/x-rpm]
Сохранение в: «sysstat-10.1.5-19.el7.x86_64.rpm»

100%[==================================>] 323 020     --.-K/s   за 0,09s

2021-12-25 14:10:42 (3,34 MB/s) - «sysstat-10.1.5-19.el7.x86_64.rpm» сохранён [323020/323020]```

#### 2. Get information from downloaded sysstat package file.

```bash
[roma2@localhost ~]$ sudo rpm -qip sysstat-10.1.5-19.el7.x86_64.rpm
[sudo] пароль для roma2:
Name        : sysstat
Version     : 10.1.5
Release     : 19.el7
Architecture: x86_64
Install Date: (not installed)
Group       : Applications/System
Size        : 1172488
License     : GPLv2+
Signature   : RSA/SHA256, Пт 03 апр 2020 17:08:48, Key ID 24c6a8a7f4a80eb5
Source RPM  : sysstat-10.1.5-19.el7.src.rpm
Build Date  : Ср 01 апр 2020 00:36:37
Build Host  : x86-01.bsys.centos.org
Relocations : (not relocatable)
Packager    : CentOS BuildSystem <http://bugs.centos.org>
Vendor      : CentOS
URL         : http://sebastien.godard.pagesperso-orange.fr/
Summary     : Collection of performance monitoring tools for Linux
Description :
The sysstat package contains sar, sadf, mpstat, iostat, pidstat, nfsiostat-sysstat,
tapestat, cifsiostat and sa tools for Linux.
The sar command collects and reports system activity information. This
information can be saved in a file in a binary format for future inspection. The
statistics reported by sar concern I/O transfer rates, paging activity,
process-related activities, interrupts, network activity, memory and swap space
utilization, CPU utilization, kernel activities and TTY statistics, among
others. Both UP and SMP machines are fully supported.
The sadf command may be used to display data collected by sar in various formats
(CSV, XML, etc.).
The iostat command reports CPU utilization and I/O statistics for disks.
The tapestat command reports statistics for tapes connected to the system.
The mpstat command reports global and per-processor statistics.
The pidstat command reports statistics for Linux tasks (processes).
The nfsiostat-sysstat command reports I/O statistics for network file systems.
The cifsiostat command reports I/O statistics for CIFS file systems.
```

#### 3. Install sysstat package and get information about files installed by this package.

```bash
[roma2@localhost ~]$ sudo yum -y install sysstat
Загружены модули: fastestmirror
Determining fastest mirrors
 * base: mirror.docker.ru
 * extras: mirror.docker.ru
 * updates: mirror.docker.ru
base                                                 | 3.6 kB     00:00
extras                                               | 2.9 kB     00:00
updates                                              | 2.9 kB     00:00
updates/7/x86_64/primary_db                            |  13 MB   00:03
Разрешение зависимостей
--> Проверка сценария
---> Пакет sysstat.x86_64 0:10.1.5-19.el7 помечен для установки
--> Обработка зависимостей: libsensors.so.4()(64bit) пакета: sysstat-10.1.5-19.el7.x86_64
--> Проверка сценария
---> Пакет lm_sensors-libs.x86_64 0:3.4.0-8.20160601gitf9185e5.el7 помечен для установки
--> Проверка зависимостей окончена

Зависимости определены

============================================================================
 Package           Архитектура
                            Версия                             Репозиторий
                                                                      Размер
============================================================================
Установка:
 sysstat           x86_64   10.1.5-19.el7                      base   315 k
Установка зависимостей:
 lm_sensors-libs   x86_64   3.4.0-8.20160601gitf9185e5.el7     base    42 k

Итого за операцию
============================================================================
Установить  1 пакет (+1 зависимый)

Объем загрузки: 357 k
Объем изменений: 1.2 M
Downloading packages:
(1/2): lm_sensors-libs-3.4.0-8.20160601gitf9185e5.el7. |  42 kB   00:00
(2/2): sysstat-10.1.5-19.el7.x86_64.rpm                | 315 kB   00:00
----------------------------------------------------------------------------
Общий размер                                   829 kB/s | 357 kB  00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Установка   : lm_sensors-libs-3.4.0-8.20160601gitf9185e5.el7.x86_64   1/2
  Установка   : sysstat-10.1.5-19.el7.x86_64                            2/2
  Проверка    : sysstat-10.1.5-19.el7.x86_64                            1/2
  Проверка    : lm_sensors-libs-3.4.0-8.20160601gitf9185e5.el7.x86_64   2/2

Установлено:
  sysstat.x86_64 0:10.1.5-19.el7

Установлены зависимости:
  lm_sensors-libs.x86_64 0:3.4.0-8.20160601gitf9185e5.el7

Выполнено!
```

#### verifying sysstat installation

```bash
[roma2@localhost ~]$ mpstat -V
sysstat, версия 10.1.5
(C) Sebastien Godard (sysstat <at> orange.fr)
```

#### - Add NGINX repository (need to find repository config on https://www.nginx.com/) and complete the following tasks using yum:

```bash
[roma2@localhost ~]$ sudo yum install yum-utils
Загружены модули: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.docker.ru
 * extras: mirror.docker.ru
 * updates: mirror.docker.ru
Разрешение зависимостей
--> Проверка сценария
---> Пакет yum-utils.noarch 0:1.1.31-54.el7_8 помечен для установки
--> Обработка зависимостей: python-kitchen пакета: yum-utils-1.1.31-54.el7_8.noarch
--> Обработка зависимостей: libxml2-python пакета: yum-utils-1.1.31-54.el7_8.noarch
--> Проверка сценария
---> Пакет libxml2-python.x86_64 0:2.9.1-6.el7_9.6 помечен для установки
--> Обработка зависимостей: libxml2 = 2.9.1-6.el7_9.6 пакета: libxml2-python-2.9.1-6.el7_9.6.x86_64
---> Пакет python-kitchen.noarch 0:1.1.1-5.el7 помечен для установки
--> Обработка зависимостей: python-chardet пакета: python-kitchen-1.1.1-5.el7.noarch
--> Проверка сценария
---> Пакет libxml2.x86_64 0:2.9.1-6.el7.5 помечен для обновления
---> Пакет libxml2.x86_64 0:2.9.1-6.el7_9.6 помечен как обновление
---> Пакет python-chardet.noarch 0:2.2.1-3.el7 помечен для установки
--> Проверка зависимостей окончена

Зависимости определены

============================================================================
 Package             Архитектура Версия                  Репозиторий  Размер
============================================================================
Установка:
 yum-utils           noarch      1.1.31-54.el7_8         base         122 k
Установка зависимостей:
 libxml2-python      x86_64      2.9.1-6.el7_9.6         updates      247 k
 python-chardet      noarch      2.2.1-3.el7             base         227 k
 python-kitchen      noarch      1.1.1-5.el7             base         267 k
Обновление зависимостей:
 libxml2             x86_64      2.9.1-6.el7_9.6         updates      668 k

Итого за операцию
============================================================================
Установить  1 пакет   (+3 зависимых)
Обновить              ( 1 зависимый)

Объем загрузки: 1.5 M
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/5): python-chardet-2.2.1-3.el7.noarch.rpm           | 227 kB   00:00
(2/5): libxml2-python-2.9.1-6.el7_9.6.x86_64.rpm       | 247 kB   00:00
(3/5): python-kitchen-1.1.1-5.el7.noarch.rpm           | 267 kB   00:00
(4/5): yum-utils-1.1.31-54.el7_8.noarch.rpm            | 122 kB   00:00
(5/5): libxml2-2.9.1-6.el7_9.6.x86_64.rpm              | 668 kB   00:00
----------------------------------------------------------------------------
Общий размер                                   1.7 MB/s | 1.5 MB  00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Обновление  : libxml2-2.9.1-6.el7_9.6.x86_64                          1/6
  Установка   : libxml2-python-2.9.1-6.el7_9.6.x86_64                   2/6
  Установка   : python-chardet-2.2.1-3.el7.noarch                       3/6
  Установка   : python-kitchen-1.1.1-5.el7.noarch                       4/6
  Установка   : yum-utils-1.1.31-54.el7_8.noarch                        5/6
  Очистка     : libxml2-2.9.1-6.el7.5.x86_64                            6/6
  Проверка    : python-chardet-2.2.1-3.el7.noarch                       1/6
  Проверка    : libxml2-2.9.1-6.el7_9.6.x86_64                          2/6
  Проверка    : libxml2-python-2.9.1-6.el7_9.6.x86_64                   3/6
  Проверка    : python-kitchen-1.1.1-5.el7.noarch                       4/6
  Проверка    : yum-utils-1.1.31-54.el7_8.noarch                        5/6
  Проверка    : libxml2-2.9.1-6.el7.5.x86_64                            6/6

Установлено:
  yum-utils.noarch 0:1.1.31-54.el7_8

Установлены зависимости:
  libxml2-python.x86_64 0:2.9.1-6.el7_9.6
  python-chardet.noarch 0:2.2.1-3.el7
  python-kitchen.noarch 0:1.1.1-5.el7

Обновлены зависимости:
  libxml2.x86_64 0:2.9.1-6.el7_9.6

Выполнено!
[roma2@localhost ~]$ sudo vi /etc/yum.repos.d/nginx.repo
[roma2@localhost ~]$ cat /etc/yum.repos.d/nginx.repo
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=1
enabled=0
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
[roma2@localhost ~]$ sudo yum-config-manager --enable nginx-mainline
```

#### 1. Check if NGINX repository enabled or not.

```bash
[roma2@localhost ~]$ yum repolist
Загружены модули: fastestmirror
Determining fastest mirrors
 * base: mirrors.datahouse.ru
 * extras: mirror.docker.ru
 * updates: centos-mirror.rbc.ru
nginx-mainline                                       | 2.9 kB     00:00
nginx-stable                                         | 2.9 kB     00:00
(1/2): nginx-stable/7/x86_64/primary_db                |  70 kB   00:00
(2/2): nginx-mainline/7/x86_64/primary_db              | 227 kB   00:00
Идентификатор репозитория           репозиторий                    состояние
base/7/x86_64                       CentOS-7 - Base                10 072
extras/7/x86_64                     CentOS-7 - Extras                 500
nginx-mainline/7/x86_64             nginx mainline repo               875
nginx-stable/7/x86_64               nginx stable repo                 256
updates/7/x86_64                    CentOS-7 - Updates              3 242
repolist: 14 945
```

#### 2. Install NGINX.

```bash
[roma2@localhost ~]$ sudo yum install nginx
.
.
.
Установлено:
  nginx.x86_64 1:1.21.4-1.el7.ngx

Выполнено!

```

#### 3. Check yum history and undo NGINX installation.

```bash
[roma2@localhost ~]$ sudo yum history list
Загружены модули: fastestmirror
ID     | Вход пользователя        | Дата и время     | Действия       | Изменен
-------------------------------------------------------------------------------
     7 | roma2 <roma2>            | 2021-12-25 14:22 | Install        |    1 EE
     6 | roma2 <roma2>            | 2021-12-25 14:17 | I, U           |    5

     5 | roma2 <roma2>            | 2021-12-25 14:14 | Install        |    2

     4 | roma2 <roma2>            | 2021-12-18 15:11 | Install        |    1

     3 | roma2 <roma2>            | 2021-12-10 08:26 | Install        |    1

     2 | roma2 <roma2>            | 2021-11-28 17:03 | Install        |    1

     1 | Система <unset>          | 2021-11-28 08:26 | Install        |  304

history list
[roma2@localhost ~]$ sudo yum history package-info nginx
Загружены модули: fastestmirror
Код операции   : 7
Время начала   : Sat Dec 25 14:22:37 2021
Пакет        : nginx-1:1.21.4-1.el7.ngx.x86_64
Состояние      : Установить
Размер           : 2 908 779
Узел сборки    : ip-10-1-17-68.eu-central-1.compute.internal
Время сборки   : Tue Nov  2 11:06:33 2021
Поставщик      : NGINX Packaging <nginx-packaging@f5.com>
Лицензия        : 2-clause BSD-like license
URL            : https://nginx.org/
Исходный RPM     : nginx-1.21.4-1.el7.ngx.src.rpm
Получено       : Tue Nov  2 08:00:00 2021
Отправитель    : Konstantin Pavlov <thresh@nginx.com>
Причина         : user
Команда: install nginx
Репозиторий    : nginx-mainline
Установлен   : roma2 <roma2>
history package-info
```

#### 4. Disable NGINX repository.

```bash
[roma2@localhost ~]$ sudo yum-config-manager --disable repository nginx-mainline
Загружены модули: fastestmirror
=========================== repo: nginx-mainline ===========================
[nginx-mainline]
async = True
bandwidth = 0
base_persistdir = /var/lib/yum/repos/x86_64/7
baseurl = http://nginx.org/packages/mainline/centos/7/x86_64/
cache = 0
cachedir = /var/cache/yum/x86_64/7/nginx-mainline
check_config_file_age = True
compare_providers_priority = 80
cost = 1000
deltarpm_metadata_percentage = 100
deltarpm_percentage =
enabled = 0
enablegroups = True
exclude =
failovermethod = priority
ftp_disable_epsv = False
gpgcadir = /var/lib/yum/repos/x86_64/7/nginx-mainline/gpgcadir
gpgcakey =
gpgcheck = True
gpgdir = /var/lib/yum/repos/x86_64/7/nginx-mainline/gpgdir
gpgkey = https://nginx.org/keys/nginx_signing.key
hdrdir = /var/cache/yum/x86_64/7/nginx-mainline/headers
http_caching = all
includepkgs =
ip_resolve =
keepalive = True
keepcache = False
mddownloadpolicy = sqlite
mdpolicy = group:small
mediaid =
metadata_expire = 21600
metadata_expire_filter = read-only:present
metalink =
minrate = 0
mirrorlist =
mirrorlist_expire = 86400
name = nginx mainline repo
old_base_cache_dir =
password =
persistdir = /var/lib/yum/repos/x86_64/7/nginx-mainline
pkgdir = /var/cache/yum/x86_64/7/nginx-mainline/packages
proxy = False
proxy_dict =
proxy_password =
proxy_username =
repo_gpgcheck = False
retries = 10
skip_if_unavailable = False
ssl_check_cert_permissions = True
sslcacert =
sslclientcert =
sslclientkey =
sslverify = True
throttle = 0
timeout = 30.0
ui_id = nginx-mainline/7/x86_64
ui_repoid_vars = releasever,
   basearch
username =

```

#### 5. Remove sysstat package installed in the first task.

```bash
[roma2@localhost ~]$ sudo yum remove sysstat
Загружены модули: fastestmirror
Разрешение зависимостей
--> Проверка сценария
---> Пакет sysstat.x86_64 0:10.1.5-19.el7 помечен для удаления
--> Проверка зависимостей окончена

Зависимости определены

============================================================================
 Package         Архитектура    Версия                  Репозиторий   Размер
============================================================================
Удаление:
 sysstat         x86_64         10.1.5-19.el7           @base         1.1 M

Итого за операцию
============================================================================
Удалить  1 пакет

Объем изменений: 1.1 M
Продолжить? [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Удаление    : sysstat-10.1.5-19.el7.x86_64                            1/1
  Проверка    : sysstat-10.1.5-19.el7.x86_64                            1/1

Удалено:
  sysstat.x86_64 0:10.1.5-19.el7

Выполнено!
```

#### 6. Install EPEL repository and get information about it.

```bash
[roma2@localhost ~]$ sudo yum -y install epel-release
[roma2@localhost ~]$ sudo yum info epel-release
Загружены модули: fastestmirror
Loading mirror speeds from cached hostfile
epel/x86_64/metalink                                 |  33 kB     00:00
 * base: mirror.docker.ru
 * epel: mirror.yandex.ru
 * extras: mirror.docker.ru
 * updates: mirror.docker.ru
epel                                                 | 4.7 kB     00:00
(1/3): epel/x86_64/group_gz                            |  96 kB   00:00
(2/3): epel/x86_64/updateinfo                          | 1.0 MB   00:00
(3/3): epel/x86_64/primary_db                          | 7.0 MB   00:02
Установленные пакеты
Название: epel-release
Архитектура: noarch
Версия: 7
Выпуск: 11
Объем: 24 k
Источник: installed
Из источника: extras
Аннотация: Extra Packages for Enterprise Linux repository configuration
Ссылка: http://download.fedoraproject.org/pub/epel
Лицензия: GPLv2
Описание: This package contains the Extra Packages for Enterprise Linux
        : (EPEL) repository GPG key as well as configuration for yum.

Доступные пакеты
Название: epel-release
Архитектура: noarch
Версия: 7
Выпуск: 14
Объем: 15 k
Источник: epel/x86_64
Аннотация: Extra Packages for Enterprise Linux repository configuration
Ссылка: http://download.fedoraproject.org/pub/epel
Лицензия: GPLv2
Описание: This package contains the Extra Packages for Enterprise Linux
        : (EPEL) repository GPG key as well as configuration for yum.
```

#### 7. Find how much packages provided exactly by EPEL repository.
(first five lines of output contented unnecessary output)
```bash
[roma2@localhost ~]$ sudo yum --disablerepo="*" --enablerepo="epel" list available | tail -n +5 | wc -l
13917
```

#### 8. Install ncdu package from EPEL repo.

```bash
Установлено:
  ncdu.x86_64 0:1.16-1.el7

Выполнено!
[roma2@localhost ~]$ sudo yum --enablerepo="epel" install ncdu
```

## Work with files

#### 1. Find all regular files below 100 bytes inside your home directory.

```bash
[roma2@localhost ~]$ sudo find ~/ -size -100b -type f
/home/roma2/.bash_logout
/home/roma2/.bash_profile
/home/roma2/.bashrc
/home/roma2/.bash_history
/home/roma2/new/data00
/home/roma2/new/data01
.
.
.
```

#### 2. Find an inode number and a hard links count for the root directory. The hard link count should be about 17. Why?

```bash
[roma2@localhost ~]$ stat /
  Файл: «/»
  Размер: 4096          Блоков: 8          Блок В/В: 4096   каталог
Устройство: fd00h/64768d        Inode: 64          Ссылки: 18
Доступ: (0555/dr-xr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Контекст: system_u:object_r:root_t:s0
Доступ: 2021-12-25 14:07:49.023000000 -0500
Модифицирован: 2021-12-13 16:58:50.862531892 -0500
Изменён: 2021-12-13 16:58:50.862531892 -0500
 Создан: -
```

##### As 17 directories are used by default, the hard link count should be about this number

#### 3. Check what inode numbers have "/" and "/boot" directory. Why?

```bash
[roma2@localhost ~]$ stat /
  Файл: «/»
  Размер: 4096          Блоков: 8          Блок В/В: 4096   каталог
Устройство: fd00h/64768d        Inode: 64          Ссылки: 18
Доступ: (0555/dr-xr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Контекст: system_u:object_r:root_t:s0
Доступ: 2021-12-25 14:07:49.023000000 -0500
Модифицирован: 2021-12-13 16:58:50.862531892 -0500
Изменён: 2021-12-13 16:58:50.862531892 -0500
 Создан: -
[roma2@localhost ~]$ stat /boot
  Файл: «/boot»
  Размер: 4096          Блоков: 8          Блок В/В: 4096   каталог
Устройство: 801h/2049d  Inode: 64          Ссылки: 5
Доступ: (0555/dr-xr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Контекст: system_u:object_r:boot_t:s0
Доступ: 2021-12-25 14:14:40.519543158 -0500
Модифицирован: 2021-11-28 08:40:49.900911958 -0500
Изменён: 2021-11-28 08:40:49.900911958 -0500
 Создан: -
```
##### /boot is a different file system of the same type (xfs), and it's the root directory of this file system, so it's very likely that it uses the same inode number as /.

#### 4. Check the root directory space usage by du command. Compare it with an information from df. If you find differences, try to find out why it happens.

```bash
[roma2@localhost ~]$ df -h
Файловая система        Размер Использовано  Дост Использовано% Cмонтировано в
devtmpfs                  1,9G            0  1,9G            0% /dev
tmpfs                     1,9G            0  1,9G            0% /dev/shm
tmpfs                     1,9G         8,6M  1,9G            1% /run
tmpfs                     1,9G            0  1,9G            0% /sys/fs/cgroup
/dev/mapper/centos-root   6,2G         1,6G  4,7G           25% /
/dev/sda1                1014M         150M  865M           15% /boot
tmpfs                     379M            0  379M            0% /run/user/10
[roma2@localhost ~]$ sudo du -hcs /
[sudo] пароль для roma2:
du: невозможно получить доступ к «/proc/1/task/1/fd/46»: Нет такого файла или каталога
du: невозможно получить доступ к «/proc/2220/task/2220/fd/4»: Нет такого файла или каталога
du: невозможно получить доступ к «/proc/2220/task/2220/fdinfo/4»: Нет такого файла или каталога
du: невозможно получить доступ к «/proc/2220/fd/3»: Нет такого файла или каталога
du: невозможно получить доступ к «/proc/2220/fdinfo/3»: Нет такого файла или каталога
1,7G    /
1,7G    итого
```
##### As boot directory is just a different file system of the same type (xfs), it's logical that it can use the same inode number as /directory.

#### 5. Check disk space usage of /var/log directory using ncdu

```bash
[roma2@localhost ~]$ ncdu -x /var/log
 Total disk usage:   4,2 MiB  Apparent size:   4,5 MiB  Items: 59       
``` 
