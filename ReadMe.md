# Операционные системы и виртуализация (Linux)

sudo usermod -aG vboxsf mordvin (предоставить админ права юзеру для общих папок)
sudo apt install gcc make perl - установка/обновление данных пакетов
sudo apt update - проверка обновлений
ip a (вывод инфы сетевого подключения)
sudo apt install openssh-server - запуск/проверка сервера
ssh -p 8022 mordvin@localhost - зайти в консоль линукс с винды (NAT)
ssh mordvin@ipAdress - зайти в консоль линукс с винды (Сетевой мост)
sudo ss -ntlp
systemctl status ssh - статус сервера
sudo su - стать админом (exit - вернуться юзером)
df -h - информация файловой системы
ln file1 file3 - абсолютная ссылка с именем file3 (на диске один файл)
ln -s file1 file3 - символическая ссылка на file1 (ярлык с именем file3)
ls - просмотр папки простой
ls -al - просмотр папки в виде списка со скрытыми файлами и папками
ls -ali - просмотр папки в виде списка со скрытыми файлами и папками + inode
ll - псевдоним Линукс просмотра папки в виде списка со скрытыми файлами и папками
rm - удалить
mv - переименовать
cp - копировать
mkdir - создать папку
mkdir -p - создать папку  (-p, --parents не выдавать ошибку, если существует; создавать родительские каталоги при необходимости)

"команда" --help справка по команде

touch filename - создать пустой файл
cat > filename - создать файл и ввести в него текст
cat >> filename - добавить текст в файл
cat filename - вывод текста файла на экран
Для безопасного удаления пустых папок удобно также использовать команду rmdir
Файл также можно создать командой:
echo "text" >> filename

sudo chmod u=rw,g=rw,o=r filename - права доступа файла
sudo chmod 664 filename - права доступа файла с помощью восьмеричной системы (цифровой код с набором прав доступа)

sudo chown -R www-data:sambashare foldername - задать владельца и группу для папки (владелец:группа)

sudo useradd -s /bin/bash username - создание пользователя без вопросов но с заданными параметрами
sudo adduser username - создание пользователя )система предложит вводить данные пользователя)

id - вывод информации текущего пользователя
id username - вывод информации указанного пользователя

sudo userdel -r username - удаление пользователя (-r этот параметр так же удалит его рабочую папку)

sudo addgroup gropname - создание группы
sudo groupdel gropname - удаление группы

sudo usermod -g gropname username - смена основной группы пользователя
sudo usermod -aG gropname username - добавление пользователя в группу

cat /etc/passwd | grep username - вывод инфы с файла пользователей ( | grep username - фильтрация)

sudo usermod -aG sudo username - дать права sudo пользователю

sudo visudo - прописать непосредственно пользователя в sudo в файле - /etc/sudoers (можно сделать неограниченные права на уровне root, убрать запрос пароля (ALL=(ALL:ALL) NOPASSWD: ALL - перед последним ALL) и т.д.), но лучше сюда не лазить и давать права на уровне групп!

sudo visudo
username    ALL=(ALL:ALL) NOPASSWD: /bin/bash, /usr/bin/passwd - права sudo на несколько команд

which passwd - где находится команда на примере passwd - /usr/bin/passwd

https://dev.mysql.com/downloads/repo/apt/ - репозиторий Ubuntu / Debian (Architecture Independent), DEB Package

wget https://dev.mysql.com/get/mysql-apt-config_0.8.30-1_all.deb - скачать пакет в текущую папку

sudo dpkg -i mysql-apt-config_0.8.30-1_all.deb - установка скачанного пакета

cd /etc/apt - папка с пакетами

cat mysql.list - вывод содержимого списка репозиториев в файле

sudo apt update - скачать списки пакетов с репозитория

sudo apt install mysql-community-server - установка необходимого с выбранного репозитория

sudo apt purge mysql-community-server - удаление выбранного пакета

sudo apt remove mysql-community-server - удаление выбранного пакета, но файлы настроек конфига останутся

sudo dpkg -r mysql-apt-config - удаление установленного пакета
Удалять пакеты в команде dpkg можно также с ключом "-P|--purge".
Этот вариант кроме удаления исходников чистит и файлы конфигурации удаляемого пакета.

sudo snap install --classic certbot - установка snap-пакета

sudo snap remove certbot - удаление snap-пакета

sudo add-apt-repository ppa:obsproject/obs-studio - подключение PPA репозитория

sudo apt install obs-studio - установка пакета из PPA репозитория

В Linux также есть планировщик задач 'at'.
Информацию можно посмотреть тут:
https://andreyex.ru/linux/komandy-linux-i-komandy-shell/komanda-at-v-linux/

nano /etc/crontab - редактирование системного файла расписания
Выполнение регулярных задач по расписанию
Автоматизация обслуживания системы или приложений
Системные задачи:
/etc/crontab
/etc/cron.d/*
Пользовательские задачи:
/var/spool/cron/*
управление: утилита crontab

crontab - l вывести содержимое текущего файла расписания
crontab -r удаление текущего файла расписания
crontab -e редактирование текущего файла расписания
sudo crontab -u username – работа с файлом расписания другого пользователя

shutdown -P --no-wall - выключить с терминала без вопросов
shutdown --help
shutdown [OPTIONS...] [TIME] [WALL...]

Shut down the system.

Options:
     --help      Show this help
  -H --halt      Halt the machine
  -P --poweroff  Power-off the machine
  -r --reboot    Reboot the machine
  -h             Equivalent to --poweroff, overridden by --halt
  -k             Don't halt/power-off/reboot, just send warnings
     --no-wall   Don't send wall message before halt/power-off/reboot
  -c             Cancel a pending shutdown
See the shutdown(8) man page for details.

## Завершить процесс можно командой kill. Справка по команде: 'man kill'.

ip a - вывести параметры сети на экран
ip -c a - вывести параметры сети на экран с цветовым подсвечиванием
параметр -s ещё и выдат статистику по интерфейсам
ip r - вывести параметры маршртизации на экран, так же можно с параметром -c

ss -ntlp - паказать набор работающих портов или сокетов
ss – socket stat
ss -ntlp – TCP-сокеты в состоянии LISTEN
ss -ntulp – TCP и UDP-сокеты в состоянии LISTEN
ss -tulpan – Все TCP и UDP-сокеты

ip addr add 10.0.2.15/24 broadcast 10.0.2.255 dev enp0s3 или
ip addr add 10.0.2.15/255.255.255.0 broadcast 10.0.2.255 dev enp0s3 - добавление ip адреса
ip addr del 10.0.2.16/24 broadcast 10.0.2.255 dev enp0s3 - удаление ip адреса

ip route add default via 10.0.2.1 dev enp0s3 - добавить маршрут по умолчанию (шлюз)
если не на правах root, то не забываем перед командами прописывать sudo

ip route del default via 10.0.2.1 dev enp0s3 - удаление указанного маршрута

cd /etc/netplan/ - каталог с файлами конфигурации сети

nano 01-network-manager-all.yaml - правка файла конфигурации сети

netplan try - применение настроек сети с подтверждением, если связь потеряется через 2 минуты вернутся предыдущие.

ping ya.ru - проверка связи с хостом

resolvectl dns - показать использующиеся DNS

Информаия о хосте:
host -t a ya.ru
host -t a ya.ru 1.1.1.1
host -t mx ya.ru
ya.ru mail is handled by 10 mx.yandex.ru.
dig ya.ru
tracepath ya.ru

iptables -nvL - информаия маршрутизаии
iptables -nvL --line-numbers - информаия маршрутизаии с номерами строк

iptables -nvL -t nat - информаия маршрутизаии NAT

## Пример конфигурации сервера
# SSH allow
iptables -A INPUT -p tcp --dport=22 -j ACCEPT
# HTTP, HTTPS allow
iptables -A INPUT -p tcp -m multiport --dport 80,443 -j ACCEPT
# loopback allow
iptables -A INPUT -i lo -j ACCEPT
# ICMP
iptables -A INPUT -p icmp -j ACCEPT
# established connections allow
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# policy drop
iptables -P INPUT DROP
-A - конец списка
-I - начало списка
Перенаправление портов
Редирект с 80 на 8080 порт (TCP):
iptables -t nat -I PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
Проверка:
iptables -L -nv -t nat

Сохранение конфигурации iptables
Сохранение и восстановление из файла
iptables-save > iptables.rules
iptables-restore < iptables.rules
Сервис netfilter-persistent для автоматического восстановления при загрузке системы
apt install iptables-persistent netfilter-persistent
netfilter-persistent save
Конфигурация в /etc/iptables

В качестве дополнительного материала рекомендую ознакомиться с альтернативой iptables: утилита UFW. https://losst.pro/nastrojka-ufw-ubuntu

apt install nginx apache2 libapache2-mod-php8.1 php8.1 php8.1-fpm mysql-server-8.0 - установка всех компонентов для работы веб серверов и базы данных mysql

Консольные утилиты для веб
Получить URL в консоли:
curl -L https://ya.ru/ - вывод кода страниы
wget https://yastatic.net/jquery/2.1.4/jquery.min.js - скачать файл в текущую папку

ps afx - Диспетчер задач

nginx -t - проверка конфигураии веб-сервера на синтаксис и прочее
apachectl -t

systemctl reload nginx - перезапуск сервера
nginx -s reload - перезагрузка с проверкой конфигураии

systemctl start apache2 - запуск сервера

systemctl status apache2 - проверка состояния сервера

РАБОТА С БАЗАМИ ДАННЫХ mysql:
mysql - запуск и вход для работы с базами данных mysql (пользователь root или права)

CREATE DATABASE mordvin_database; - создание базы данных
USE mordvin_database; - вход для работы с базой данных
CREATE TABLE mordvin_table(i INT); - создание таблицы

## Установка MySQL и первые шаги
● Установка: apt install mysql-server-8.0
● Заходим в консоль MySQL: sudo mysql
● Переходим в системную БД mysql: use mysql;
● Получаем список пользователей: SELECT * FROM user\G
● Создаём новую базу данных: CREATE DATABASE gb;
● Создаём таблицу: CREATE TABLE test(i INT);
● Создадим записи в таблице: INSERT INTO test (i) VALUES (1),(2),(3),(4);
● Сделаем выборку из таблицы: SELECT * FROM test;

apt install docker.io docker-compose - установка докера и докер-компоус (Запуск веб-приложения из контейнеров)

service nginx stop - остановить сервер (либо systemctl)

curl -L localhost:8082 - зайти на сайт с консоли

docker ps - диспетчер задач докера

docker run --rm --network compose-network --name mordvin-mariadb -e MYSQL_ROOT_PASSWORD=Mordvin00 -d mariadb:10.8

docker run --name myadmin -d --network compose-network --link mordvin-mariadb:db -p 8082:80 phpmyadmin - запуск с параметрами

docker network create compose-network - создание сетевого интерфейса

ss -ntlp | grep 80 - проверка соединений с филтром по 80

docker-compose ps - диспетчер задач

docker-compose up -d - запуск

apt install tree
tree - вывод древа папки и файлов

## Скрипты Bash

Bash — язык программирования
● Интерпретатор — /bin/bash
● Переменные
● Условия
● Циклы
● Функции
● Однострочные скрипты

Код возврата (завершения) — exit code
● Код ошибки последней команды
● Проверить: echo $?
● Условная связка (И): ls -al && echo "Success!"
● Условная связка (ИЛИ): ls -al || echo "Fail!"

Перенаправление потоков ввода-вывода
● program < file – перенаправление ввода из файла file
● program > file – перенаправление вывода (STDOUT) в файл file (запись с начала файла)
● program >> file – перенаправление вывода (STDOUT) в файл file в режиме дополнения файла
● program 2> file – перенаправление ошибок (STDERR) в файл file (запись с начала файла)
● program 2>> file – перенаправление ошибок (STDERR) в файл file в режиме дополнения файла
● program > file 2>&1 – перенаправление вывода (STDOUT) и ошибок (STDERR) в файл file
(запись с начала файла)

Конвейер (pipeline, pipe)

● Перенаправление ввода-вывода между процессами
● ls -al | grep file
● ls -al | grep -P '\.[cs]+'
● cat /var/log/syslog | grep 'mysql' | grep -v 'file' | wc -l

Переменные и их классификация

● Переменные окружения
○ $PATH
○ $UID
○ $PWD
● Пользовательские переменные
○ var1=test
○ echo $var1
● Специальные переменные
○ $1…$9
○ $?

Создаём первый скрипт на bash

cat > testscript
#!/bin/bash
directory=$1
hidden_count=$(ls -A $directory | grep '^\.' | wc -l)
echo “Hidden files in $directory found: $hidden_count”

Методы запуска скрипта

● Относительный путь: ./testscript
● Абсолютный путь: /home/db/test/testscript
● Команда (должен быть в $PATH): testscript
● Через команду bash: bash testscript
● Первые три варианта требуют шебанг и права на исполнение

Однострочные скрипты

● Разделитель команд — ";"
● Удобны для выполнения в терминале
● Применимы все основные конструкции из bash
● apt update; apt upgrade; echo "Upgrade complete!"

Условия if и ветвления

Синтаксис:
if [ выражение ]
 then
 Действия, если выражение истинно
 else
 Действия в противоположном случае
fi
Пример:
if [ -e file_name ]
 then
 echo "true"
 else
 echo "false"
fi

Варианты условий

Операции сравнения строк
● = или == возвращает true (истина), если строки равны
● != возвращает true (истина), если строки не равны
● -z возвращает true (истина), если строка пуста
● -n возвращает true (истина), если строка не пуста
Операции проверки файлов
● -e возвращает true (истина), если файл существует (exists)
● -d возвращает true (истина), если каталог существует (directory)
Операции сравнения целых чисел (наиболее используемые)
● -eq возвращает true (истина), если числа равны (equals)
● -ne возвращает true (истина), если числа не равны (not equal)

Цикл for

Синтаксис:
for имя_переменной in значения
do
 тело_цикла
done
Примеры:
for h in {01..24}
do
echo $h
done
for (( c=1; c<=5; c++ ))
do
 echo "Попытка номер $c"
done

Цикл while

Цикл while
Синтаксис:
while [ условие ]
do
 Тело_цикла
done
Пример:
c=10
while [ $c -ge 0 ]
do
echo "Test"
let "c = c - 1"
done