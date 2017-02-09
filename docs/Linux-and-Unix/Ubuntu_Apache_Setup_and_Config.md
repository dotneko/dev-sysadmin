# Check Version
```
more /etc/issue
```

# Installing LAMP on Ubuntu
- Source: [Installing LAMP on Ubuntu 16.04](https://www.atlantic.net/community/howto/install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04/)

# Install Apache
```
sudo apt-get update
sudo apt-get install apache2

service apache2 status          # Check status
```
- Configuration overview in default page: `/var/www/html/index.html`
- Full documentation in `/user/share/doc/apache2/README.Debian.gz`
- Configuration files in `/etc/apache2`
- Default document root in `var/www/html`; virtual hosts could be made uder `var/www`.

### Restarting, Starting and Stopping
```
sudo /etc/init.d/apache2 restart
sudo /etc/init.d/apache2 stop
sudo /etc/init.d/apache2 start
```
### Configuring Autostart
```
sudo update-rc.d -f apache2 remove
sudo update-rc.d apache2 defaults
```
### Securing Apache Ubuntu
- [Securing Apache Ubuntu](https://www.maketecheasier.com/securing-apache-ubuntu/)

# Installing MySQL
```
sudo apt install mysql-server php7.0-mysql
my_sql_secure_installation                  # Configure secure settings
service mysql status                        # Check status of mysql
```
# Installing PHP
```
sudo apt install php libapache2-mod-php
sudo service apache2 restart
```
- Can create a test php file in `/var/www/html/info.php` and load in html:
```
<?php
phpinfo();
?>
```
