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

### Step 1 — Create a conf file