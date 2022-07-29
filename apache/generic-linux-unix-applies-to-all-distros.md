# Generic Linux/Unix (applies to all distros)

### Generic method to start/stop/restart Apache on a Linux/Unix/\*BSD machines

First, use the [type command](https://bash.cyberciti.biz/guide/Type\_command?utm\_source=Linux\_Unix\_Command\&utm\_medium=faq\&utm\_campaign=nixcmd) or [command command](https://bash.cyberciti.biz/guide/Command?utm\_source=Linux\_Unix\_Command\&utm\_medium=faq\&utm\_campaign=nixcmd) to find the apachectl or apachectl2 path:\
`type -a apachectl`\
`type -a apache2ctl`\
Outputs from the Ubuntu Linux 20.04 LTS server:

```
apachectl is /usr/sbin/apachectl
apachectl is /sbin/apachectl
```

Then use the syntax is as follows (must be run as root user):\
`## stop it ##`\
`# apachectl -k stop`\
`## restart it ##`\
`# apachectl -k restart`\
`## graceful restart it ##`\
`# apachectl -k graceful`\
`## Start it ##`\
`# apachectl -f /path/to/your/httpd.conf`\
`# apachectl -f /usr/local/apache2/conf/httpd.conf`\
The apachectl/apache2ctl is Apache HTTP server control interface. Other options are as follows:

#### Start the Apache daemon

`# apachectl start`\
`# OR #`\
`# apache2ctl start`

#### Stops the Apache daemon

`# apachectl stop`\
`# OR #`\
`# apache2ctl stop`

#### Restarts the Apache daemon by sending it a SIGHUP

`# apachectl restart`\
`# OR #`\
`# apache2ctl restart`

#### Shows a full status report from mod\_status

`# apachectl fullstatus`\
`# OR #`\
`# apache2ctl fullstatus`

#### Displays a brief status report

`# apachectl status`\
`# OR #`\
`# apache2ctl status`

#### Gracefully restarts the Apache daemon by sending it a SIGUSR1

`# apachectl graceful`\
`# OR #`\
`# apache2ctl graceful`\
We can do gracefully stops the Apache httpd daemon too? Try:\
`# apachectl graceful-stop`\
`# OR #`\
`# apache2ctl graceful-stop`

#### Run a configuration file syntax test

`# apachectl configtest`\
`# OR #`\
`# apache2ctl configtest`

### Summing up

You learned how to start, stop or restart the Apache 2 web server using command-line over ssh-based session. Use the [man command](https://bash.cyberciti.biz/guide/Man\_command?utm\_source=Linux\_Unix\_Command\&utm\_medium=faq\&utm\_campaign=nixcmd) or [help command](https://bash.cyberciti.biz/guide/Help\_command?utm\_source=Linux\_Unix\_Command\&utm\_medium=faq\&utm\_campaign=nixcmd) to read the following man pages:\
`$ man service`\
`$ man systemctl`\
`$ man httpd`\
`$ man apachectl`
