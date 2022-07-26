# Домашнее задание SELinux
<ol> 
  <li> Создать стенд для выполнения домашнего задания
  <li> Запустить nginx 1 способом
  <li> Запустить nginx 2 способом
  <li> Запустить nginx 3 способом
  <li> 
  <li> 
  <li> 
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

# 2. Запустить nginx 1 способом
<ul>
  <p>
</ul>

# 3. Запустить nginx 2 способом
<ul>
  <p>
</ul>

# 4. Запустить nginx 3 способом
<ul>
  <p>
</ul>
