# Домашнее задание к занятию "Система мониторинга Zabbix" - Калитвянский Александр SYS-27


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Процесс выполнения установки Zabbix Server с веб-интерфейсом

1.  sudo apt update
2.  sudo apt install postgresql
3.  wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb
4.  sudo dpkg -i zabbix-release_6.0-5+debian12_all.deb
5.  sudo apt update
6.  sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts
7.  sudo -u postgres createuser --pwprompt zabbix
8.  sudo -u postgres createdb -O zabbix zabbix
9.  zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
10. vim /etc/zabbix/zabbix_server.conf
11. DBPassword=zabbix
12. sudo systemctl restart zabbix-server apache2
13. sudo systemctl enable zabbix-server apache2

![скриншот 1](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/1_welcome/png)
![скриншот 2](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/2_step.png)
![скриншот 3](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/3_step.png)
![скриншот 4](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/4_step.png)
![скриншот 5](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/5_step.png)
![скриншот 6](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/6_step.png)
![скриншот 7](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/7_step.png)
![скриншот 8](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/8_step.png)
![скриншот 9](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/9_step_zabix_window.png)


---

### Задание 2

Установка Zabbix Agent на хосты.

1. Устаннавливаем Zabbix Agent на 2 вирт. машины, одна из которых Zabbix Server:
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb
   sudo dpkg -i zabbix-release_6.0-5+debian12_all.deb
   sudo apt update
   sudo apt install zabbix-agent
2. Добавляем Zabbix Server в список разрешенных серверов Zabbix Agent:
   sed -i 's/Server=127.0.0.1/Server=192.168.122.88'/g' /etc/zabbix/zabbix_server.conf
![скриншот 1](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/log_vm1.png)
![скриншот 2](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/log_zabbix_server.png) 
3. Добавляем Zabbix Agent в раздел Configuration > Hosts:
![скриншот 3](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/hosts.png)
4. Проверяем, что в разделе Latest Data начали появляться данные с добавленных агентов:
![скриншот 4](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/monitoring_vm1.png)
![скриншот 5](https://github.com/akalitvyanskiy/zabbix1/blob/main/img/monitoring_zabbix_server.png)

