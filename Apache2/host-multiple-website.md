# How to Host Multiple Websites with Apache Virtual Hosts

### Introduction

Apache’s virtual hosts can run multiple websites on a single server. In this article, you will learn how to host multiple websites including sub-domains.

My Ubuntu 21.04 server has some files in the /etc/apache2/sites-available directory. We will create more files in this directory to create multiple virtual hosts.

```
$ ls /etc/apache2/sites-available
000-default.conf       000-default-ssl.conf  
```
### Creating a new virtual host

Let’s create a virtual host for `example.com`. (You need to change example.com to your domain name.) We store files in the /var/www/example.com/public_html directory.

#### Step 1 — Create a conf file

Copy `000-default.com.conf` to create a new file in `/etc/apache2/sites-available`:

```
$ cd /etc/apache2/sites-available
$ sudo cp 000-default.com.conf example.com.conf
```
#### Step 2 — Modify the new conf file

In the `example.com.conf`:

```
<VirtualHost *:80>
    ServerAdmin your.email@gmail.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com/public_html
    <Directory /var/www/example.com/public_html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <IfModule mod_dir.c>
        DirectoryIndex index.php index.pl index.cgi index.html index.xhtml index.htm
    </IfModule>
</VirtualHost>
```
**Line 2: Add your email for ServerAdmin**
**Line 3: Use your domain name for ServerName.**
**Line 4: Add www to your domain name for ServerAlias.**
**Line 5 & 6: Add the file directory for DocumentRoot.**

#### Step 3 — Enabling a virtual host

`a2ensite` enables the specified site within the `apache2` configuration. It creates a symlink within `/etc/apache2/sites-enabled` (not sites-available).

`$ sudo a2ensite example.com.conf`

The above command will create a symlink, `example.com.conf`, within the `/etc/apache2/sites-enabled` directory.

#### Step 4— Enabling SSL

Create the `/etc/certificate` folder to save both the **certificate** and the **private key** in it:

`$ sudo mkdir /etc/certificate`

Modify the SSL configuration of the Virtual Host of the domain you want to protect with SSL connection. In this tutorial the SSL configuration of the default Apache Virtual Host will be used, as an example.

Open the Virtual Host SSL configuration:

`$ sudo nano /etc/apache2/sites-available/default-ssl.conf`

You'll find a file structured as follows :

```
<IfModule mod_ssl.c>
            <VirtualHost _default_:443>
                    ServerAdmin webmaster@localhost
                    DocumentRoot /var/www/html
                    ErrorLog ${APACHE_LOG_DIR}/error.log
                    CustomLog ${APACHE_LOG_DIR}/access.log combined
                    SSLEngine on
                    SSLCertificateFile      /etc/certificate/ssl-cert-example.pem
                    SSLCertificateKeyFile /etc/certificate/ssl-cert-example.key
                    <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                    SSLOptions +StdEnvVars
                    </FilesMatch>
                    <Directory /usr/lib/cgi-bin>
                                    SSLOptions +StdEnvVars
                    </Directory>
            </VirtualHost>
    </IfModule>
```

Set up the ServerAdmin directive correctly by entering your email and add the ServerName directive followed by your domain or your server's IP address.

Finally, change the path indicated by the SSLCertificateFile and SSLCertificateKeyFile directives, entering respectively the path of your certificate and private key .

You will get a result similar to the following :

Then save and close the file.

Site available creating a symbolic link:

`sudo a2ensite default-ssl.conf`

Now we install the SSL mod for apache, this instruction pre configure the file /etc/apache2/ports.conf with some line and the important one that say Listen 443.

`sudo a2enmod ssl`

#### Step 5— Restart apache

`$ sudo systemctl restart apache2`

If your DNS is configured correctly, you should be able to see your domain.

### Subdomains

We are going to create a virtual host for a subdomain. The process is the same as in the previous section.

We store web files within `/var/www/newsletter.example.com/public_html`

We copy `000-default.com.conf` to create a new file `newsletter.example.com.conf`.

`$ sudo cp 000-default.com.conf newsletter.example.com.conf`

Edit the `newsletter.example.com.conf`:

```
<VirtualHost *:80>
    ServerAdmin your.email@gmail.com
    ServerName newsletter.example.com
    ServerAlias www.newsletter.example.com
    DocumentRoot /var/www/newsletter.example.com/public_html
    <Directory /var/www/newsletter.example.com/public_html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <IfModule mod_dir.c>
        DirectoryIndex index.php index.pl index.cgi index.htmt index.xhtml index.htm
    </IfModule>
</VirtualHost>
```

The differences from the previous one are adding a subdomain to the ServerName, ServerAlias, DocumentRoot, and Directory.

#### Enabling a virtual host and SSL

#### Adding A record to your DNS service

If you are using godaddy.com, go to Domain > DNS Manage and add a new record.

Set Custom TTL (600 Sec). It may take 10–15 minutes.