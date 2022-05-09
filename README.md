# systemd

## Задание 
1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/sysconfig).
2. Из репозитория epel установить spawn-fcgi и переписать init-скрипт на unit-файл (имя service должно называться так же: spawn-fcgi).
3. Дополнить unit-файл httpd (он же apache) возможностью запустить несколько инстансов сервера с разными конфигурационными файлами. 
4*. Скачать демо-версию Atlassian Jira и переписать основной скрипт запуска на unit-файл.

## Решение 

### 1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/sysconfig).
Решение представленно в виде shell скрипта при развертывании машины командой "vagrant up", используемые файлы находятся в директории st1 и копируются на сервер. В качестве ключа используется "ALERT".

```
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

### 2. Из репозитория epel установить spawn-fcgi и переписать init-скрипт на unit-файл (имя service должно называться так же: spawn-fcgi).

Решение представлено в виде shell скрипта в Vagrantfile. Используемые файлы находятся в директории st2. 

```
    systemd: Loaded plugins: fastestmirror
    systemd: Loading mirror speeds from cached hostfile
    systemd:  * base: centos-mirror.rbc.ru
    systemd:  * epel: ftp.lysator.liu.se
    systemd:  * extras: mirror.reconn.ru
    systemd:  * updates: mirror.reconn.ru
    systemd: Package epel-release-7-14.noarch already installed and latest version
    systemd: Nothing to do
    systemd: Loaded plugins: fastestmirror
    systemd: Loading mirror speeds from cached hostfile
    systemd:  * base: centos-mirror.rbc.ru
    systemd:  * epel: mirror.nsc.liu.se
    systemd:  * extras: mirror.reconn.ru
    systemd:  * updates: mirror.reconn.ru
    systemd: Package spawn-fcgi-1.6.3-5.el7.x86_64 already installed and latest version
    systemd: Package php-5.4.16-48.el7.x86_64 already installed and latest version
    systemd: Package php-cli-5.4.16-48.el7.x86_64 already installed and latest version
    systemd: Package mod_fcgid-2.3.9-6.el7.x86_64 already installed and latest version
    systemd: Package httpd-2.4.6-97.el7.centos.5.x86_64 already installed and latest version
    systemd: Nothing to do
    systemd: ● spawn-fcgi.service - Spawn-fcgi startup service by Otus
    systemd:    Loaded: loaded (/etc/systemd/system/spawn-fcgi.service; disabled; vendor preset: disabled)
    systemd:    Active: active (running) since Mon 2022-05-09 14:01:24 UTC; 45s ago
    systemd:  Main PID: 3045 (php-cgi)
    systemd:    CGroup: /system.slice/spawn-fcgi.service
    systemd:            ├─3045 /usr/bin/php-cgi
    systemd:            ├─3047 /usr/bin/php-cgi
    systemd:            ├─3048 /usr/bin/php-cgi
    systemd:            ├─3049 /usr/bin/php-cgi
    systemd:            ├─3050 /usr/bin/php-cgi
    systemd:            ├─3051 /usr/bin/php-cgi
    systemd:            ├─3052 /usr/bin/php-cgi
    systemd:            ├─3053 /usr/bin/php-cgi
    systemd:            ├─3054 /usr/bin/php-cgi
    systemd:            ├─3055 /usr/bin/php-cgi
    systemd:            ├─3056 /usr/bin/php-cgi
    systemd:            ├─3057 /usr/bin/php-cgi
    systemd:            ├─3058 /usr/bin/php-cgi
    systemd:            ├─3059 /usr/bin/php-cgi
    systemd:            ├─3060 /usr/bin/php-cgi
    systemd:            ├─3061 /usr/bin/php-cgi
    systemd:            ├─3062 /usr/bin/php-cgi
    systemd:            ├─3063 /usr/bin/php-cgi
    systemd:            ├─3064 /usr/bin/php-cgi
    systemd:            ├─3065 /usr/bin/php-cgi
    systemd:            ├─3066 /usr/bin/php-cgi
    systemd:            ├─3067 /usr/bin/php-cgi
    systemd:            ├─3068 /usr/bin/php-cgi
    systemd:            ├─3069 /usr/bin/php-cgi
    systemd:            ├─3070 /usr/bin/php-cgi
    systemd:            ├─3071 /usr/bin/php-cgi
    systemd:            ├─3072 /usr/bin/php-cgi
    systemd:            ├─3073 /usr/bin/php-cgi
    systemd:            ├─3074 /usr/bin/php-cgi
    systemd:            ├─3075 /usr/bin/php-cgi
    systemd:            ├─3076 /usr/bin/php-cgi
    systemd:            ├─3077 /usr/bin/php-cgi
    systemd:            └─3078 /usr/bin/php-cgi
    systemd:
    systemd: May 09 14:01:24 systemd systemd[1]: Started Spawn-fcgi startup service by Otus.
```

### 3. Дополнить unit-файл httpd (он же apache) возможностью запустить несколько инстансов сервера с разными конфигурационными файлами. 

Решение представленно в виде скрипта в Vagrantfile. Используемые файлы находятся в директории st3.

```
    systemd: Результат третьего задания
    systemd: tcp    LISTEN     0      128    [::]:8080               [::]:*                   users:(("httpd",pid=3124,fd=4),("httpd",pid=3123,fd=4),("httpd",pid=3122,fd=4),("httpd",pid=3121,fd=4),("httpd",pid=3119,fd=4),("httpd",pid=3118,fd=4),("httpd",pid=3117,fd=4))
    systemd: tcp    LISTEN     0      128    [::]:8082               [::]:*                   users:(("httpd",pid=3135,fd=4),("httpd",pid=3134,fd=4),("httpd",pid=3131,fd=4),("httpd",pid=3130,fd=4),("httpd",pid=3129,fd=4),("httpd",pid=3128,fd=4),("httpd",pid=3127,fd=4))
    systemd: =======================================================
```
