```
<IfModule mod_ssl.c>
<VirtualHost *:443>
         ServerAdmin megamindtamizhan@itechki.com
         ServerName itechki.com
         ServerAlias www.itechki.com
         DocumentRoot /var/www/html/itechki/

     <Directory /var/www/html/itechki/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
       SSLEngine on

SSLCertificateKeyFile /etc/apache2/ssl/itechki/private.key
SSLCertificateFile /etc/apache2/ssl/itechki/itechkicert.crt
SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm.crt


#SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
#SSLCertificateFile /etc/apache2/ssl/itechki/itechki.crt
#SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm.crt (Bundle)


</VirtualHost>
</IfModule>
```