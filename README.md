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
1. Download Private Key [here](https://drive.google.com/open?id=1D68yL0jylTFDiywWLQM-zZrW1UAj0qsx) or in this link [here](https://onedrive.live.com/?cid=F5A51A663F940699&id=F5A51A663F940699%21253231&parId=F5A51A663F940699%21109&o=OneUp)
2. Put the private key file into the folder `~/.ssh` (in your local machine).
3. In your terminal:
	`ssh -i ~/.ssh/key grader@3.88.117.25`
4. Type the Passphrase:
  `inter123`

##Private key

if you cant downloded the key above.

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,DFB2B18DFB0CBE660F4A7D0387C96E64

ixyDptJqX7w16niO3CDlUYQELjakF9zicXuY/MI4ypx+0DtlrSpqfHzKw4v29IK4
+d0Hy73o5FtCZoYAz7QsUOc+u4/c3zRj2x+vj8YTBkFyCnleCu3dz6hM1HDq/YgF
nz2/QgjvOFIsj4LNETdUqn68k9kJgNvjd12ai7XU6QPdjFgWWUyLwky3PTfvw5h7
kXC1KTjIIfUw6ITT3NxfXC64HROLQdqoErSeQoYAVmHKxb5QbCmABpdtEtyxSl6n
QqA/fhU6UlLGF6YOGUn0CudR7TnIx/7hAxs1lm7ccDeWzzpJjKRv2AoOpw8DPajD
YTkpqMq77VsRwUlTudVXDX7Bu7nt2oij4DepX3XDPshVK8BQ1JGXpWRjdXMXmopo
7/uxJiew9AyOMlT2j7mnaGCWG+VTPPpkZJzELhm3HrPytcxFt6n5nZfeTt0FVbTZ
VunKAtHJmyeuJdHrrtPM2QHXneRUHQJ/4zQBJOaoe/a7xPbThIJzGnIn4U9KAgR9
78e/z5FlRlcaEx0I1QlM5Uo5RwAsZc0BTophGZPi1uy+pHHIrjEjAni3VDbvQ2nW
doNr2aIzLiUgUQR3DzEcGV8Mo5sZt1h9STrAq6B0wfk2BqPOSDNqIo0HQMJbZFh6
znGeMRX5Qpv5QSBoAxjS2tCojUdOfo9qTaBqak3Bw5w1mlGU13KzMZRVftgpSuww
Lzh6DmZscrS70HP99REJSCG9EHOjaaFTxgyVO0+/vUDREkb+sjIW4iJFb2LubRnk
eMA6+x1jZt0r4wRKIkM4C9sNjQq+Ztkd/4LU2/rw2cwnRNzrZChWW4pkBF9g1leu
Z4NJRf+A0iS74tRhzflTJeOhMcNxoB+E0NdPA2smFOjx5Ei30tsW4KK4cffzCv6L
6PJlcUPkqnK1aDH2Z9vdlGgRFmc25Ha1PzzQut+wTb/95E/VaYQJTx8oCQuAV5dJ
ZFPYHC98QNih6rQxLq7wEV6sZHDrNWi0kN30hM+crtXH52catQI1vpB4G44ga6OT
GAuMDZNvevnBZM9HbLG1tKhnm1dZLJyqhfbZ8AbORqlhkZNNVTZoecckL+n/n9YN
LDD0CX4BLKNpW1kXoHH27Vx00zkxTYvST9GFCitI+UqANEObNNbNyUSbprWrhfey
noHETSG/nAe+aIqfpNwJqhiWJhfnaddoASFprX9ECoItEUtY2xdJvoQA5upKCuvf
80MoJSouPiubh3glqdPl2KexzeiIa9yyhyce4+zTuEiPK4eTy60tm/+6k/Ariu5q
/xVcNhRMMkayCX9n/hzwgFiYCHmoGdUlWIaDUzCH6XVVrUTkIUtpOYTxOcDT2ofI
Ls2TsHuX67GoPG/r3X2dWJoZtVCQc5MER1+ReLCaXD+EFF0A0zXYENMAnYDjRv2a
pvwv3m8JaCiJwFeWtx0DB8T7Yr9fy/vSIq6vr6bSEGCUm6dVky7jShDpUx9qAOww
hsCpIqCWHowD6vRrF6eUFQjxPM187/eSNQTBYy4G2VRRLLIgyHr8ENdk7Z66RqUN
VdmFq/dwF565ddQi87/B5eqLGFu9XJYTQUk1ZTiZVRl6Uqe+O9iPs/+o5epEDaBQ
-----END RSA PRIVATE KEY-----
```


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

## Install git and deploying Catalog App project.
1. Install Git using `sudo apt-get install git`
2. Use `cd /var/www`
3. Create the application directory `sudo mkdir FlaskApp`
4. Move inside this directory using `cd FlaskApp`
5. Clone the Catalog App to the virtual machine `git clone https://github.com/PedroArch/bookstore-catalog.git
6. Rename the project's name `sudo mv ./Item_Catalog_UDACITY ./FlaskApp`
7. Use `cd FlaskApp`
8. Rename `application.py` to `__init__.py` using `sudo mv application.py __init__.py`
9. Edit `database_setup.py`, `__init__.py` and change `engine = create_engine('sqlite:///bookstorecatalog.db')` to `engine = create_engine('postgresql://catalog:password@localhost/catalog')`
10. Install pip `sudo apt-get install python-pip`
11. Use pip to install dependencies `sudo pip install -r requirements.txt`
12. Install psycopg2 `sudo apt-get -qqy install postgresql python-psycopg2`
13. Create database schema `sudo python database_setup.py`
14. Filling the tables `sudo python lotsofbooks.py`

## Configure and Enable a New Virtual Host
1. Create FlaskApp.conf to edit: `sudo nano /etc/apache2/sites-available/FlaskApp.conf`
2. Add the following lines

	```
	<VirtualHost *:80>
		ServerName 3.88.117.25
		ServerAdmin pedrofrancocarvalho@gmail.com
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
1. Create the .wsgi File

	```
	sudo nano /var/www/FlaskApp/flaskapp.wsgi
	```
2. Add the following lines:

	```
	#!/usr/bin/python
	import sys
	import logging
	logging.basicConfig(stream=sys.stderr)
	sys.path.insert(0,"/var/www/FlaskApp/")

	from FlaskApp import app as application
	application.secret_key = 'super_secret_key'
	```

## Restart Apache
 Restart Apache `sudo service apache2 restart `

## Meta

Pedro Carvalho – [@PedrArch](https://twitter.com/PedroArch) – pedrofrancocarvalho@gmail.com

[https://github.com/PedroArch](https://github.com/PedroArch/)

## Contributing

1. Fork it (<https://github.com/PedroArch/Linux-Server-Configuration/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[twitter]:https://twitter.com/PedroArch
[github]:https://github.com/PedroArch
[email]: pedrofrancocarvalho@gmail.com

## References:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

https://github.com/jungleBadger/-nanodegree-linux-server/blob/master/README.md
