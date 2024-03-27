**Created the directory for the cataloging html and php:**

 -cd /var/www/html
 -sudo mkdir cataloging


**Set the user name for the catalog in apache:**

 -sudo htpasswd -c /etc/apache2/.htpasswd 
 -user = libcat
 -pw = ********


**http://34.23.173.5/cataloging/**

cataloging site
author, book title, publisher, copyright
- if refresh is hit or forn submission duplicates then an identical entry is made to the data
still trying to figure out where this entry got stored so I can delete the duplicate

Figured out how to delete row from database, **mysql> DELETE FROM books WHERE id='12';**



---**CLASS NOTES**---

Cataloging Module:


-contain four fields similar to books table in MYSQL:
author
title
publisher
copyright

-create new directory:
cd /var/www/html
sudo mkdir cataloging

-create index.html and add content:
cd cataloging
sudo nano index.html

-add below text:
<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>

-add php:
insert.php, referenced in HTML:

<?php

// Load MySQL credentials
require_once '../login.php';

// Establish connection
$conn = mysqli_connect($db_hostname, $db_username, $db_password) or
  die("Unable to connect");

// Open database
mysqli_select_db($conn, $db_database) or
  die("Could not open database '$db_database'");

// Prepare and bind SQL statement
$stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
$stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

// Set parameters and execute statement
$author = $_POST["author"];
$title = $_POST["title"];
$publisher = $_POST["publisher"];
$copyright = $_POST["copyright"];

if ($stmt->execute() === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->error;
}

// Close statement and connection
$stmt->close();
$conn->close();

echo "<p>Return to the cataloging page: <a href='http://11.111.111.111/cataloging/'>http://11.111.111.111/cataloging/</a></p>";
?>

-Security
Apache2 server uses password protection called htpasswd.

-create a hashed password and username. username will be libcat for this purpose:
sudo htpasswd -c /etc/apache2/.htpasswd libcat
"Next we need to tell the Apache2 web server that we will use the htpasswd to control access to our cataloging module. To do that, we use nano to open the apache2.conf file. We need

sudo nano /etc/apache2/apache2.conf
In the apache2.conf file, look for the following code block / stanza. We are interested in the third line in the stanza, which is line 172 for me, and probably is for you, too.

<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride None
  Require all granted
</Directory>
Carefully, we need to change the word None to the word All:

<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
Next, change to the cataloging directory and use nano to create a file called .htaccess (note the leading period):

cd /var/www/html/cataloging
sudo nano .htaccess
Add the following content to .htaccess:

AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
Check that the configuration file is okay:

apachectl configtest
If you get a Syntax OK message, then restart Apache2 and check its status:

sudo systemctl restart apache2
systemctl status apache2
Permissions and Ownership
The Apache2 web server has a user account on your Linux server. The account name is www-data, and it's account details are stored in the /etc/passwd file:

grep "www-data" /etc/passwd
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
From the output, we can see that the www-apache user's home directory is /var/www and its default shell is /usr/sbin/nologin. See man nologin for details, but in short, the nologin prevents the www-data account to be able to login to a shell."

-usegrep $USER /etc/passwd to see root user's default password access set to bash

-limit file permissions for the libcat user:
"Change the group ownership of /var/www/html to www-data:
sudo chown :www-data /var/www/html
Set the setgid bit on /var/www/html. This command makes it so that any new files and directories created within /var/www/html will inherit the group ownership of the parent directory (www-data, in this case). While this ensures that group ownership is inherited, the user ownership of new files will still be the user that creates the files. In our case, since we use sudo to work in this directory, that means that the user owner for subsequent files and directories will be the Linux root user.

sudo chmod -R g+s /var/www/html"
Now time to add entries to the catalog module


