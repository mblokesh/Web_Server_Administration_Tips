```
<IfModule mod_ssl.c>
<VirtualHost *:443>
         ServerAdmin zahir@itechki.com
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

SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
SSLCertificateFile /etc/apache2/ssl/itechki/itechki2023.crt
SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm2023.crt

#SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
#SSLCertificateFile /etc/apache2/ssl/itechki/itechki.crt
#SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm.crt

</VirtualHost>
</IfModule>


<IfModule mod_ssl.c>
<VirtualHost *:443>
        ServerAdmin zahir@itechki.com
         ServerName remote.itechki.com
         ServerAlias www.remote.itechki.com
         DocumentRoot /var/www/html/remote/

     <Directory /var/www/html/remote/>
       Options Indexes FollowSymLinks MultiViews
      AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
       SSLEngine on

SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
SSLCertificateFile /etc/apache2/ssl/itechki/itechki2023.crt
SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm2023.crt


#SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
#SSLCertificateFile /etc/apache2/ssl/itechki/itechki.crt
#SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm.crt

</VirtualHost>
</IfModule>


<IfModule mod_ssl.c>
<VirtualHost *:443>
         ServerAdmin zahir@itechki.com
         ServerName sap.itechki.com
         ServerAlias www.sap.itechki.com
         DocumentRoot /var/www/html/sap/
     
	 <Directory /var/www/html/sap/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
       SSLEngine on


SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
SSLCertificateFile /etc/apache2/ssl/itechki/itechki2023.crt
SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm2023.crt


#SSLCertificateKeyFile /etc/apache2/ssl/itechki/itechki.key
#SSLCertificateFile /etc/apache2/ssl/itechki/itechki.crt
#SSLCertificateChainFile /etc/apache2/ssl/itechki/itechki.interm.crt


</VirtualHost>
</IfModule>
```