**Check and install updates**
1. sudo apt update
2. sudo apt -y upgrade

**Sort through search results for the initial matches**
1. apt search apache2 | head

**Check apache status**
1. systemctl status apache2

**Install the text web page editor**
1. sudo apt install w3m

**Visiting the default home page**
1. w3m localhost or 
2. w3m 127.0.0.1


**Exitng w3m:To exit w3m, press q and then y to confirm exit**


**Switching to the directory and making a new default page**
1. cd /var/www/html/
2. sudo mv index.html index.html.original
3. sudo nano index.html

**Basic html for the default site:**
<html>
<head>
<title>My first web page using Apache2</title>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my web site.
I created this site using the Apache2 HTTP server.</p>

</body>
</html>


**Created a browser detector in PHP:**
<html>
<head>
<title>Broswer Detector</title>
</head>
<body>
<p>You are using the following browser to view this site:</p>

<?php
$user_agent = $_SERVER['HTTP_USER_AGENT'];

if(strpos($user_agent, 'Edge') !== FALSE) {
    $browser = 'Microsoft Edge';
} elseif(strpos($user_agent, 'Firefox') !== FALSE) {
    $browser = 'Mozilla Firefox';
} elseif(strpos($user_agent, 'Chrome') !== FALSE) {
    $browser = 'Google Chrome';
} elseif(strpos($user_agent, 'Opera Mini') !== FALSE) {
    $browser = "Opera Mini";
} elseif(strpos($user_agent, 'Opera') !== FALSE) {
    $browser = 'Opera';
} elseif(strpos($user_agent, 'Safari') !== FALSE) {
    $browser = 'Safari';
} else {
    $browser = 'Unknown';
}

if(strpos($user_agent, 'Windows') !== FALSE) {
    $os = 'Windows';
} elseif(strpos($user_agent, 'Linux') !== FALSE) {
    $os = 'Linux';
} elseif(strpos($user_agent, 'Mac') !== FALSE) {
    $os = 'Mac';
} elseif(strpos($user_agent, 'iOS') !== FALSE) {
    $os = 'iOS';
} elseif(strpos($user_agent, 'Android') !== FALSE) {
    $os = 'Android';
} else {
    $os = 'Unknown';
}

if($browser === 'Unknown' || $os === 'Unknown') {
    echo 'No browser detected.';
} else {
    echo 'Your browser is ' . $browser . ' and your operating system is ' . $os . '.';
}
?>

</body>
</html>


**MYSQL
**Create a database, add access to the opac user and then show list of databases:**
1. create database opacdb;
2. grant all privileges on opacdb.* to 'opacuser'@'localhost';
3. show databases;

**Found this to be very helpful:
Reminder: each MySQL command ends with a semi-colon. Some of the following MySQL commands are single-line, but others are multi-line. 
Regardless if a MySQL command is one-line or multi-line, it doesn't end until it ends with a semi-colon:


-------------------------------------------------------------------------------------------------------------


**CLASS NOTES**

How to install Apache Web Server while applying updates:

sudo apt update
sudo apt -y upgrade

apt search apache2 | head

apt show apache2 //adds more info about this package

sudo apt install apache2

--Basic checks--

Check apache status, is it enabled and running:

systemctl status apache2
-enabled = will run on reboot

--Creating a web page--

Text Based Web Browser w3m installation:

sudo apt install w3m

Run one of these to view the browser output:

w3m 127.0.0.1
Or:
w3m localhost

"We can also get the system's private IP address using the ip a command. This address will begin with the number 10 and look like 10.128.0.99. To use that with w3m from the virtual machine's command line, we run:

w3m 10.128.0.99

Apache2 Ubuntu Default Page
It works!

To exit w3m, press q and then y to confirm exit."

--Graphical Browser--

Use only http and not https as not supported: http://IP-ADDRESS and not https://IP-ADDRESS.

--Create a Web Page--

"When we navigate to the document root on the command line, we'll see that there is already an index.html file located in that directory. This is the Apache2 Ubuntu Default Page that we visited above in our browsers. Let's rename that index.html file, and create a new one:

cd /var/www/html/
sudo mv index.html index.html.original
sudo nano index.html
Note: we use sudo in this directory because we are working on files and directories outside our home directories. Thus, be careful here about the commands you run. Any mistake may result in deleting necessary files or directories."


Text to input:

<html>
<head>
<title>My first web page using Apache2</title>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my web site.
I created this site using the Apache2 HTTP server.</p>

</body>
</html>
If you have your site open in your web browser, reload the page, and you should see the new text.

* //http://55.222.55.222/index.html.original - this is an example of the URL used to view the original index.html page before modifying it.
* 


----------------------------------------------------------------------------------------

*PHP NOTES*

Installing and Configuring PHP

Steps to install PHP within the commandline and get everything running:

Install PHP and relevant Apache2 modules
Configure PHP and relevant modules to work with Apache2
Configure PHP and relevant modules to work with MySQL
Install PHP

sudo apt install php libapache2-mod-php
sudo systemctl restart apache2

check its status and errors:

systemctl status apache2

Check Install and create a php file:
cd to the /var/www/html/ directory and create a file called info.php:

cd /var/www/html/
sudo nano info.php

Add the following text to the php file, save and exit:

<?php
phpinfo();
?>

http://55.333.55.333/info.php
^ example, replace with google cloud external IP and use http.

create a backup of the original:

cd /etc/apache2/mods-enabled/
sudo cp dir.conf dir.conf.bak
sudo nano dir.conf

-Next we change the line to this:

DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

check our configuration in apache:

apachectl configtest
Syntax Ok message, then restart:

sudo systemctl reload apache2
sudo systemctl restart apache2
Create an index.php File
cd to the Apache2 document root directory and use nano to create and open an index.php file:

cd /var/www/html/
sudo nano index.php

add HTML and PHP to the index.php file:

<html>
<head>
<title>Broswer Detector</title>
</head>
<body>
<p>You are using the following browser to view this site:</p>

<?php
$user_agent = $_SERVER['HTTP_USER_AGENT'];

if(strpos($user_agent, 'Edge') !== FALSE) {
    $browser = 'Microsoft Edge';
} elseif(strpos($user_agent, 'Firefox') !== FALSE) {
    $browser = 'Mozilla Firefox';
} elseif(strpos($user_agent, 'Chrome') !== FALSE) {
    $browser = 'Google Chrome';
} elseif(strpos($user_agent, 'Opera Mini') !== FALSE) {
    $browser = "Opera Mini";
} elseif(strpos($user_agent, 'Opera') !== FALSE) {
    $browser = 'Opera';
} elseif(strpos($user_agent, 'Safari') !== FALSE) {
    $browser = 'Safari';
} else {
    $browser = 'Unknown';
}

if(strpos($user_agent, 'Windows') !== FALSE) {
    $os = 'Windows';
} elseif(strpos($user_agent, 'Linux') !== FALSE) {
    $os = 'Linux';
} elseif(strpos($user_agent, 'Mac') !== FALSE) {
    $os = 'Mac';
} elseif(strpos($user_agent, 'iOS') !== FALSE) {
    $os = 'iOS';
} elseif(strpos($user_agent, 'Android') !== FALSE) {
    $os = 'Android';
} else {
    $os = 'Unknown';
}

if($browser === 'Unknown' || $os === 'Unknown') {
    echo 'No browser detected.';
} else {
    echo 'Your browser is ' . $browser . ' and your operating system is ' . $os . '.';
}
?>

</body>
</html>
Next, save the file and exit nano. 

View in graphical browser via external IP:
http://55.333.55.333/


