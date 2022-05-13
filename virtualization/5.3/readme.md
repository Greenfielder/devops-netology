# DevOps Netology HW 5.3 "Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера"

### Вопрос 1. 
#### Ответ:
**[Link to https://hub.docker.com](https://hub.docker.com/repository/docker/greenfielder/netology_nginx)**

### Вопрос 2.
#### Ответ:

* Высоконагруженное монолитное java веб-приложение;

<b> Можно использовать докер с целью экономии ресурсов (в сравнении с в.м.) и упрощения администрирования. Если цель - максимальная производительность - физический сервер.</b>

*  Nodejs веб-приложение;

<b> Используем докер - удобство администрирования, экономия ресурсов. </b>

*  Мобильное приложение c версиями для Android и iOS;

<b> Используем докер - удобство администрирования, экономия ресурсов. </b>

*  Шина данных на базе Apache Kafka;

<b> Можно использовать докер - для экономии ресурсов, физические машины - для максимальной производительности. </b>

*  Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;

<b> Используем докер - удобство администрирования, экономия ресурсов. </b>

*  Мониторинг-стек на базе Prometheus и Grafana;

<b> Используем докер - удобство администрирования, экономия ресурсов. </b>

*  MongoDB, как основное хранилище данных для java-приложения;

<b> Можно использовать докер - для экономии ресурсов, физические машины - для максимальной производительности. </b>

*  Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

<b> Используем докер - удобство администрирования, экономия ресурсов. </b>
   
### Вопрос 3.
#### Ответ:
```
dimon@dimon-VirtualBox:~$ sudo docker pull centos
dimon@dimon-VirtualBox:~$ sudo docker pull debian
dimon@dimon-VirtualBox:~$ sudo docker run -d -t -v "$(pwd)"/data/:/data centos /bin/bash
dimon@dimon-VirtualBox:~$ sudo docker run -d -t -v "$(pwd)"/data/:/data debian /bin/bash
dimon@dimon-VirtualBox:~$ sudo docker ps -a
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS                     PORTS     NAMES
272df42e248b   debian           "/bin/bash"              6 minutes ago   Up 6 minutes                         eager_engelbart
842913eb88de   centos           "/bin/bash"              7 minutes ago   Up 7 minutes                         focused_zhukovsky
db70b70b319d   netology_nginx   "/docker-entrypoint.…"   18 hours ago    Exited (0) 18 hours ago              sweet_panini
2101e4a5d1c7   nginx            "/docker-entrypoint.…"   18 hours ago    Exited (0) 18 hours ago              dazzling_mccarthy
2772f4a55eb5   ubuntu           "bash"                   2 weeks ago     Exited (0) 2 weeks ago               goofy_chatelet
ead2bf4f69f5   ubuntu           "bash"                   2 weeks ago     Exited (127) 2 weeks ago             brave_nash
45a551e5fac7   hello-world      "/hello"                 2 weeks ago     Exited (0) 2 weeks ago               heuristic_booth

dimon@dimon-VirtualBox:~$ sudo docker exec -it focused_zhukovsky bash
[root@842913eb88de /]# echo 'This is test document' > /data/test.txt
[root@842913eb88de /]# exit

dimon@dimon-VirtualBox:~$ echo  'Second text document' > data/test2.txt

dimon@dimon-VirtualBox:~$ sudo docker exec -it eager_engelbart bash
root@272df42e248b:/# ls /data
test.txt  test2.txt

```

