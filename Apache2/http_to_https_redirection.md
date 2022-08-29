# HTTP to HTTPS Redirection

### Add the below code inside Virtualhost config file

```
RewriteEngine on
RewriteCond %{SERVER_NAME} =itechki.com [OR]
RewriteCond %{SERVER_NAME} =www.itechki.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
```

### Virtualhost config file - Before Changes

```
<VirtualHost *:80>
     ServerAdmin megamindtamizhan@itechki.com
     DocumentRoot /var/www/html/itechki/
     ServerName itechki.com
     ServerAlias www.itechki.com

     <Directory /var/www/html/itechki/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Virtualhost config file - After Changes

```
<VirtualHost *:80>
     ServerAdmin megamindtamizhan@itechki.com
     DocumentRoot /var/www/html/itechki/
     ServerName itechki.com
     ServerAlias www.itechki.com

     <Directory /var/www/html/itechki/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined

RewriteEngine on
RewriteCond %{SERVER_NAME} =itechki.com [OR]
RewriteCond %{SERVER_NAME} =www.itechki.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

</VirtualHost>
```