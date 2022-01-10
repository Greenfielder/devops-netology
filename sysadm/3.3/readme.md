# DevOps Netology HW 3.3

### Вопрос 1. 
#### Ответ:
* execve("/bin/bash", ["/bin/bash", "-c", "cd /tmp"], 0x7ffe5be384d0 /* 24 vars */) = 0

### Вопрос 2.
#### Ответ:
* "/etc/magic"
* "/usr/share/misc/magic.mgc"

### Вопрос 3.
#### Ответ:
* " ls -l /proc/<pid>/fd - (fd удаленного файла) "
* " > /proc/<pid>/fd/<fd> "

### Вопрос 4.
#### Ответ:
* Нет. Только кусок памяти где хранится информации о нём.

### Вопрос 5.
#### Ответ:
* 849    vminfo              5   0 /var/run/utmp
* 580    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
* 580    dbus-daemon        18   0 /usr/share/dbus-1/system-services
* 580    dbus-daemon        -1   2 /lib/dbus-1/system-services
* 580    dbus-daemon        18   0 /var/lib/snapd/dbus-1/system-services/

### Вопрос 6.
#### Ответ:
Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.

### Вопрос 7.
#### Ответ:
";" commands separated by a ; are executed sequentially. The shell waits for each command to terminate in turn.
"&&" command after && is executed if, and only if, command before && returns an exit status of zero

Нет смысла использовать &&, т.к. при использовании set -e в случае возврата любой из подкомманд exit code != 0 скрипт автоматически завершится.

### Вопрос 8.
#### Ответ:
* -e Exit immediately if a command exits with a non-zero status.
* -u Treat unset variables as an error when substituting.
* -x Print commands and their arguments as they are executed.
* -o pipefail the return value of a pipeline is the status of the last command to exit with a non-zero status, or zero if no command exited with a non-zero status

Хорошо использовать в сценариях т.к. с этими опциями написанный код лучше проверяется на корректность и его проще диагностировать в случае каких-либо ошибок или некорректной работы.

### Вопрос 9.
#### Ответ: 
* interruptible sleep (waiting for an event to complete)