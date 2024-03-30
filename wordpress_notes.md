**WORDPRESS**

This week required checking versions of mysql and php:
- php --version
- mysql --version


This required a restart of several services:
- sudo systemctl restart apache2
- sudo systemctl restart mysql


Install wordpress:
- cd /var/www/html
- sudo wget https://wordpress.org/latest.tar.gz
- sudo tar -xzvf latest.tar.gz


Where to define the wordpress .php:
- cd /var/www/html/wordpress
- sudo cp wp-config-sample.php wp-config.php
- sudo nano wp-config.php


We also changed file ownership and had the ability to change the wordpress file title via from the default "wordpress" to something else:
- sudo mv /var/www/html/wordpress /var/www/html/blog


I always found wordpress a struggle as the amount of customization via simple blocks of entry when I was used to working with them in html or css sheets.  
Obviously this should be easier without the code required but I did not find that the case.
- The images I grabbed for the pages came from a free image site: https://www.dreamstime.com/free-it-computer-images-photos-freecat108
