# Linux-Server-Configuration-UDACITY
Linux Configuration Project

> In this project, a Linux virtual machine needs to be configurated to support the Item Catalog website.

IP ADDRESS: 3.88.117.25
HTTP ADDRESS: #######

## Tasks
1. Get a server (I used Amazon Lightsail)
2. Secure the server
    * Update and Upgrade all packages
    * Change the SHH port from 22 to 2200
    * Configure the UFW to only allow incomig connections for SSH, HTTP, NTP
4. Give the grader acess with sudo
5. Configure the local timezone to UTC
6. Install and configure Apache to serve a Python mod_wsgi application
7. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
8. Configure the local timezone to UTC
9. Install and configure Apache to serve a Python mod_wsgi application
10. Install and configure PostgreSQL
	 * Do not allow remote connections
	 * Create a new user named catalog that has limited permissions to your catalog application database
11. Deploy the Item Catalog project

## Launch Virtual Machine

## Instructions for SSH access to the instance
1. Download Private Key [here](https://drive.google.com/open?id=1D68yL0jylTFDiywWLQM-zZrW1UAj0qsx)
2. Put the private key file into the folder `~/.ssh` (in your local machine).
3. In your terminal:
	`ssh -i ~/.ssh/key grader@3.88.117.25`
4. Type the Passphrase:
  `inter123`

## Create a new user
1. `sudo adduser grader`
2. `sudo nano /etc/sudoers.d/grader`
4. type in
  `grader ALL=(ALL:ALL) NOPASSWD:ALL`
5.  save and quit

## Set ssh login using keys
1. generate keys on local machine using `ssh-keygen` ; then save the private key in `~/.ssh` on local machine
2. deploy public key on developement enviroment

	On you virtual machine:
  ```
    $ su  grader
	$ mkdir .ssh
	$ sudo nano .ssh/authorized_keys
  ```

	Copy the public key generated on your local machine to this file and save

  ```
	$ sudo chown grader .ssh
    $ chmod 700 .ssh
	$ chmod 644 .ssh/authorized_keys
  ```


3. reload SSH using `service ssh restart`
4. now you can use ssh to login with the new user you created

	`ssh -i [privateKeyFilename] -p 22 grader@3.88.117.25`

## Update and Upgrade all packages

	sudo apt-get update
	sudo apt-get upgrade

## Setting SSH port to 2200
1. Use `sudo nano /etc/ssh/sshd_config` and then insert Port 2200 below to Port 22 , save & quit.
2. Reload SSH using `sudo service ssh restart`

## Configure UFW Firewall

```
	sudo ufw allow 2200/tcp
	sudo ufw allow 80/tcp
	sudo ufw allow 123/udp
	sudo ufw enable
```

## Configure the local timezone to UTC
1. Configure the time zone `sudo dpkg-reconfigure tzdata`
2. set to UTC.

## Install Apache to serve a Python mod_wsgi
1. Install Apache `sudo apt-get install apache2`
2. Install mod_wsgi `sudo apt-get install python-setuptools libapache2-mod-wsgi`
3. Restart Apache `sudo service apache2 restart`

## Install and configure PostgreSQL
1. Install PostgreSQL `sudo apt-get install postgresql`
2. Login as user "postgres" `sudo su postgres`
4. Get into postgreSQL shell `psql`
5. Create a new database and create a new user in postgreSQL

	```
	postgres=# CREATE DATABASE catalog;
	postgres=# CREATE USER catalog;
	```
5. Set a password for user catalog

	```
	postgres=# ALTER ROLE catalog WITH PASSWORD 'password';
	```
6. Give user "catalog" permission to "catalog" application database

	```
	postgres=# GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;
	```
7. Exit from user "postgres" type `exit`

## Install git, clone and setup your Catalog App project.
1. Install Git using `sudo apt-get install git`
2. Use `cd /var/www` to move to the /var/www directory
3. Create the application directory `sudo mkdir FlaskApp`
4. Move inside this directory using `cd FlaskApp`
5. Clone the Catalog App to the virtual machine `git clone https://github.com/kongling893/Item_Catalog_UDACITY.git`
6. Rename the project's name `sudo mv ./Item_Catalog_UDACITY ./FlaskApp`
7. Move to the inner FlaskApp directory using `cd FlaskApp`
8. Rename `website.py` to `__init__.py` using `sudo mv website.py __init__.py`
9. Edit `database_setup.py`, `website.py` and `functions_helper.py` and change `engine = create_engine('sqlite:///toyshop.db')` to `engine = create_engine('postgresql://catalog:password@localhost/catalog')`
10. Install pip `sudo apt-get install python-pip`
11. Use pip to install dependencies `sudo pip install -r requirements.txt`
12. Install psycopg2 `sudo apt-get -qqy install postgresql python-psycopg2`
13. Create database schema `sudo python database_setup.py`

## Configure and Enable a New Virtual Host
1. Create FlaskApp.conf to edit: `sudo nano /etc/apache2/sites-available/FlaskApp.conf`
2. Add the following lines of code to the file to configure the virtual host.

	```
	<VirtualHost *:80>
		ServerName ec2-18-216-71-137.compute-1.amazonaws.com
		ServerAdmin danielpaladar@gmail.com
		WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
		<Directory /var/www/FlaskApp/FlaskApp/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/FlaskApp/FlaskApp/static
		<Directory /var/www/FlaskApp/FlaskApp/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>
	```
3. Enable the virtual host with the following command: `sudo a2ensite FlaskApp`

## Create the .wsgi File
1. Create the .wsgi File under /var/www/FlaskApp:

	```
	cd /var/www/FlaskApp
	sudo nano flaskapp.wsgi
	```
2. Add the following lines of code to the flaskapp.wsgi file:

	```
	#!/usr/bin/python
	import sys
	import logging
	logging.basicConfig(stream=sys.stderr)
	sys.path.insert(0,"/var/www/FlaskApp/")

	from FlaskApp import app as application
	application.secret_key = 'Add your secret key'
	```

## Restart Apache
1. Restart Apache `sudo service apache2 restart `

## References:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
