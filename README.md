# Linux-Server-Configuration

## Server Ip
http://18.184.87.59

## SSH port 
2200

## Complete URL
http://18.184.87.59/catalog/

## Configuration 
- Cloned the webapp repo in the folder /var/www/flaskApp/items-catalog
- Added the `items-catalog.wsgi` file
```
#!/usr/bin/python2.7
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/flaskApp/items-catalog/")

import databasesetup
from project import app as application
from project import renderToken
application.secret_key = renderToken(32)
```
- Added the Apache configuration file in /etc/apache2/sites-availeble/items-catalog.conf
```
<VirtualHost *:80>
                ServerName 18.184.87.59
                ServerAdmin ciscuypers@gmail.com
                WSGIDaemonProcess project user=www-data group=www-data threads=5 home=/var/www/flaskApp/items-catalog/
                WSGIScriptAlias / /var/www/flaskApp/items-catalog/items-catalog.wsgi
                <Directory /var/www/flaskApp/items-catalog>
                        WSGIProcessGroup project
                        WSGIApplicationGroup %{GLOBAL}
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog /var/www/flaskApp/items-catalog/FlaskApp-error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/FlaskApp-access.log combined
</VirtualHost>
```
- Enabled the site with `sudo a2ensite items-catalog`


## Software Insatalled
### redis 
- sudo apt-get install python-redis
- pip2 install redis
### requests
- sudo apt-get install python-requests
- pip2 install redis
### oauth2client.client
- sudo apt-get install python-oauth2client
- pip2 install oauth2client
### HTTPBasicAuth
- sudo apt-get install python-flask-httpauth
- pip2 install flask-httpauth
### Flask
- sudo apt-get install python-flask
- pip2 install flask
### psycopg2
- sudo apt-get install python-psycopg2
- pip2 install psycopg2-binary
### itsdangerous
- sudo apt-get install python-itsdangerous
- pip2 install itsdangerous
### passlib.apps
- sudo apt-get install python-passlib
- pip2 install passlib
### sqlalchemy
- sudo apt-get install python-sqlalchemy
- pip2 install sqlalchemy flask-sqlalchemy
### postgresql
- sudo apt-get install postgress

## Recources
### Configuration:
https://pythonprogramming.net/basic-flask-website-tutorial/?completed=/practical-flask-introduction/
http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://www.howtoinstall.co/en/ubuntu/trusty/

### WebApp:
https://github.com/ciscu/items-catalog

### Resloving import errors:
https://stackoverflow.com/questions/13329354/flask-mod-wsgi-and-apache-importerror

