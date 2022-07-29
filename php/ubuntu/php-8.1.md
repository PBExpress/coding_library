# PHP 8.1



### How to Upgrade or from PHP 7.x to PHP 8 on Ubuntu (Apache)

PHP 8.0 is a major update of the PHP language released on November 26, 2020. It contains many new features and optimizations. In this guide we will upgrade from PHP 7.x to PHP 8 on Ubuntu.

### Prerequisites

You must back up your server before running these commands as they cannot be reversed. If you are on cloud hosting, make sure you image your instance before running any of these commands. You have been warned!

To find out which version of PHP you are currently using, run:

```bash
php -v
```

If you are running PHP 7.x, you can continue with this guide to upgrade to PHP 8.

### 1. PHP Packages

Upgrading from PHP 7.x to PHP 8 involves not only upgrading PHP core, but all of its extensions. For example, if you use the PHP extension cURL, you will need to manually install the PHP 8 version at the end of this guide.

At the end of this guide, I have included a command to install the most common PHP 8 extensions, however, you should check which PHP 7.x extensions are currently installed on your particular server and take note of anything critical to the running of your own web app.

```bash
dpkg -l | grep php | tee packages.txt
```

Output:

```
ii  libapache2-mod-php               1:7.2+60ubuntu1                             all          server-side, HTML-embedded scri
ii  libapache2-mod-php7.2            7.2.24-0ubuntu0.18.04.7                     amd64        server-side, HTML-embedded scri
ii  php                              1:7.2+60ubuntu1                             all          server-side, HTML-embedded scri
ii  php-bz2                          1:7.2+60ubuntu1                             all          bzip2 module for PHP [default]
ii  php-common                       1:60ubuntu1                                 all          Common files for PHP packages
ii  php-curl                         1:7.2+60ubuntu1                             all          CURL module for PHP [default]
ii  php-gd                           1:7.2+60ubuntu1                             all          GD module for PHP [default]
ii  php-mbstring                     1:7.2+60ubuntu1                             all          MBSTRING module for PHP [defaul
ii  php-mysql                        1:7.2+60ubuntu1                             all          MySQL module for PHP [default]
ii  php-pear                         1:1.10.5+submodules+notgz-1ubuntu1.18.04.3  all          PEAR Base System
ii  php-php-gettext                  1.0.12-0.1                                  all          read gettext MO files directly,
ii  php-phpseclib                    2.0.9-1                                     all          implementations of an arbitrary
ii  php-tcpdf                        6.2.13+dfsg-1ubuntu1                        all          PHP class for generating PDF fi
ii  php-xml                          1:7.2+60ubuntu1                             all          DOM, SimpleXML, WDDX, XML, and
ii  php-zip                          1:7.2+60ubuntu1                             all          Zip module for PHP [default]
ii  php7.2                           7.2.24-0ubuntu0.18.04.7                     all          server-side, HTML-embedded scri
ii  php7.2-bz2                       7.2.24-0ubuntu0.18.04.7                     amd64        bzip2 module for PHP
ii  php7.2-cli                       7.2.24-0ubuntu0.18.04.7                     amd64        command-line interpreter for th
ii  php7.2-common                    7.2.24-0ubuntu0.18.04.7                     amd64        documentation, examples and com
ii  php7.2-curl                      7.2.24-0ubuntu0.18.04.7                     amd64        CURL module for PHP
ii  php7.2-gd                        7.2.24-0ubuntu0.18.04.7                     amd64        GD module for PHP
ii  php7.2-json                      7.2.24-0ubuntu0.18.04.7                     amd64        JSON module for PHP
ii  php7.2-mbstring                  7.2.24-0ubuntu0.18.04.7                     amd64        MBSTRING module for PHP
ii  php7.2-mysql                     7.2.24-0ubuntu0.18.04.7                     amd64        MySQL module for PHP
ii  php7.2-opcache                   7.2.24-0ubuntu0.18.04.7                     amd64        Zend OpCache module for PHP
ii  php7.2-readline                  7.2.24-0ubuntu0.18.04.7                     amd64        readline module for PHP
ii  php7.2-xml                       7.2.24-0ubuntu0.18.04.7                     amd64        DOM, SimpleXML, WDDX, XML, and
ii  php7.2-zip                       7.2.24-0ubuntu0.18.04.7                     amd64        Zip module for PHP
ii  phpmyadmin                       4:4.6.6-5ubuntu0.5                          all          MySQL web administration tool
```

The example above shows PHP 7.2 extensions installed on my own server before upgrading to PHP 8. Copy your own results into a text file and keep it safe in case you need to install the PHP 8 version later.

### 2. Uninstall/Remove PHP 7.x and Extensions

To uninstall PHP 7.x and all of its extensions, run the command below. Press `y` and `ENTER` when prompted.

```bash
sudo apt-get purge php7.*
```

If you have phpMyAdmin installed, you may be presented with this screen.

If prompted with message the below, select `YES` and press `ENTER`.![](https://devanswers.co/wp-content/uploads/2021/05/image-1024x316.png?v=1620503170)

If prompted with the message below, select `NO` and press `ENTER`.

![](https://devanswers.co/wp-content/uploads/2021/05/image-1-1024x257.png?v=1620503259)

### 3. Autoclean and Autoremove

After uninstalling packages from Linux, it’s advised to run these two commands.

```bash
sudo apt-get autoclean
```

Press `Y` and `ENTER` if prompted.

```bash
sudo apt-get autoremove
```

### 4. Install PHP 8.1

You can now install PHP 8.1 Press `ENTER` to continue when prompted.

```bash
sudo add-apt-repository ppa:ondrej/php
```

```bash
sudo apt-get update
```

```bash
sudo apt-get install php8.1
```

Restart Apache.

```bash
sudo service apache2 restart
```

### 5. Install PHP 8 Extensions

The command below includes some of the most popular PHP extensions, which should hopefully cover you. However, if you find that some extensions are missing, refer to Step 1 above and manually install the packages you require.

```bash
sudo apt install php8.1-common php8.1-mysql php8.1-xml php8.1-xmlrpc php8.1-curl php8.1-gd php8.1-imagick php8.1-cli php8.1-dev php8.1-imap php8.1-mbstring php8.1-opcache php8.1-soap php8.1-zip php8.1-intl -y
```

apt install -y php8.0-{common,xml,zip,mysql,curl,mbstring,gd,intl,xsl,bcmath,imap,soap,readline,sqlite3,gmp}

```bash
sudo service apache2 restart
```

### 6. Check PHP version

To check if you have installed PHP 8 correctly, run:

```bash
php -v
```
