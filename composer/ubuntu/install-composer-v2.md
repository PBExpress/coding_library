# Install Composer V2

#### Introduction <a href="#introduction" id="introduction"></a>

[Composer](https://getcomposer.org/) is a popular dependency management tool for PHP, created mainly to facilitate installation and updates for project dependencies. It will check which other packages a specific project depends on and install them for you, using the appropriate versions according to the project requirements. Composer is also commonly used to bootstrap new projects based on popular PHP frameworks, such as [Symfony](https://symfony.com/) and [Laravel](https://laravel.com/).

In this tutorial, you’ll install and get started with Composer on an Ubuntu 20.04 system.

### Step 1 — Installing PHP and Additional Dependencies <a href="#step-1-installing-php-and-additional-dependencies" id="step-1-installing-php-and-additional-dependencies"></a>

In addition to dependencies that should be already included within your Ubuntu 20.04 system, such as `git` and `curl`, Composer requires `php-cli` in order to execute PHP scripts in the command line, and `unzip` to extract zipped archives. We’ll install these dependencies now.

First, update the package manager cache by running:

```
sudo apt update
```

Next, run the following command to install the required packages:

```
sudo apt install php-cli unzip
```

You will be prompted to confirm installation by typing `Y` and then `ENTER`.

Once the prerequisites are installed, you can proceed to installing Composer.

### Step 2 — Downloading and Installing Composer <a href="#step-2-downloading-and-installing-composer" id="step-2-downloading-and-installing-composer"></a>

Composer provides an [installer](https://getcomposer.org/installer) script written in PHP. We’ll download it, verify that it’s not corrupted, and then use it to install Composer.

Make sure you’re in your home directory, then retrieve the installer using `curl`:

```
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
```

Next, we’ll verify that the downloaded installer matches the SHA-384 hash for the latest installer found on the [Composer Public Keys / Signatures](https://composer.github.io/pubkeys.html) page. To facilitate the verification step, you can use the following command to programmatically obtain the latest hash from the Composer page and store it in a shell variable:

```
HASH=`curl -sS https://composer.github.io/installer.sig`
```

If you want to verify the obtained value, you can run:

```
echo $HASH
```

```
Output
e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a
```

Now execute the following PHP code, as provided in the Composer [download page](https://getcomposer.org/download/), to verify that the installation script is safe to run:

```
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

You’ll see the following output:

Output

```
Installer verified.
```

To install `composer` globally, use the following command which will download and install Composer as a system-wide command named `composer`, under `/usr/local/bin`:

```
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

You’ll see output similar to this:

```
OutputAll settings correct for using Composer
Downloading...

Composer (version 2.2.9) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```

To test your installation, run:

```
composer
```

Laravel Command not found fix

```bash
echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc && source ~/.bashrc
```

```
Output   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version Composer version 2.2.9 2022-03-15 22:13:37
Usage:
  command [options] [arguments]

Options:
  -h, --help                     Display this help message
  -q, --quiet                    Do not output any message
  -V, --version                  Display this application version
      --ansi                     Force ANSI output
      --no-ansi                  Disable ANSI output
  -n, --no-interaction           Do not ask any interactive question
      --profile                  Display timing and memory usage information
      --no-plugins               Whether to disable plugins.
  -d, --working-dir=WORKING-DIR  If specified, use the given directory as working directory.
      --no-cache                 Prevent use of the cache
  -v|vv|vvv, --verbose           Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
...
```

This verifies that Composer was successfully installed on your system and is available system-wide
