# How to add virtual host in Ubuntu 16.04
____
- step one. Content folder. Створимо папку в якій буде контент розміщуватися.
  ```
  sudo mkdir -p /var/www/lucku.less/public_html
```
___
- step two. Access rights. Роздамо потрібні права.
  ```
  sudo chown -R $USER:$USER /var/www/lucku.less/public_html
```
Змінна $USER тримає імя, активного на даний час, користувача
 ```
 sudo chmod -R 755 /var/www
 ````
____
- step three. Create some content. Щоб мати змогу побачити що я начудив - потрібно створити якусь інфу.
```
  subl /var/www/lucku.less/public_html/index.html
```
в відкрившомуся вікні треба вписати щось. Краще це:
```
<html>
  <head>
    <title>Welcome to Example.com!</title>
  </head>
  <body>
    <h1>Success!  The lucku.less virtual host is working!</h1>
  </body>
</html>
```
__
- step four. Creating new host's files. Створюємо конфігурацію хоста. Є така фішка в апача - він по замовчуванню створює файл 000-default.conf його я й скопіюю
```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/lucku.less.conf
```
і відредагуємо його
sudo subl /etc/apache2/sites-available/lucku.less.conf
і зафігачим туди такий контент
```
<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName lucku.less
    ServerAlias www.lucku.less
    DocumentRoot /var/www/lucku.less/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
__
-step five. Swich on the host. Вмикаємо новий хост.
```
sudo a2ensite lucku.less.conf
```
після чого перезапускаємо апач
```
sudo service apache2 restart
```
__
- step six. Host options. Налаштування файла hosts
```
sudo subl /etc/hosts
```
там буде щось типу такої хуйні:
```
127.0.0.1	localhost
127.0.1.1	kucheriavii-HP-255-G5-Notebook-PC
127.111.111.111	example.com
127.0.111.111	test.com
```
добавимо наш хост
```
127.111.111.112	lucku.less
```
###ВАЖЛИВО. Тут в hosts не пробіли, а таби
