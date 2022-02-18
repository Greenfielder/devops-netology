# DevOps Netology HW 4.1

### Вопрос 1. 
#### Ответ:

```
a=1
b=2
c=a+b
d=$a+$b
e=$(($a+$b))
```
| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной c?	  | not defined  | 
| Как получить для переменной c значение 12? | c = str(a) + b  |
| Как получить для переменной c значение 3?  | c = a + int(b)  |


### Обязательная задача 2.
#### Ответ:

```bash
#!/usr/bin/env python3

import os

git_path = "~/study/netology/sysadm-homeworks"

bash_command = ["cd "+git_path, "git status"]
result_os = os.popen(' && '.join(bash_command)).read()

for result in result_os.splitlines():
if result.find('modified') != -1:
prepare_result = result.replace('modified:', '')
print(git_path+"/"+prepare_result.strip())
```

```bash
vagrant@vagrant:~/study/netology/sysadm-homeworks$ ./pyscrypt.py
~/study/netology/sysadm-homeworks/readme.md
~/study/netology/sysadm-homeworks/test.txt
```
### Вопрос 3.
#### Ответ:
```bash
#!/usr/bin/env python3

import os
import sys
 
git_path = "~/study/netology/sysadm-homeworks"

if len(sys.argv)==2:
    if not os.path.exists(sys.argv[1]) or not os.path.isdir(sys.argv[1]):
        print(f'{sys.argv[1]} directory is not found')
        exit(1)
    git_path = sys.argv[1]

bash_command = ["cd "+git_path, "git status"]
result_os = os.popen(' && '.join(bash_command)).read()

for result in result_os.splitlines():
    if result.find('modified') != -1:
        prepare_result = result.replace('modified:', '')
        print(git_path+"/"+prepare_result.strip())
```
```
vagrant@vagrant:~/study/netology/sysadm-homeworks$ ./pyscrypt2.py
~/study/netology/sysadm-homeworks/pyscrypt.py
~/study/netology/sysadm-homeworks/readme.md
~/study/netology/sysadm-homeworks/test.txt
vagrant@vagrant:~/study/netology/sysadm-homeworks$ ./pyscrypt2.py /home/vagrant/study/netology/sysadm-homeworks/
/home/vagrant/study/netology/sysadm-homeworks//pyscrypt.py
/home/vagrant/study/netology/sysadm-homeworks//readme.md
/home/vagrant/study/netology/sysadm-homeworks//test.txt
vagrant@vagrant:~/study/netology/sysadm-homeworks$
```

### Вопрос 4.
#### Ответ:
```bash
#!/usr/bin/env python3

import os, socket, json

data_file = 'dns-list.json'

if not os.path.exists(data_file):
    data = {}
    data['servers'] = []
    server_dns_list = ['drive.google.com', 'mail.google.com', 'google.com']

    for server_dns in server_dns_list:
        data['servers'].append( {
        'dns': server_dns,
        'ip': socket.gethostbyname(server_dns)
        })

    with open(data_file, 'w') as outfile:
        json.dump(data, outfile)

with open(data_file) as json_file:
    data = json.load(json_file)

write_new_data = False
for server in data['servers']:

    curr_ip = socket.gethostbyname(server['dns'])
    console_output = (f'{server["dns"]} - {curr_ip}') 
    print("\033[36m{}\033[0m".format(console_output))

    if curr_ip != server['ip']:
        warn_console_output = (f'[WARNING] {server["dns"]} IP changed: Old: {server["ip"]} -> New: {curr_ip}')
        print("\033[31m{}\033[0m".format(warn_console_output))
        write_new_data = True
        server['ip'] = curr_ip

if write_new_data:
    with open(data_file, 'w') as outfile:
        json.dump(data, outfile)
        
```