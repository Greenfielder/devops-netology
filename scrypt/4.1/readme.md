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
| Переменная  | Значение | Обоснование |
| ------------- | ------------- | ------------- |
| `a`  | 1  | присваивание значение переменной |
| `b`  | 2  | присваивание значение переменной |
| `c`  | a+b  | Без $ a и b это просто строка |
| `d`  | 1+2  | Подставляет значения переменных $a и $b и выводит строку (без операций вычисления) |
| `e`  | 3  | Производит вычисление переменных $a и $b|


### Вопрос 2.
#### Ответ:
Первая строка не хватает второй закрывающей скобки.  
В цикле в условии нет else exit для корректного завершения скрипта на случай когда сервис станет доступным.

```bash
while ((1==1))
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	else
	    exit
	fi
done
```
### Вопрос 3.
#### Ответ:
```bash
#!/usr/bin/env bash

testconnect() {

if [ -z "$1" ]
then
        echo no host specified
        exit 1
fi

date >> log

curl -k -m 3 http://$1:80

if [ "$?" -eq "0" ]
then
        echo $1:80 is available >> log
else
        echo $1:80 is unavailable >> log
fi

echo  >> log
sleep 1
}

testcurrcount=0
while (($testcurrcount<5))
do
        let "testcurrcount += 1"
        testconnect 192.168.0.1
        testconnect 173.194.222.113
        testconnect 87.250.250.242
done
```
### Вопрос 4.
#### Ответ:
```bash
#!/usr/bin/env bash

testconnect() {

if [ -z "$1" ]
then
        echo no host specified
        exit 1
fi

date >> log

curl -k -m 3 http://$1:80

if [ "$?" -eq "0" ]
then
        echo $1:80 is available >> log
else
        echo $1:80 is unavailable >> log
        date >> error
        echo $1 >> error
        exit 1
fi

echo  >> log
sleep 1
}

while ((1==1))
do
        testconnect 192.168.0.1
        testconnect 173.194.222.113
        testconnect 87.250.250.242
done
```