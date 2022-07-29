# Debian/Ubuntu

### Debian/Ubuntu Linux Specific Commands to Start/Stop/Restart Apache

You can either use service or /etc/init.d/ command as follows on **Debian Linux version 7.x or Ubuntu Linux version Ubuntu 14.10 or older**:

#### Restart Apache 2 web server, enter:

`# /etc/init.d/apache2 restart`\
OR\
`$ sudo /etc/init.d/apache2 restart`\
OR\
`$ sudo service apache2 restart`

#### To stop Apache 2 web server, enter:

`# /etc/init.d/apache2 stop`\
OR\
`$ sudo /etc/init.d/apache2 stop`\
OR\
`$ sudo service apache2 stop`

#### To start Apache 2 web server, enter:

`# /etc/init.d/apache2 start`\
OR\
`$ sudo /etc/init.d/apache2 start`\
OR\
`$ sudo service apache2 start`

### A note about Debian/Ubuntu Linux **systemd** users

Use the following systemctl command on **Debian Linux version 8.x+ or Ubuntu Linux version Ubuntu 15.04+ or above**:\
`## Start command ##`\
`$ sudo systemctl start apache2.service`\
`## Stop command ##`\
`$ sudo systemctl stop apache2.service`\
`## Restart command ##`\
`$ sudo systemctl restart apache2.service`\
We can view status using the following command:\
`$ sudo systemctl status apache2.service`\
Outputs:

```
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2021-02-24 20:39:39 UTC; 5 days ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 115 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
    Process: 15247 ExecReload=/usr/sbin/apachectl graceful (code=exited, status=0/SUCCESS)
   Main PID: 128 (apache2)
      Tasks: 6 (limit: 4672)
     Memory: 16.4M
     CGroup: /system.slice/apache2.service
             ├─  128 /usr/sbin/apache2 -k start
             ├─15254 /usr/sbin/apache2 -k start
             ├─15255 /usr/sbin/apache2 -k start
             ├─15256 /usr/sbin/apache2 -k start
             ├─15257 /usr/sbin/apache2 -k start
             └─15258 /usr/sbin/apache2 -k start

Feb 27 00:00:23 ubuntu-db-mgmnt systemd[1]: Reloaded The Apache HTTP Server.
Feb 28 00:00:23 ubuntu-db-mgmnt systemd[1]: Reloading The Apache HTTP Server.
```

###
