# Домашнее задание SELinux
<ol> 
  <li> Создать стенд для выполнения домашнего задания
  <li> Запустить nginx 1 способом c помощью переключателей setsebool
  <li> Запустить nginx 2 способом c помощью добавления нестандартного порта в имеющийся тип
  <li> Запустить nginx 3 способом c помощью формирования и установки модуля SELinux
</ol>  

# 1. Создать стенд для выполнения домашнего задания
<ul>
  <p> Развернута VM на базе CentOS-7-x86_64
  <p> Установил nginx 
  <p> yum install nginx
  <p> Изменил стандартные порты nginx 
  <p> sed -ie 's/:80/:4881/g' /etc/nginx/nginx.conf 
  <p> sed -i 's/listen 80;/listen 4881;/' /etc/nginx/nginx.conf  
  <p> Установил audit2why
  <p> yum install policycoreutils-python
</ul>

# 2. Запустить nginx 1 способом c помощью переключателей setsebool
<ul> 
  <p> В логе /var/log/audit/audit.log нашёл информацию об nginx
  <p> Используя утилиту audit2why посмотрел информацию о запрете
  <p> grep 1636489992.273:967 /var/log/audit/audit.log | audit2why
  <p> На основании вывода утилиты изменил параметр nis_enabled и запустил enginx
  <p> setsebool -P nis_enabled on
  <p> systemctl start nginx
  <p> Проверил работу nginx
  <p> systemctl status nginx
  <p> Вывод с терминала находиться здесь https://github.com/sergeyorb/DZ-15_SELinux/blob/main/terminal.txt
  <p> Для выполнения третьего пункта задания изменил параметр nis_enabled 
  <p> setsebool -P nis_enabled off 
</ul>

# 3. Запустить nginx 2 способом c помощью добавления нестандартного порта в имеющийся тип
<ul>
  <p> Нашёл имеющийся тип, для http трафика
  <p> semanage port -l | grep http
  <p> Добавил порт в тип http_port_t и проверил что порт добавился
  <p> semanage port -a -t http_port_t -p tcp 4881
  <p> semanage port -l | grep http_port_t
  <p> Запустил nginx и проверил его работу
  <p> systemctl start nginx
  <p> systemctl status nginx
  <p> Для выполнения четвёртого пункта удалил порт из имеющегося типа 
  <p> semanage port -d -t http_port_t -p tcp 4881
  <p> Вывод с терминала находиться здесь https://github.com/sergeyorb/DZ-15_SELinux/blob/main/terminal.txt  
</ul>

# 4. Запустить nginx 3 способом
<ul>
  <p> Просмотрел логи SELinux относящиеся к nginx
  <p> grep nginx /var/log/audit/audit.log
  <p> С помощью утилиты audit2allow создал модуль разрешающий работу nginx по нестандартному порту
  <p> grep nginx /var/log/audit/audit.log | audit2allow -M nginx
  <p> Применил модуль
  <p> semodule -i nginx.pp
  <p> Запустил nginx и проверил его работу
  <p> systemctl start nginx
  <p> systemctl status nginx
  <p> Вывод с терминала находиться здесь https://github.com/sergeyorb/DZ-15_SELinux/blob/main/terminal.txt  
</ul>
