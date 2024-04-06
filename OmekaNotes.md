**Create mysql user and db
1. mysql> create user 'omekauser'@'localhost' identified by 'txxxxxxxx4';
2. mysql> create database omekadb;
3. mysql> grant all privileges on omekadb.* to 'omekauser'@'localhost';
4. within the db.ini file for Omeka:
```
[database]
host     = "localhost"
username = "omekauser"
password = "txxxxxxxx4"
dbname   = "omekadb"
prefix   = "omeka_"
charset  = "utf8"
;port     = ""
```

**Install Omeka
1. willw@wwubuntu-1:/var/www/html$ sudo wget https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
2. willw@wwubuntu-1:/var/www/html$ ls
```
cataloging           index.php      login.php        opac.php
index.html           info.php       mylibrary.html   search.php
index.html.original  latest.tar.gz  omeka-3.1.2.zip  wordpress
```

3. willw@wwubuntu-1:/var/www/html$ sudo apt install unzip
4. willw@wwubuntu-1:/var/www/html$ unzip omeka-3.1.2.zip
5. willw@wwubuntu-1:/var/www/html$ sudo mv omeka-3.1.2 omeka
6. willw@wwubuntu-1:/var/www/html$ ls
```
cataloging           index.php      login.php       omeka-3.1.2.zip  wordpress
index.html           info.php       mylibrary.html  opac.php
index.html.original  latest.tar.gz  omeka           search.php
```

7. willw@wwubuntu-1:/var/www/html/omeka$ sudo nano db.ini
8. revisit #4 above ^
9. after finishing step #4 above restart apache and mysql:
```sudo systemctl restart apache2```
```sudo systemctl restart mysqld```
