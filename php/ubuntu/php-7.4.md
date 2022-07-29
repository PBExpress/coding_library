# PHP 7.4

## How To Install PHP 7.4 and Set Up a Local Development Environment on Ubuntu 20.04

#### Introduction <a href="#introduction" id="introduction"></a>

PHP is a popular server scripting language known for creating dynamic and interactive web pages. Getting up and running with your language of choice is the first step in learning to program.

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

### Step 1 — Setting Up PHP 7.4 <a href="#step-1-setting-up-php-7-4" id="step-1-setting-up-php-7-4"></a>

You’ll be completing your installation and setup on the command line, which is a non-graphical way to interact with your computer. That is, instead of clicking on buttons, you’ll be typing in text and receiving feedback from your computer through text as well.

The command line, also known as a shell or terminal, can help you modify and automate many of the tasks you do on a computer every day and is an essential tool for software developers. There are many terminal commands to learn that can enable you to do more powerful things. The article [An Introduction to the Linux Terminal](https://www.digitalocean.com/community/tutorials/an-introduction-to-the-linux-terminal) can get you better oriented with the terminal.

On Ubuntu, you can find the Terminal application by clicking on the Ubuntu icon in the upper-left-hand corner of your screen and typing `terminal` into the search bar. Click on the Terminal application icon to open it. Alternatively, you can hit the `CTRL`, `ALT`, and `T` keys on your keyboard at the same time to open the Terminal application automatically.

![Ubuntu terminal](https://assets.digitalocean.com/articles/eng\_python/UbuntuDebianSetUp/UbuntuSetUp.png)

**Note:** Ubuntu 20.04 ships with PHP 7.4 in its upstream repositories. This means that if you attempt to install PHP without a specified version, it will use 7.4.

You will want to avoid relying on the default version of PHP because that default version could change depending on where you are running your code. You may also wish to install a different version to match an application you are using or to upgrade to a newer version, such as PHP 8.

Run the following command to update `apt-get` itself, which ensures that you have access to the latest versions of anything you want to install:

```
sudo apt-get update
```

Next, install `software-properties-common`, which adds management for additional software sources:

```
sudo apt -y install software-properties-common
```

The `-y` flag will automatically agree to the installation. Without that, you would receive a prompt in your terminal window for each installation.

Next, install the repository `ppa:ondrej/php`, which will give you all your versions of PHP:

```
sudo add-apt-repository ppa:ondrej/php
```

Finally, you update `apt-get` again so your package manager can see the newly listed packages:

```
sudo apt-get update
```

Now you’re ready to install PHP 7.4 using the following command:

```
sudo apt -y install php7.4
```

Check the version installed:

```
php -v
```

You will receive something similar to the following:

```
OutputPHP 7.4.0beta4 (cli) (built: Aug 28 2019 11:41:49) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0-dev, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.0beta4, Copyright (c), by Zend Technologies
```

Besides PHP itself, you will likely want to install some additional PHP modules. You can use this command to install additional modules, replacing `PACKAGE_NAME` with the package you wish to install:

```
sudo apt-get install php7.4-PACKAGE_NAME
```

You can also install more than one package at a time. Here are a few suggestions of the most common modules you will most likely want to install:

```
sudo apt-get install -y php7.4-cli php7.4-json php7.4-common php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath
```

apt install -y php8.0-{common,xml,zip,mysql,curl,mbstring,gd,intl,xsl,bcmath,imap,soap,readline,sqlite3,gmp}

This command will install the following modules:

* `php7.4-cli` - command interpreter, useful for testing PHP scripts from a shell or performing general shell scripting tasks
* `php7.4-json` - for working with JSON data
* `php7.4-common` - documentation, examples, and common modules for PHP
* `php7.4-mysql` - for working with MySQL databases
* `php7.4-zip` - for working with compressed files
* `php7.4-gd` - for working with images
* `php7.4-mbstring` - used to manage non-ASCII strings
* `php7.4-curl` - lets you make HTTP requests in PHP
* `php7.4-xml` - for working with XML data
* `php7.4-bcmath` - used when working with precision floats

PHP configurations related to Apache are stored in `/etc/php/7.4/apache2/php.ini`. You can list all loaded PHP modules with the following command:

```
php -m
```

You have installed PHP and verified the version you have running. You also installed any required PHP modules and were able to list the modules that you have loaded.

You could start using PHP right now, but you will likely want to use various libraries to build PHP applications quickly. Before you test your PHP environment, first set up a dependency manager for your projects.

### Step 2 — Setting Up Composer for Dependency Management (Optional) <a href="#step-2-setting-up-composer-for-dependency-management-optional" id="step-2-setting-up-composer-for-dependency-management-optional"></a>

Libraries are a collection of code that can help you solve common problems without needing to write everything yourself. Since there are many libraries available, using a dependency manager will help you manage multiple libraries as you become more experienced in writing PHP.

[Composer](https://getcomposer.org/) is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and will manage installing and updating these packages.

Although similar, Composer is not a package manager in the same sense as `yum` or `apt`. It deals with “packages” or libraries, but it manages them on a per-project basis, installing them in a directory (e.g. `vendor`) inside your project. By default, it does not install anything globally. Thus, it is a _dependency manager_. It does, however, support a global project for convenience via the `global` command.

This idea is not new, and Composer is strongly inspired by Node’s `npm` and Ruby’s `bundler`.

Suppose:

* You have a project that depends on several libraries.
* Some of those libraries depend on other libraries.

Composer:

* Enables you to declare the libraries you depend on.
* Finds out which versions of which packages can and need to be installed and installs them by downloading them into your project.
* Enables you to update all your dependencies in one command.
* Enables you to see the Basic Usage chapter for more details on declaring dependencies.

There are, in short, two ways to install Composer: locally as part of your project or globally as a system-wide executable. Either way, you will start with the local install.

#### Locally <a href="#locally" id="locally"></a>

To quickly install Composer in the current directory, run this script in your terminal:

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

This installer script will check some `php.ini` settings, warn you if they are set incorrectly, and then download the latest `composer.phar` in the current directory. The four lines will, in order:

* Download the installer to the current directory
* Verify the installer SHA-384, which you can also [cross-check here](https://composer.github.io/pubkeys.html)
* Run the installer
* Remove the installer

The installer will check a few PHP settings and then download `composer.phar` to your working directory. This file is the Composer binary. It is a PHAR (PHP archive), which is an archive format for PHP that can be run on the command line, amongst other things.

In order to run Composer, you use `php composer.phar`. As an example, run this command to see the version of Composer you have installed:

```
php composer.phar --version
```

To use Composer locally, you will want your `composer.phar` file to be in your project’s root directory. You can start in your project directory before installing Composer. You can also move the file after installation. You can also install Composer to a specific directory by using the `--install-dir` option and additionally (re)name it using the `--filename` option.

Since Composer is something used across projects, it’s recommended that you continue to the next portion and set Composer to run globally.

#### Globally <a href="#globally" id="globally"></a>

You can place the Composer PHAR anywhere you wish. If you put it in a directory that is part of your `$PATH`, you can access it globally. You can even make it executable on Ubuntu (and other Unix systems) and invoke it without directly using the PHP interpreter.

After installing locally, run this command to move `composer.phar` to a directory that is in your path:

```
sudo mv composer.phar /usr/local/bin/composer
```

If you’d like to install it only for your user and avoid requiring root permissions, you can use `~/.local/bin` instead, which is available by default on some Linux distributions:

```
mv composer.phar ~/.local/bin/composer
```

Now to run Composer, use `composer` instead of `php composer.phar`. To check for your Composer version, run:

```
composer --version
```

As a final step, you may optionally initialize your project with `composer init`. This will create the `composer.json` file that will manage your project dependencies. Initializing the project will also let you define project details such as Author and License, and use [Composer’s autoload functionality](https://getcomposer.org/doc/01-basic-usage.md#autoloading). You can define dependencies now or add them later.

Run this command to initialize a project:

```
composer init
```

Running this command will start the setup wizard. Details that you enter in the wizard can be updated later, so feel free to leave the defaults and just press `ENTER`. If you aren’t ready to install any dependencies, you can choose `no`. Enter in your details at each prompt:

```
Output
This command will guide you through creating your composer.json config.
Package name (sammy/php_install): sammy/project1
Description []:
Author [Sammy <sammy@digitalocean.com>, n to skip]:
Minimum Stability []: 
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []: 

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]? no
Would you like to define your dev dependencies (require-dev) interactively [yes]? no

{
    "name": "sammy/project1",
    "type": "project",
    "authors": [
        {
            "name": "Sammy",
            "email": "sammy@digitalocean.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]? yes
```

Before you confirm the generation, you will see a sample of the `composer.json` file that the wizard will create. If it all looks good, you can confirm the default of `yes`. If you need to start over, choose `no`.

The first time you define any dependency, Composer will create a `vendor` folder. All dependencies install into this `vendor` folder. Composer also creates a `composer.lock` file. This file specifies the **exact** version of each dependency and subdependency used in your project. This assures that any machine on which your program is run, will be using the exact same version of each packages.

**Note:** The `vendor` folder should never be committed to your version control system (VCS). The `vendor` folder only contains packages you have installed from other vendors. Those individual vendors will maintain their own code in their own version control systems. You should only be tracking the code you write. Instead of committing the `vendor` folder, you only need to commit your `composer.json` and `composer.lock` files. You can learn more about ignoring specific files in [How To Use Git: A Reference Guide](https://www.digitalocean.com/community/cheatsheets/how-to-use-git-a-reference-guide#ignoring-files).
