# DevOps Netology HW 3.6

### Вопрос 1. 
#### Ответ:
* HTTP/1.1 301 Moved Permanently
* Код показывает, что запрошенный ресурс был окончательно перемещён в URL, указанный в заголовке Location
* location: https://stackoverflow.com/questions
### Вопрос 2.
#### Ответ:
* 307 Internal Redirect
* document 407ms
![scr36.png](/img/scr36.png)
### Вопрос 3.
#### Ответ:
* Мой IP: 95.31.181.32
### Вопрос 4.
#### Ответ:
* Beeline Home, AS8402
### Вопрос 5.
#### Ответ:
* AS8402, AS15169
```
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.0.1 [*]  2.966 ms  2.849 ms  2.784 ms
 2  100.120.0.1 [*]  10.236 ms  10.077 ms  10.003 ms
 3  * * *
 4  * * *
 5  85.21.93.129 [AS8402]  12.471 ms  12.293 ms 85.21.224.191 [AS8402]  12.181 ms
 6  * * *
 7  108.170.226.90 [AS15169]  11.159 ms 172.253.66.116 [AS15169]  97.579 ms 108.170.250.33 [AS15169]  97.361 ms
 8  108.170.250.130 [AS15169]  97.225 ms * 108.170.250.83 [AS15169]  96.992 ms
 9  142.250.238.181 [AS15169]  96.991 ms 172.253.66.116 [AS15169]  96.851 ms *
10  108.170.232.251 [AS15169]  96.674 ms * 216.239.48.224 [AS15169]  96.444 ms
11  142.250.56.215 [AS15169]  96.413 ms * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * 8.8.8.8 [AS15169]  27.253 ms  30.715 ms
```
### Вопрос 6.
#### Ответ:
* 216.239.48.224 56.3 ms avg
### Вопрос 7.
#### Ответ:
```
mickey@mickey-pc:~$ dig dns.google ns | grep zdns
dns.google.    21600  IN  NS  ns4.zdns.google.
dns.google.    21600  IN  NS  ns3.zdns.google.
dns.google.    21600  IN  NS  ns2.zdns.google.
dns.google.    21600  IN  NS  ns1.zdns.google.
```
```
mickey@mickey-pc:~$ dig dns.google | grep 8.8.
dns.google.    1359  IN  A  8.8.4.4
dns.google.    1359  IN  A  8.8.8.8
```
### Вопрос 8.
#### Ответ:
```
mickey@mickey-pc:~$ dig -x 8.8.8.8 | grep dns.google
8.8.8.8.in-addr.arpa.  6766  IN  PTR  dns.google.
mickey@mickey-pc:~$ dig -x 8.8.4.4 | grep dns.google
4.4.8.8.in-addr.arpa.  37386  IN  PTR  dns.google.
mickey@mickey-pc:~$
```