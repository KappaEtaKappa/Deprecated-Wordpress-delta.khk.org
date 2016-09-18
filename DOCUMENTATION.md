# DOCUMENTATION

# Cloning from this repository
This repository lacks two files
.htaccess: you'll need this if you're using apache server
wp-config.php: you can copy this from wp-config-sample.php

# !!!(Do not simply upload wp-config.php because it contains the username and password for your database)

# Basic setup
wp-config.php
You'll need to edit 3 things:
define('DB_NAME', 'NameOfADatabaseForWordpress');
define('DB_USER', 'TheUserNameThatHasAccessToYourDatabase');
define('DB_PASSWORD', 'ThePassword');

Login to http://<website-url>/wp-admin to make changes to the website
You'll have to ask for the username and password

# Update wordpress, Upload pictures, Install themes, Install plugins
You will have to change the user:group for wordpress to auto update itself
There's two script written for this
run ./setForUpdate.sh to change the user:group of the files to allow wordpress to access it
run ./setToNormal.sh to change it back so wordpress can't access certain files

# Moving wordpress
1) You will have to copy the whole wordpress folder to its new repository
2) You will also need to copy the wordpress database to the new repository
3) You need to change some rows in the wp_options table in the wordpress database
4) Run this sql code in the command line to import the database:
	mysql -u <username> -p<password> < <wordpressDatabase.sql>
5) Run this sql code to update some fields in the database
	siteurl: the location you store the wordpress folder
	home: the url of your website

	mysql -u <username> -p<password>
	use <wordpressDatabase>;
	UPDATE wp_options SET option_value = <siteurl> WHERE option_name = 'siteurl';
	UPDATE wp_options SET option_value = <home> WHERE option_name = 'home';

TODO: Write a script to build wordpress 