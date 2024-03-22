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

Installing the Apache Web Server

Introduction

In this section, we focus on a fundamental component of the internet's infrastructure: the web server, or alternatively, the HTTP server.

The web server is software that makes websites available. The basic function is to make files accessible on at least one computer to anyone with a web browser. Thus, at a basic level, the web is essentially a world wide file system, and the web browser is essentially a file explorer, like Windows Explorer on Windows or Finder on macOS.

Understanding how an HTTP server functions is crucial for anyone wanting to manage or deploy web services. This session will guide you through installing Apache, one of the most popular web server applications, conducting basic checks to ensure its operation, and creating your first web page.

It's important to understand the basics of an HTTP server, and therefore I ask you to read Apache's Getting Started page before proceeding with the rest of this section. Each of the main sections on that page describe the important elements that make up and serve a website, including:

clients, servers, and URLs
hostnames and DNS
configuration files and directives
web site content
log files and troubleshooting
Installation
Before we install Apache, we need to update our systems first.

sudo apt update
sudo apt -y upgrade
Once the machine is updated, we can install Apache2 using apt. First we'll use apt search to identify the specific package name. I already know that a lot of results will be returned, so I will pipe the apt search command through head to look at the initial results:

apt search apache2 | head
The package that we're interested in happens to be named apache2 on Ubuntu. This package name is not a given. On other distributions, like Fedora, the Apache package is called httpd. To learn more about the apache2 package, we can examine it with the apt show command:

apt show apache2
Once we've confirmed that apache2 is the package that we want, we install it with the apt install command. Press Y to agree to continue after running the command below:

sudo apt install apache2
Basic checks
One thing that makes Apache2, and some other web servers, powerful is the library of modules that extend Apache's functionality. We'll come back to modules soon. For now, we're going to make sure the server is up and running, configure some basic things, and then create a basic web site.

To start, I will use the systemctl command to acquire some info about apache2 and make sure it is enabled and running:

systemctl status apache2
The output shows that apache2 is enabled, which is the default for this software. The systemctl command's use of the term enabled means that the software will start automatically on reboot. However, it may not be running. The output should state that the software is active if it is running.

Creating a web page
Since apache2 is running, let's look at the default web page.

There are two ways we can look at the default web page. We can use a text based web browser or a graphical web browser like Firefox, Chrome, etc.

Text Based Web Browser
There are a number of text based web browsers available. I like w3m because it defaults to Vim keybindings, but many like elinks.

To check the site with w3m, we have to install it first:

sudo apt install w3m
If you want to try elinks, then run sudo apt install elinks.

Once the text based browser is installed, we can visit our default site using its loopback IP address (aka, localhost). From the command line on our server, we can run either of these two commands:

w3m 127.0.0.1
Or:

w3m localhost
We can also get the system's private IP address using the ip a command. This address will begin with the number 10 and look like 10.128.0.99. To use that with w3m from the virtual machine's command line, we run:

w3m 10.128.0.99
If the apache2 installed and started correctly, then you should see the following text at the top of the screen:

Apache2 Ubuntu Default Page
It works!

To exit w3m, press q and then y to confirm exit.

Graphical Browser
To view the default web page using a regular web browser, like Firefox, Chrome, Safari, Edge, or etc., you need to get your server's public IP address. To do that, log into the Google Cloud Console. In the left hand navigation panel, hover your cursor over the Compute Engine link, and then click on VM instances. You should see your External IP address in the table on that page. You can copy that external IP address or simply click on it to open it in a new browser tab. Then you should see the graphical version of the Apache2 Ubuntu Default Page.

Note that most browsers nowadays may try to force HTTPS mode, and they also often hide the protocol from the URL. If your web page is not loading, make sure your URL is http://IP-ADDRESS and not https://IP-ADDRESS.

Please take a moment to read through the text on the default page. It provides important information about where Ubuntu stores configuration files and what those files do, and the document root, which is where website files are stored.

Create a Web Page
Let's create our first web page. The default page described above provides the location of the document root at /var/www/html. Remember that the web is, at its simplest, a filesystem that has been made available to the wide world. The web server is what provides access to part of the filesystem. That point of access is called the document root, which may be on a different location on a different machine, configured to be at a different location than the default, or web servers may also be configured to expose multiple parts of the filesystem to the web.

When we navigate to the document root on the command line, we'll see that there is already an index.html file located in that directory. This is the Apache2 Ubuntu Default Page that we visited above in our browsers. Let's rename that index.html file, and create a new one:

cd /var/www/html/
sudo mv index.html index.html.original
sudo nano index.html
Note: we use sudo in this directory because we are working on files and directories outside our home directories. Thus, be careful here about the commands you run. Any mistake may result in deleting necessary files or directories.

If you know HTML, then feel free to write some basic HTML code to get started. Otherwise, you can re-type the content below in nano, and then save and exit out.

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

You can still view the original default page by specifying its name in the URL. Remember that web browsers are, at their most basic, simply file viewers. So it makes sense that you simply have to specify the name of the file you want to view. For example, if your external IP address is 55.222.55.222, then you'd specify it like so:

http://55.222.55.222/index.html.original
Conclusion
In this section, we learned about the Apache2 HTTP server. We learned how to install it on Ubuntu, how to use a systemctl command to check its status, how to create a basic web page in /var/www/html, how to view that web page using the w3m command line browser and our regular graphical browser,

In the next section, we will install PHP, which will provide the language needed to connect to MySQL, and thus enable more data driven web sites.


----------------------------------------------------------------------------------------

*PHP NOTES*

Installing and Configuring PHP

Introduction

Client-side programming languages, like JavaScript, are handled by the browser. Major browsers like Firefox, Chrome, Safari, Edge, etc. all include JavaScript engines that use just-in-time compilers to execute JavaScript code (Mozilla has a nice description of the process.) From an end user's perspective, you basically install JavaScript when you install a web browser.

PHP, on the other hand, is a server-side programming language, which means it must be installed on the server in order to be used. From a system or web administrator's perspective, this means that not only does PHP have be installed on a server, but it must also be configured to work with the HTTP server, which in our case is Apache2.

The main use of PHP is to interact with databases, like MySQL, MariaDB, PostgreSQL, etc., in order to create data-based page content. To begin to set this up, we have to:

Install PHP and relevant Apache2 modules
Configure PHP and relevant modules to work with Apache2
Configure PHP and relevant modules to work with MySQL
Install PHP
As usual, we will use apt install to install PHP and relevant modules. Then we will restart Apache2 using the systemctl command. Use apt show [package_name] to read more about each package we will install. The first command below installs the php and the libapache2-mod-php packages. The latter package is used to create a connection between PHP and Apache2.

sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
We can check its status and see if there are any errors:

systemctl status apache2
Check Install
To check that it's been installed and that it's working with Apache2, we can create a small PHP file in our web document root. To do that, we cd to the /var/www/html/ directory and create a file called info.php:

cd /var/www/html/
sudo nano info.php
In that file, add the following text, then save and close the file:

<?php
phpinfo();
?>
No visit that file using the external IP address for your server. For example, in Firefox, Chrome, etc, go to:

http://55.333.55.333/info.php
Again, be sure to replace the IP below with the IP address of your server and be sure to use http and not https.

You should see a page that provides system information about PHP, Apache2, and the server. The top of the page should look like Figure 1 below:

PHP install page
Fig. 1. A screenshot of the title of the PHP install page.
Basic Configurations
By default, when Apache2 serves a web page, it looks for and serves a file titled index.html, even if it does not display that file in the URL bar. Thus, http://example.com/ actually resolves to http://example.com/index.html in such cases.

However, if our plan is to provide for PHP, we want Apache2 to default to a file titled index.php instead of index.html file. To configure that, we need to edit the dir.conf file in the /etc/apache2/mods-enabled/ directory. In that file there is a line that starts with DirectoryIndex. The first file in that line is index.html, and then there are a series of other files that Apache2 will look for in the order listed. If any of those files exist in the document root, then Apache2 will serve those before proceeding to the next. We simply want to put index.php first and let index.html be second on that line. Before modifying this file, it's good practice to create a backup of the original. So we will use the cp command to create a copy with a new name, and then we will use nano to edit the file.

cd /etc/apache2/mods-enabled/
sudo cp dir.conf dir.conf.bak
sudo nano dir.conf
Next we change the line to this:

DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
Whenever we make a configuration change, we can use the apachectl command to check our configuration:

apachectl configtest
If we get a Syntax Ok message, we can reload the Apache2 configuration and restart the service:

sudo systemctl reload apache2
sudo systemctl restart apache2
Create an index.php File
Now create a basic PHP page. cd back to the Apache2 document root directory and use nano to create and open an index.php file:

cd /var/www/html/
sudo nano index.php
Let's add some HTML and PHP to it. We will add PHP that functions as a simple browser detector. Add the following code:

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
Next, save the file and exit nano. In your browser, visit your external IP address site (again, replace your server's IP address):

http://55.333.55.333/
Although your index.html file still exists in your document root, Apache2 now returns the index.php file instead. However, if for some reason the index.php was deleted, then Apache2 would revert to the index.html file since that's what is listed next in the dir.conf DirectoryIndex line.

Conclusion
In this section, we installed PHP and configured it work with Apache2. We also created a simple PHP test page that reported our browser user agent information on our website.

In the next section, we'll learn how to complete the LAMP stack by adding the MySQL relational database to our setup.
