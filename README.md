# systemd

## Задание 
1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/sysconfig).
2. Из репозитория epel установить spawn-fcgi и переписать init-скрипт на unit-файл (имя service должно называться так же: spawn-fcgi).
3. Дополнить unit-файл httpd (он же apache) возможностью запустить несколько инстансов сервера с разными конфигурационными файлами. 
4*. Скачать демо-версию Atlassian Jira и переписать основной скрипт запуска на unit-файл.

## Решение 

Решение представленно в виде shell скрипта при развертывании машины командой "vagrant up", файлы watchlog.timer, watchlog.service, watchlog.sh и watchdog копируются на сервер. 

```
    systemd: Running: inline script
    systemd: May  8 20:25:06 localhost systemd: Reloading.
    systemd: May  8 20:25:07 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:07 localhost root: Sun May  8 20:25:07 UTC 2022: I found word, Master!
    systemd: May  8 20:25:07 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:07 localhost systemd: Started Run watchlog script every 30 second.
==> systemd: Running provisioner: shell...
    systemd: Running: inline script
    systemd: May  8 20:25:06 localhost systemd: Reloading.
    systemd: May  8 20:25:07 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:07 localhost root: Sun May  8 20:25:07 UTC 2022: I found word, Master!
    systemd: May  8 20:25:07 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:07 localhost systemd: Started Run watchlog script every 30 second.
    systemd: May  8 20:25:09 localhost systemd: Reloading.
    systemd: May  8 20:25:09 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:09 localhost root: Sun May  8 20:25:09 UTC 2022: I found word, Master!
    systemd: May  8 20:25:09 localhost systemd: Started My watchlog service.
==> systemd: Running provisioner: shell...
    systemd: Running: inline script
    systemd: May  8 20:25:06 localhost systemd: Reloading.
    systemd: May  8 20:25:07 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:07 localhost root: Sun May  8 20:25:07 UTC 2022: I found word, Master!
    systemd: May  8 20:25:07 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:07 localhost systemd: Started Run watchlog script every 30 second.
    systemd: May  8 20:25:09 localhost systemd: Reloading.
    systemd: May  8 20:25:09 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:09 localhost root: Sun May  8 20:25:09 UTC 2022: I found word, Master!
    systemd: May  8 20:25:09 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:11 localhost systemd: Reloading.
    systemd: May  8 20:25:11 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:11 localhost root: Sun May  8 20:25:11 UTC 2022: I found word, Master!
    systemd: May  8 20:25:12 localhost systemd: Started My watchlog service.
==> systemd: Running provisioner: shell...
    systemd: Running: inline script
    systemd: May  8 20:25:06 localhost systemd: Reloading.
    systemd: May  8 20:25:07 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:07 localhost root: Sun May  8 20:25:07 UTC 2022: I found word, Master!
    systemd: May  8 20:25:07 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:07 localhost systemd: Started Run watchlog script every 30 second.
    systemd: May  8 20:25:09 localhost systemd: Reloading.
    systemd: May  8 20:25:09 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:09 localhost root: Sun May  8 20:25:09 UTC 2022: I found word, Master!
    systemd: May  8 20:25:09 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:11 localhost systemd: Reloading.
    systemd: May  8 20:25:11 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:11 localhost root: Sun May  8 20:25:11 UTC 2022: I found word, Master!
    systemd: May  8 20:25:12 localhost systemd: Started My watchlog service.
    systemd: May  8 20:25:14 localhost systemd: Reloading.
    systemd: May  8 20:25:14 localhost systemd: Starting My watchlog service...
    systemd: May  8 20:25:14 localhost root: Sun May  8 20:25:14 UTC 2022: I found word, Master!
    systemd: May  8 20:25:14 localhost systemd: Started My watchlog service.
```
