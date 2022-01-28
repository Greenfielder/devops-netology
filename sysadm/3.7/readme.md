# DevOps Netology HW 3.6

### Вопрос 1. 
#### Ответ:
* Под Windows: ipconfig, под linux: ip link show
### Вопрос 2.
#### Ответ:
* Протокол: LLDP 
* Пакет: lldpd
* Команда в Linux: lldpctl
### Вопрос 3.
#### Ответ:
* VLAN; vlan
```
vi /etc/network/interfaces
auto vlan1400
iface vlan1400 inet static        
            address 192.168.1.1        
            netmask 255.255.255.0        
            vlan_raw_device eth0
```
### Вопрос 4.
#### Ответ:
* Bonding; balance-rr, active-backup, balance-xor, broadcast, 802.3ad, balance-tlb, balance-alb

```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto bond0 eth0 eth1
# настроим параметры бонд-интерфейса
iface bond0 inet static
        address 10.0.0.11
        netmask 255.255.255.0
        gateway 10.0.0.254
        # определяем объединяемые интерфейсы
        bond-slaves eth0 eth1
        # задаем тип бондинга
        bond-mode balance-alb
        # интервал проверки линии в миллисекундах
        bond-miimon 100
        # Задержка перед установкой соединения в миллисекундах
        bond-downdelay 200
        # Задержка перед обрывом соединения в миллисекундах
        bond-updelay 200
```

### Вопрос 5.
#### Ответ:
* /29 - 8ips; 32 /29 subnets from /24 network;
* 10.10.10.8/29, 10.10.10.16/29, 10.10.10.248/29
### Вопрос 6.
#### Ответ:
* 100.64.0.0/26
### Вопрос 7.
#### Ответ:
* Win: arp -a, arp -d ip, arp -d *;
* Linux: ip neigh show, ip neigh del ip dev int, ip -s neigh flush all
