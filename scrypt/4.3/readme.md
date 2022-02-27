# DevOps Netology HW 4.3

# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            },
            { "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"
            }
        ]
    }
```
Нужно найти и исправить все ошибки, которые допускает наш сервис

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import os, socket, json, yaml

data_file_json = 'dns-list.json'
data_file_yaml = 'dns-list.yaml'

if not os.path.exists(data_file_json) or not os.path.exists(data_file_yaml):
    data = {}
    data['servers'] = []
    server_dns_list = ['drive.google.com', 'mail.google.com', 'google.com']

    for server_dns in server_dns_list:
        data['servers'].append( {
        server_dns: socket.gethostbyname(server_dns)
        })
    with open(data_file_json, 'w') as outfile:
        json.dump(data, outfile)
    with open(data_file_yaml, 'w') as file:
        yaml.dump(data, file)

with open(data_file_json) as json_file:
    data = json.load(json_file)

write_new_data = False
for server in data['servers']:

    for data_dns in server:
        data_ip = server[data_dns]
        curr_ip = socket.gethostbyname(data_dns)
    console_output = (f'{data_dns} - {curr_ip}') 
    print("\033[36m{}\033[0m".format(console_output))

    if curr_ip != data_ip:
        warn_console_output = (f'[WARNING] {data_dns} IP changed: Old: {data_ip} -> New: {curr_ip}')
        print("\033[31m{}\033[0m".format(warn_console_output))
        write_new_data = True
        server[data_dns] = curr_ip

if write_new_data:
    with open(data_file_json, 'w') as outfile:
        json.dump(data, outfile)
    with open(data_file_yaml, 'w') as file:
        yaml.dump(data, file)
```

### Вывод скрипта при запуске при тестировании:
```
drive.google.com - 173.194.222.194
mail.google.com - 74.125.131.19
[WARNING] mail.google.com IP changed: Old: 108.177.14.19 -> New: 74.125.131.19
google.com - 173.194.222.102
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
{"servers": [{"drive.google.com": "173.194.222.194"}, {"mail.google.com": "74.125.131.19"}, {"google.com": "173.194.222.102"}]}
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
servers:
  - drive.google.com: 173.194.222.194
  - mail.google.com: 74.125.131.19
  - google.com: 173.194.222.102
```
