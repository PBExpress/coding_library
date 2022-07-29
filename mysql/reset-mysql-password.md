# Reset MySQL Password



### To reset the password

Follow these steps (can be helpful if you really forget your password and you can try it anytime, even if you're not in the situation at the moment):

1.  Stop `mysql`

    ```sql
    sudo /etc/init.d/mysql stop
    ```

    Or for other distribution versions:

    ```sql
    sudo /etc/init.d/mysqld stop
    ```
2.  Start MySQL in safe mode

    ```sql
    sudo mysqld_safe --skip-grant-tables &
    ```
3.  Log into MySQL using root

    ```sql
    mysql -u root
    ```
4.  Select the MySQL database to use

    ```sql
    use mysql;
    ```
5.  Reset the password

    ```sql
    -- MySQL version < 5.7
    update user set password=PASSWORD("mynewpassword") where User='root';

    -- MySQL 5.7, mysql.user table "password" field -> "authentication_string"

    update user set authentication_string=password('mynewpassword') where user='root';
    ```
6.  Flush the privileges

    ```sql
    flush privileges;
    ```
7.  Restart the server

    ```sql
    quit
    ```
8.  Stop and start the server again

    Ubuntu and Debian:

    ```sql
    sudo /etc/init.d/mysql stop
    ...
    sudo /etc/init.d/mysql start
    ```

On CentOS, Fedora, and RHEL:

```sql
    sudo /etc/init.d/mysqld stop
    ...
    sudo /etc/init.d/mysqld start
```

1.  Login with a new password

    ```sql
    mysql -u root -p
    ```
2. Type the new password and enjoy your server again like nothing happened
