# Homework 2
## ex 1
```bash
[roma@localhost ~]$ man awk
[roma@localhost ~]$ man awk | grep -C10 'ENVIRONMENT VARIABLES' | tail -11 > descretion.txt
[roma@localhost ~]$ cat descretion.txt
ENVIRONMENT VARIABLES
       The AWKPATH environment variable can be used to provide a  list  of
       directories that gawk searches when looking for files named via the
       -f and --file options.

       For socket communication, two special environment variables can  be
       used  to control the number of retries (GAWK_SOCK_RETRIES), and the
       interval between retries (GAWK_MSEC_SLEEP).   The  interval  is  in
       milliseconds.  On  systems that do not support usleep(3), the value
       is rounded up to an integral number of seconds.`
```
## ex 2
```bash
#!/bin/bash
path2=`pwd`
cd ..
if [[ ! "$path2" == "$pwd" ]];
        then touch task2.txt
        else > ~/err2.log 2>&1 echo "Error"
fi
```
## ex 2*
```bash
#!/bin/bash

a=$(find ../ -name "task2.txt")
        touch ../task2.txt 2>err.log
b=$(awk '/Permission denied/ {print "Permission denied"}' err.log)

if [[ $a = '../task2.txt' ]];
        then
                echo "The file already exists in a directory"
                        elif [[ $b = 'Permission denied' ]];
                                then echo "Permission denied"
        else
                echo "Done"
fi

```

## ex 3
```bash
[roma@localhost 2.2]$ pwd >road.txt
[roma@localhost 2.2]$ cat road.txt
/home/roma/2.2

#!/bin/bash

a=$(cat road.txt)
ls -R $a
```

## ex 3*
```bash
#!/bin/bash

a="/home/roma/3"
ls -R $a > $a/road.txt
files=$(find "$a" -type f | wc -l )
folders=$(find "$a" -type d | wc -l )

echo "Files: $files" >> $a/road.txt
echo "Folders: $folders" >> $a/road.txt
~    

```
## ex 3**
```bash

#!/bin/bash

a="/home/roma/3"
w=1
while [ -n "$1" ]
do
echo "Number $w = $1" >> $a/road.txt
w=$[ $w + 1 ]
shift
done

[roma@localhost 3]$ bash bash++.sh 19 8 4
[roma@localhost 3]$ cat road.txt
Number 1 = 19
Number 2 = 8
Number 3 = 4

```
