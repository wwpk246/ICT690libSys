**Created the directory for the cataloging html and php:**

 -cd /var/www/html
 -sudo mkdir cataloging


**Set the user name for the catalog in apache:**

 -sudo htpasswd -c /etc/apache2/.htpasswd 
 -user = libcat
 -pw = test1234


**http://34.23.173.5/cataloging/**

cataloging site
author, book title, publisher, copyright
- if refresh is hit or forn submission duplicates then an identical entry is made to the data
still trying to figure out where this entry got stored so I can delete the duplicate

Figured out how to delete row from database, **mysql> DELETE FROM books WHERE id='12';**
