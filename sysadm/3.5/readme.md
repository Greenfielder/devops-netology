# DevOps Netology HW 3.5

### Вопрос 1. 
#### Ответ:
* Файл, в котором последовательности нулевых байтов заменены на информацию об этих последовательностях (список дыр).

### Вопрос 2.
#### Ответ:
* Нет. Это один и тот же объект.
### Вопрос 3.
#### Ответ:
* Выполнено

### Вопрос 4.
#### Ответ:
* sudo fdisk -l (Что бы посмотреть какие есть диски)
* sudo fdisk /dev/sdb

### Вопрос 5.
#### Ответ:
* sudo sfdisk -d /dev/sdb | sudo sfdisk --force /dev/sdc

### Вопрос 6.
#### Ответ:
* sudo mdadm --create --verbose /dev/md0 --level=mirror --raid-devices=2 /dev/sdb1 /dev/sdc1
### Вопрос 7.
#### Ответ:
* sudo mdadm --create --verbose /dev/md1 --level=stripe --raid-devices=2 /dev/sdb2 /dev/sdc2
### Вопрос 8.
#### Ответ:
* sudo pvcreate /dev/md0
* sudo pvcreate /dev/md1
### Вопрос 9.
#### Ответ:
* sudo vgcreate vg01 /dev/md0 /dev/md1
### Вопрос 10.
#### Ответ:
* sudo lvcreate -n volume_0 -L 100 vg01 /dev/md1
### Вопрос 11.
#### Ответ:
* sudo mkfs.ext4 /dev/vg01/volume_0
### Вопрос 12.
#### Ответ:
* mkdir /tmp/new
* sudo mount /dev/vg01/volume_0 /tmp/new
### Вопрос 13.
#### Ответ:
* sudo wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
### Вопрос 14.
#### Ответ:
```
vagrant@vagrant:~$ lsblk
NAME                 MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                    8:0    0   64G  0 disk
├─sda1                 8:1    0  512M  0 part  /boot/efi
├─sda2                 8:2    0    1K  0 part
└─sda5                 8:5    0 63.5G  0 part
├─vgvagrant-root   253:0    0 62.6G  0 lvm   /
└─vgvagrant-swap_1 253:1    0  980M  0 lvm   [SWAP]
sdb                    8:16   0  2.5G  0 disk
├─sdb1                 8:17   0    2G  0 part
│ └─md0                9:0    0    2G  0 raid1
└─sdb2                 8:18   0  511M  0 part
└─md1                9:1    0 1018M  0 raid0
└─vg01-volume_0  253:2    0  100M  0 lvm   /tmp/new
sdc                    8:32   0  2.5G  0 disk
├─sdc1                 8:33   0    2G  0 part
│ └─md0                9:0    0    2G  0 raid1
└─sdc2                 8:34   0  511M  0 part
└─md1                9:1    0 1018M  0 raid0
└─vg01-volume_0  253:2    0  100M  0 lvm   /tmp/new
```

### Вопрос 15.
#### Ответ:
* 0
### Вопрос 16.
#### Ответ:
* sudo pvmove /dev/md1 /dev/md0
### Вопрос 17.
#### Ответ:
* sudo mdadm --fail /dev/md0 /dev/sdb1
### Вопрос 18.
#### Ответ:
```
vagrant@vagrant:~$ dmesg | tail -n 2
[64718.531980] md/raid1:md0: Disk failure on sdb1, disabling device.
md/raid1:md0: Operation continuing on 1 devices.
```
### Вопрос 19.
#### Ответ:
* 0
### Вопрос 20.
#### Ответ:
* Тестовый хост погашен