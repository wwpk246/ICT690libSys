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


