# Serviço Apache/2.4.66 (Debian) em Buchenavia #

Roda nesse web Server os seguintes sites:

- service.sugesp.ro.gov.br (GLPI)
- service.sugesp.ro.gov.br/visit (VISIT)

Local de instalação: 
/usr/sbin/apache2  
/usr/lib/apache2  
/etc/apache2  
/usr/share/apache2 


## Conteúdo di DIRETÓRIO /etc/apache2/sites-available ##
### 000-default.conf ###
~~~bash
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        # DocumentRoot /var/www/html
        DocumentRoot /opt/sgp/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
~~~

### visit.conf ###
~~~bash
  Alias /visit /opt/sgp/www/visit

<Directory /opt/sgp/www/visit>
    AllowOverride All
    Require all granted
</Directory>
~~~


### fotografia.conf ###
~~~bash
Alias /fotografia /opt/sgp/www/fotografia

<Directory /opt/sgp/www/fotografia>
    AllowOverride All
    Require all g
~~~


## Conteúdo do DIRETÓRIO /etc/apache2/conf-enabled ##
~~~bash
Alias /glpi /opt/sgp/www/glpi/public
<Directory "/opt/sgp/www/glpi/public">
    AllowOverride All
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^(.*)$ index.php [QSA,L]
    Options -Indexes
    Options -Includes -ExecCGI
    Require all granted

    <IfModule mod_php7.c>
        php_value max_execution_time 600
        php_value always_populate_raw_post_data -1
    </IfModule>

    <IfModule mod_php8.c>
        php_value max_execution_time 600
        php_value always_populate_raw_post_data -1
    </IfModule>
</Directory>

~~~