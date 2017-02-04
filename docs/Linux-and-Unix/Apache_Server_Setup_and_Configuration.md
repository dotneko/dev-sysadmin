# Resources
- [Apache HTTP Server Version 2.4 Documentation](http://httpd.apache.org/docs/2.4/)
- [Oracle Docs: Apache Web Server](https://docs.oracle.com/cd/E53394_01/html/E54831/gnvhs.html)

# Apache on Oracle Solaris 11.3
- By default apache22 is installed but disabled. One can check using either of the following:
```
svcs *apache*       # Or:
svcs http
```
- To enable default apache22 service if currently disabled.
```
svcadm enable svc:/network/http:apache22
```
- Can install newer version then enable the server.
```
pkg install web/server/apache-24
svcadm -v enable /network/http:apache24
```
- Alternately can install a Apache webserver with MySQL and PHP:
```
pkg install group/feature/amp
```
- Verify that webserver works by opening: `http://localhost:80` in browser.

# Configuring Apache
- Configuration is stored in the `/etc/apache2/2.2/httpd.conf` file.
- By default, web pages are served from `/var/apache2/2.2/htdocs` folder.

### Edit `/etc/apache2/2.2/httpd.conf`

- Can edit `DocumentRoot` to point to another directory.
- Make sure to change the <Directory ""> to point to the same DocumentRoot
- Also need to make sure that the directory it points into to has execute permissions, otherwise others won't be able to read the files within the directory.

### Directives in `httpd.conf`
```
Allow from <address>        # <address> is IP address or fully qualified domain name
Deny from <address>
```
- Using `Order` allows one to fine-tune the access:
```
Order deny,allow            # Specifies restriction order
Deny from all
Allow from some.host.com
```
- The above example will by default deny access to all, and then only allow access from some.host.com.

# Setting up Virtual Hosts in Apache
- One can examine `/etc/apache2/2.2/samples-conf.d/vhosts.conf` to show examples of VirtualHost configuration tags that should be added to the `/etc/apache2/2.2/httpd.conf` file.

### Edit the `/etc/apache2/2.2/httpd.conf` file:

- Comment out the default `DocumentRoot "..."`
- Add the following to direct queries to the specified DocumentRoot:

```
Listen 80                   # Check that Apache listens on this port (default)

NameVirtualHost *:80        # Allows for name based virtual hosts

<VirtualHost *:80>
    DocumentRoot "/path/directory"
    ServerName www.host.name
</VirtualHost>
```

- Next, need to give access through Apache to the specified directory by adding:

```
<Directory "/path/directory">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

Also ensure the `/etc/inet/hosts` file is configured to resolve the ServerName (note that `/etc/hosts` symbolically links to `/etc/inet/hosts`):

```
192.168.1.123 www.host.name     # Assigns 192.168.1.123 to www.host.name
```

## Additional steps for virtual hosts on different ports

Assuming the above virtual host is created, we add another virtual host that runs on a different port:

```
Listen 8123

<VirtualHost *:8123>
    DocumentRoot "/path/anotherDirectory"
</VirtualHost>

<Directory "/path/anotherDirectory">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>

```


# Configuring Authentication and Authorization
- [Authentication and Authorization for version 2.2 from apache.org](http://httpd.apache.org/docs/2.2/howto/auth.html)
- Create a password file (not accessible from the web) using `htpasswd`.
- Note that `htpasswd` is located at `/usr/local/apache2/bin/htpasswd`
- E.g. `htpasswd -c /usr/local/apache/passwd/passwords user_name`
- Then configure the server to request the password by editing the `httpd.conf` file or using an `.htaccess` file:
```
AuthType Basic
AuthName "Restricted Files"
# (Following line optional)
AuthBasicProvider file
AuthUserFile /usr/local/apache/passwd/passwords
Require user user_name
```
- So to protect a folder `/pathto/secret`:
    - Place the above directives in `.htaccess` within the folder `/pathto/secret`.
    - Alternatively, place the above directives in the `httpd.conf` file within a directory section: `<Directory /pathto/secret> ... </Directory>`
