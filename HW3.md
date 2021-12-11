# Homework 3
## ex 1
```bash
[roma2@localhost ~]$ cat access.log | grep -Po '\"\s\".*\"$' | grep -Po '[^\"]{1,}' | awk -F '"' '{arr[$1]+=1}END{for (ip in arr) print arr[ip], ip}' | uniq |sort -k1n | tail -n3 | head -n1
340874 Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)
```
## ex 2
```bash
[roma2@localhost ~]$ awk 'BEGIN{cnt=0;}{split($4,y,"/");split(y[3],yy,":");i
f($1=="216.244.66.230"){r[sprintf("%s %s",y[2],yy[1])]+=1;cnt+=1;}}END{for (
i in r) print i, r[i], "reqs"; print "Total requests:",cnt}' access.log | so
rt -k1,1M | sort -k2n
Total requests: 396
Dec 2020 1 reqs
Apr 2021 34 reqs
Aug 2021 108 reqs
Dec 2021 5 reqs
Feb 2021 14 reqs
Jan 2021 43 reqs
Jul 2021 23 reqs
Jun 2021 3 reqs
Mar 2021 2 reqs
May 2021 27 reqs
Nov 2021 106 reqs
Oct 2021 23 reqs
Sep 2021 7 reqs
```
## ex 3
```bash
[roma2@localhost ~]$ awk 'BEGIN{ips[$1]=0}{ips[$1]+=$10}END{for (key in ips) print ips[key]" bytes for "key}' access.log
10439 bytes for 34.223.3.249
10439 bytes for 3.19.243.250
.
.
.
10466 bytes for 94.154.220.93
26209910 bytes for 145.253.118.26
```
## ex 4
```bash

[roma2@localhost ~]$ sed -E 's/\"\s\".*\"$/" "lynx"/' access.log
13.66.139.0 - - [19/Dec/2020:13:57:26 +0100] "GET /index.php?option=com_phocagallery&view=category&id=1:almhuette-raith&Itemid=53 HTTP/1.1" 200 32653 "-" "lynx"
157.48.153.185 - - [19/Dec/2020:14:08:06 +0100] "GET /apache-log/access.log HTTP/1.1" 200 233 "-" "lynx"
157.48.153.185 - - [19/Dec/2020:14:08:08 +0100] "GET /favicon.ico HTTP/1.1" 404 217 "http://www.almhuette-raith.at/apache-log/access.log" "lynx"
216.244.66.230 - - [19/Dec/2020:14:14:26 +0100] "GET /robots.txt HTTP/1.1" 200 304 "-" "lynx"
54.36.148.92 - - [19/Dec/2020:14:16:44 +0100] "GET /index.php?option=com_phocagallery&view=category&id=2%3Awinterfotos&Itemid=53 HTTP/1.1" 200 30662 "-" "lynx"
92.101.35.224 - - [19/Dec/2020:14:29:21 +0100] "GET /administrator/index.php HTTP/1.1" 200 4263 "" "lynx"
73.166.162.225 - - [19/Dec/2020:14:58:59 +0100] "GET /apache-log/access.log HTTP/1.1" 200 1299 "-" "lynx"
73.166.162.225 - - [19/Dec/2020:14:58:59 +0100] "GET /favicon.ico HTTP/1.1" 404 217 "http://www.almhuette-raith.at/apache-log/access.log" "lynx"
54.36.148.108 - - [19/Dec/2020:15:09:30 +0100] "GET /robots.txt HTTP/1.1" 200 304 "-" "lynx"
.
.
.
```
## ex 5
```bash
[roma2@localhost ~]$ unset x; declare -Ax; while read line; do word1=&(echo $line | sed 's/[//'); word2=$(echo $line | sed 's/[^"["]*//'); if [[ ${x[${word1}]} == "" ]]; then x[${word1}]='ip'; fi; echo ${x[${word1}]} $word2 >> dump; done < access.log; mv dump access.log
[roma2@localhost ~]$ cat access.log
ip [19/Dec/2020:13:57:26 +0100] "GET /index.php?option=com_phocagallery&view=category&id=1:almhuette-raith&Itemid=53 HTTP/1.1" 200 32653 "-" "Mozilla/5.0 (compatible; bingbot/2.0; +http://www.bing.com/bingbot.htm)" "-"
ip [19/Dec/2020:14:08:06 +0100] "GET /apache-log/access.log HTTP/1.1" 200 233 "-" "Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36" "-"
.
.
.
```
