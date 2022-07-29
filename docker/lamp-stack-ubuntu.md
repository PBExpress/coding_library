# Lamp Stack (Ubuntu)

## LAMP stack built with Docker Compose

[![Landing Page](https://user-images.githubusercontent.com/43859895/141092846-905eae39-0169-4fd7-911f-9ff32c48b7e8.png)](https://user-images.githubusercontent.com/43859895/141092846-905eae39-0169-4fd7-911f-9ff32c48b7e8.png)

A basic LAMP stack environment built using Docker Compose. It consists of the following:

* PHP
* Apache
* MySQL
* phpMyAdmin
* Redis

As of now, we have several different PHP versions. Use appropriate php version as needed:

* 5.4.x
* 5.6.x
* 7.1.x
* 7.2.x
* 7.3.x
* 7.4.x
* 8.0.x

### Installation

* Clone this repository on your local computer
* configure .env as needed
* Run the `docker-compose up -d`.

```
git clone https://github.com/sprintcube/docker-compose-lamp.git
cd docker-compose-lamp/
cp sample.env .env
// modify sample.env as needed
docker-compose up -d
// visit localhost
```

Your LAMP stack is now ready!! You can access it via `http://localhost`.

### Configuration and Usage

#### General Information

This Docker Stack is build for local development and not for production usage.

#### Configuration

This package comes with default configuration options. You can modify them by creating `.env` file in your root directory. To make it easy, just copy the content from `sample.env` file and update the environment variable values as per your need.

#### Configuration Variables

There are following configuration variables available and you can customize them by overwritting in your own `.env` file.

### **PHP**

_**PHPVERSION**_ Is used to specify which PHP Version you want to use. Defaults always to latest PHP Version.

_**PHP\_INI**_ Define your custom `php.ini` modification to meet your requirments.

### **Apache**

_**DOCUMENT\_ROOT**_

It is a document root for Apache server. The default value for this is `./www`. All your sites will go here and will be synced automatically.

_**APACHE\_DOCUMENT\_ROOT**_

Apache config file value. The default value for this is /var/www/html.

_**VHOSTS\_DIR**_

This is for virtual hosts. The default value for this is `./config/vhosts`. You can place your virtual hosts conf files here.

> Make sure you add an entry to your system's `hosts` file for each virtual host.

_**APACHE\_LOG\_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/apache2`.

### **Database**

> For Apple Silicon Users: Please select Mariadb as Database. Oracle doesn't build their SQL Containers for the arm Architecure

_**DATABASE**_

Define which MySQL or MariaDB Version you would like to use.

_**MYSQL\_INITDB\_DIR**_

When a container is started for the first time files in this directory with the extensions `.sh`, `.sql`, `.sql.gz` and `.sql.xz` will be executed in alphabetical order. `.sh` files without file execute permission are sourced rather than executed. The default value for this is `./config/initdb`.

_**MYSQL\_DATA\_DIR**_

This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.

_**MYSQL\_LOG\_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/mysql`.

### Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

**Apache Modules**

By default following modules are enabled.

* rewrite
* headers

> If you want to enable more modules, just update `./bin/phpX/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose. You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

**Connect via SSH**

You can connect to web server using `docker-compose exec` command to perform various operation on it. Use below command to login to container via ssh.

```
docker-compose exec webserver bash
```

### PHP

The installed version of php depends on your `.env`file.

**Extensions**

By default following extensions are installed. May differ for PHP Versions <7.x.x

* mysqli
* pdo\_sqlite
* pdo\_mysql
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> If you want to install more extension, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if it seems good for general purpose. You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

### phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

[http://localhost:8](http://localhost:8080/)3\
username: root\
password: Chunkers123!

### Redis

It comes with Redis. It runs on default port `6379`.

### Why you shouldn't use this stack unmodified in production

We want to empower developers to quickly create creative Applications. Therefore we are providing an easy to set up a local development environment for several different Frameworks and PHP Versions. In Production you should modify at a minimum the following subjects:

* php handler: mod\_php=> php-fpm
* secure mysql users with proper source IP limitation
