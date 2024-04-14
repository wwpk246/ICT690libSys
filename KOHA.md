**-NEW VM MACHINE**
Series= E2
Machine Type= 2 vCPU, 4 GB memory, Ubuntu 20.04

**-VPC NETWORKS->FIREWALLS**
create firewall _rule_
name= koha
port= 8080
For TCP ports, add 8080


**UPDATE SERVER**
-sudo apt update / upgrade

**Next was updating repository for Koha and Koha installation, installation of MYSQL**
```
sudo su
echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list
wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -
apt install koha-common
nano /etc/koha/koha-sites.conf
INTRAPORT="80" -> INTRAPORT="8080"
apt install mysql-server
mysqladmin -u root password xxxxxxxxx
```

**Allow apache rewrite ability**

a2enmod rewrite
a2enmod cgi 
systemctl restart apache2


**CREATE DB FOR KOHA**
koha-create --create-db bibliolib
nano /etc/apache2/ports.conf -> "add" Listen 8080
//check config -> apachectl configtest





