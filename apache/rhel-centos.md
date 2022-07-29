# RHEL/CentOS

### How to install Apache on RHEL 8 / CentOS 8 Linux step by step instructions

1.  First step is to use `dnf` command to [install package](https://linuxconfig.org/how-to-install-packages-on-redhat-8) called `httpd`:

    ```
    dnf install httpd
    ```
2.  Run and enable the Apache webserver to start after reboot:

    ```
    systemctl enable httpd
    systemctl start httpd
    ```
3.  Optionally, if you need your Apache web server to be accessed from remote locations open HTTP firewall port 80:

    ```
    firewall-cmd --zone=public --permanent --add-service=http
    firewall-cmd --reload
    ```

    For more information visit [RHEL 8 open HTTP firewall port 80 and HTTPS port 443 with firewalld](https://linuxconfig.org/redhat-8-open-http-port-80-and-https-port-443-with-firewalld) tutorial.
4.  Insert your website files.

    By default the Apache web server will greet you with a default welcome page.To disable the default Apache welcome page insert your `index.html` into `/var/www/html/` directory. For example:

    ```
    echo Apache on RHEL 8 / CentOS 8 > /var/www/html/index.html
    ```
5.  Access your website.

    To access your new sample website navigate your web browser to either `http://YOUR-APACHE-IP-ADDRESS` or `http://YOUR-APACHE-HOSTNAME`. For example `http://192.168.1.151`.
