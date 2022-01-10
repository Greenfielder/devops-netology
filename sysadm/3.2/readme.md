1. Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа.

Ответ: Это встроенная команда Bash и меняет текущую папку только в том терминале, в которой она выполняется.

2. Какая альтернатива без pipe команде grep <some_string> <some_file> | wc -l? man grep поможет в ответе на этот вопрос. 

Ответ: grep -c <some_string> <some_file>

3. Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?

Ответ: systemd

4. Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?

Ответ:  ls 2> /dev/pts/1

5. Получится ли одновременно передать команде файл на stdin и вывести ее stdout в другой файл? Приведите работающий пример.

Ответ: cat input.txt 1> output.txt
Новый ответ: cat <input.txt >> output.txt

6. Получится ли находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?

Ответ: Да, можно.

7. Выполните команду bash 5>&1. К чему она приведет? Что будет, если вы выполните echo netology > /proc/$$/fd/5? Почему так происходит?

Ответ: bash 5>&1 - Тут только перенаправление из нового дискриптора 5 в stdout.

Создаст виртуальный псевдо-файл 5, и запишет в него "netology"
vagrant@vagrant:~/work$ cat /proc/$$/fd/5
netology

8. Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв при этом отображение stdout на pty? Напоминаем: по умолчанию через pipe передается только stdout команды слева от | на stdin команды справа. Это можно сделать, поменяв стандартные потоки местами через промежуточный новый дескриптор, который вы научились создавать в предыдущем вопросе.

Ответ: 
vagrant@vagrant:~/work$ (dir && ls —xxx) 5>&1 1>&2 2>&5 | cat>err.txt
err.txt  input  lala  output
vagrant@vagrant:~/work$

9. Что выведет команда cat /proc/$$/environ? Как еще можно получить аналогичный по содержанию вывод?

Ответ: env

10. Используя man, опишите что доступно по адресам /proc/<PID>/cmdline, /proc/<PID>/exe.
Ответ: 
/proc/<PID>/cmdline. В этом файле(доступный только для чтения) хранится командная строка, которой был запущен данный процесс, до тех пор пока процесс не превратиться в зомби;
/proc/<PID>/exe представляет собой символическую ссылку на исполняемый файл, который инициировал запуск процесса;

11. Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор с помощью /proc/cpuinfo.

Ответ: sse2

12. При открытии нового окна терминала и vagrant ssh создается новая сессия и выделяется pty. Это можно подтвердить командой tty, которая упоминалась в лекции 3.2. Однако:

vagrant@netology1:~$ ssh localhost 'tty'
not a tty
Почитайте, почему так происходит, и как изменить поведение.

Ответ: 
Для того, что бы подключаться по ssh к самому себе (localhost) нужно добавить публичный ключ (~/.ssh/id_rsa.pub) в конец файла ~/.ssh/authorized_keys 


13. Бывает, что есть необходимость переместить запущенный процесс из одной сессии в другую. Попробуйте сделать это, воспользовавшись reptyr. Например, так можно перенести в screen процесс, который вы запустили по ошибке в обычной SSH-сессии.

vagrant@vagrant:~$ ps -a
    PID TTY          TIME CMD
   1400 tty1     00:00:00 bash
   2011 pts/1    00:00:00 sudo
   2081 pts/6    00:00:00 ps
vagrant@vagrant:~$
vagrant@vagrant:~$screen
vagrant@vagrant:~$ ps -a
    PID TTY          TIME CMD
   1400 tty1     00:00:00 bash
   2011 pts/1    00:00:00 sudo
   2082 pts/6    00:00:00 screen
   2092 pts/7    00:00:00 ps
vagrant@vagrant:~$
vagrant@vagrant:~$ tty
/dev/pts/7
vagrant@vagrant:~$
vagrant@vagrant:~$ sudo reptyr -T 2082
(закрыли терминал)

vagrant@vagrant:~$
vagrant@vagrant:~$ tty
/dev/pts/8
vagrant@vagrant:~$ ps -a
    PID TTY          TIME CMD
   1400 tty1     00:00:00 bash
   2011 pts/1    00:00:00 sudo
   2082 pts/6    00:00:00 screen
   2142 pts/7    00:00:00 sudo
   2144 pts/7    00:00:00 reptyr
   2146 pts/8    00:00:00 ps
vagrant@vagrant:~$


14. sudo echo string > /root/new_file не даст выполнить перенаправление под обычным пользователем, так как перенаправлением занимается процесс shell'а, который запущен без sudo под вашим пользователем. Для решения данной проблемы можно использовать конструкцию echo string | sudo tee /root/new_file. Узнайте что делает команда tee и почему в отличие от sudo echo команда с sudo tee будет работать.

Ответ: 
Команда tee читает из стандартного ввода и записывает как в стандартный вывод, в один или несколько файлов одновременно.
"sudo echo string > /root/new_file" - эта команда завершится ошибкой, потому что sudo не выполняет перенаправление вывода, это произойдет как непривилегированный пользователь.
Необходимо использовать команду tee вместе с sudo для записи в файлы, принадлежащие другим пользователям.