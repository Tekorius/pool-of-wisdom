# Configuring a new PHP machine

Here we will assume that you just started with a new
DigitalOcean droplet.

**Operating System:** Ubuntu 18.04

## Step 1: Non-root User

Add a non-root user and assign him as sudoer. Let's call him deploy.
Partially adapted from [this guide](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04)

    adduser deploy

Do all the passwords and stuff. Now assign sudo rights

    usermod -aG sudo deploy

Now switch to your new user

    su deploy

## Step 2: Upgrade the Packages

With your `deploy` user, use these commands

    sudo apt update
    sudo apt upgrade

## Step 3: CSF

Chinese bots are going crazy, step zero is to only allow your
IP address to SSH to the server.

[Install and configure CSF](csf.md)

## Step 4: Install Apache

Partially adapter from [this guide](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04)

    sudo apt install apache2

Now go to your IP and check that Apache is installed

## Step 5: Install MariaDB

Search for a stable version in [MariaDB Website](https://downloads.mariadb.org/)

You can find Debian/Ubuntu instructions [here](https://mariadb.com/kb/en/library/installing-mariadb-deb-files/)

Use [repository configuration tool](https://downloads.mariadb.org/mariadb/repositories/)
to configure your repository.

## Step 6: Install PHP

Ubuntu 18.04 comes with PHP 7.2 by default at the time of writing,
which is super awesome. All you need to do is type

    sudo apt install php

And it should install automagically.

You may also want to install these modules depending on your
requirements:

* php-pear
* php-fpm
* php-dev
* php-zip
* php-curl
* php-xmlrpc
* php-gd
* php-mysql
* php-mbstring
* php-xml
* libapache2-mod-php

Here's a quick copy-paste line to install some of those modules

    sudo apt install php-fpm php-zip php-curl php-gd php-mysql php-xml libapache2-mod-php

## Step 7: Configure Your Site

Go to `/var/www` and create a folder with your website

    cd /var/www
    mkdir app.mysite.com
