# DevOps Netology HW 3.4

### Вопрос 1. 
#### Ответ:
* Готово

### Вопрос 2.
#### Ответ:
* CPU - node_cpu_seconds_total{cpu="0",mode="system"}
* Memory - node_memory_MemTotal_bytes - node_memory_MemFree_bytes
* Disk - node_disk_io_time_seconds_total{device="sda"}
* Network - node_network_receive_bytes_total{device="enp0s3"}

### Вопрос 3.
#### Ответ:
* Готово

### Вопрос 4.
#### Ответ:
Да

* CPU MTRRs all blank - virtualized system.
* scsi 2:0:0:0: Direct-Access     ATA      VBOX HARDDISK    1.0  PQ: 0 ANSI: 5 
* systemd[1]: Detected virtualization oracle.

### Вопрос 5.
#### Ответ:
* sysctl -a | grep fs.nr_open
* fs.nr_open = 1048576
* Лимит на количество открытых файловых дескрипторов
* ulimit -n number (number - the maximum number of open file descriptors)

### Вопрос 6.
#### Ответ:
>root@vagrant:/# nsenter -t 1369 -p -m<br>
root@vagrant:/# ps aux<br>
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND<br>
root           1  0.0  0.0   8076   528 pts/2    S    20:53   0:00 sleep 1h<br>
root           2  0.0  0.4   9836  4132 pts/2    S    20:56   0:00 -bash<br>
root          11  0.0  0.3  11492  3384 pts/2    R+   20:56   0:00 ps aux<br>

### Вопрос 7.
#### Ответ:

fork bomb<br>
: - function name<br>
[Tue Jan 11 21:16:18 2022] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-1.scope<br>
ulimit -u 50 helps to limit amount of processes per user<br>
