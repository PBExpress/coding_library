# Composer V2

To be able to use composer we naturally need `php`, with some extensions. PHP 7.2 and extensions for it are reachable after [enabling subsription management repositories](https://linuxconfig.org/enable-subscription-management-repositories-on-redhat-8-linux), as well as on the installer distributed in ISO format.

1.  First we need to install php related packages with `dnf`:

    ```
    dnf install php php-cli php-zip php-json
    ```
2.  Now we can download the Composer installer with php:

    ```
    # php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    ```
3.  To be able to access the tool from anywhere on the system, we place it on the `$PATH`. `/usr/local/bin` is included in the `$PATH` by default.

    ```
    # php composer-setup.php --install-dir=/usr/local/bin --filename=composer
    All settings correct for using Composer
    Downloading...

    Composer (version 1.8.0) successfully installed to: /usr/local/bin/composer
    Use it: php /usr/local/bin/composer
    ```
