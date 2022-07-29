# MySQL (Create a Database)

*   Log into MySQL as root

    ```
    mysql -u root
    ```
*   Create a new database user

    ```
    GRANT ALL PRIVILEGES ON *.* TO 'db_user'@'localhost' IDENTIFIED BY 'P@s$w0rd123!';
    ```

    **NOTE:** Be sure to modify `db_user` with the actual name, you would like to give the database user, as well as, `P@s$w0rd123!` with the password to be given to the user.
* Log out of MySQL by typing: `\q`.
*   Log in as the new database user you just created:Copy

    ```
    mysql -u db_user -p
    ```

    **NOTE:** Be sure to modify `db_user` with the actual database user name.

    Then, type the new database user’s password and press **Enter**.
*   Create a new database

    ```
    CREATE DATABASE db_name;
    ```

    **NOTE:** Be sure to modify `db_name` with the actual name you would like to give the database.
* **mysql> GRANT ALL PRIVILEGES ON pblaravel.** **\* TO 'pbexpress'@'localhost';**

**note don't delete dot after pblaravel**
