# MySQL Server Management

## How To Create a New User and Grant Permissions in MySQL

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

In order to follow along with this guide, you’ll need access to a MySQL database. This guide assumes that this database is installed on a virtual private server running Ubuntu 20.04, though the principles it outlines should be applicable regardless of how you access your database.

If you don’t have access to a MySQL database and would like to set one up yourself, you can follow one of our guides on [How To Install MySQL](https://www.digitalocean.com/community/tutorial\_collections/how-to-install-mysql). Again, regardless of your server’s underlying operating system, the methods for creating a new MySQL user and granting them permissions will generally be the same.

Please note that any portions of example commands that you need to change or customize will be highlighted `like this` throughout this guide.

### Creating a New User <a href="#creating-a-new-user" id="creating-a-new-user"></a>

Upon installation, MySQL creates a **root** user account which you can use to manage your database. This user has full privileges over the MySQL server, meaning it has complete control over every database, table, user, and so on. Because of this, it’s best to avoid using this account outside of administrative functions. This step outlines how to use the **root** MySQL user to create a new user account and grant it privileges.

In Ubuntu systems running MySQL `5.7` (and later versions), the **root** MySQL user is set to authenticate using the `auth_socket` plugin by default rather than with a password. This plugin requires that the name of the operating system user that invokes the MySQL client matches the name of the MySQL user specified in the command. This means that you need to precede the `mysql` command with `sudo` to invoke it with the privileges of the **root** Ubuntu user in order to gain access to the **root** MySQL user:

```
sudo mysql
```

**Note:** If your **root** MySQL user is configured to authenticate with a password, you will need to use a different command to access the MySQL shell. The following will run your MySQL client with regular user privileges, and you will only gain administrator privileges within the database by authenticating with the correct password:

```
mysql -u root -p
```

Once you have access to the MySQL prompt, you can create a new user with a `CREATE USER` statement. These follow this general syntax:

```
CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';
```

After `CREATE USER`, you specify a username. This is immediately followed by an `@` sign and then the hostname from which this user will connect. If you only plan to access this user locally from your Ubuntu server, you can specify `localhost`. Wrapping both the username and host in single quotes isn’t always necessary, but doing so can help to prevent errors.

You have several options when it comes to choosing your user’s authentication plugin. The `auth_socket` plugin mentioned previously can be convenient, as it provides strong security without requiring valid users to enter a password to access the database. But it also prevents remote connections, which can complicate things when external programs need to interact with MySQL.

As an alternative, you can leave out the `WITH`` ``authentication_plugin` portion of the syntax entirely to have the user authenticate with MySQL’s default plugin, `caching_sha2_password`. [The MySQL documentation recommends this plugin ](https://dev.mysql.com/doc/refman/8.0/en/upgrading-from-previous-series.html#upgrade-caching-sha2-password)for users who want to log in with a password due to its strong security features.

Run the following command to create a user that authenticates with `caching_sha2_password`. Be sure to change `sammy` to your preferred username and `password` to a strong password of your choosing:

```
CREATE USER 'pbexpress'@'localhost' IDENTIFIED BY 'Chunkers123!';
```

**Note**: There is a known issue with some versions of PHP that causes problems with `caching_sha2_password`. If you plan to use this database with a PHP application — phpMyAdmin, for example — you may want to create a user that will authenticate with the older, though still secure, `mysql_native_password` plugin instead:

```
CREATE USER 'pbexpress'@'localhost' IDENTIFIED WITH mysql_native_password 
BY 'Chunkers123!';
```

If you aren’t sure, you can always create a user that authenticates with `caching_sha2_plugin` and then `ALTER` it later on with this command:

```
ALTER USER 'pbexpress'@'localhost' IDENTIFIED WITH mysql_native_password 
BY 'Chunkers123!';
```

After creating your new user, you can grant them the appropriate privileges.

### Granting a User Permissions <a href="#granting-a-user-permissions" id="granting-a-user-permissions"></a>

The general syntax for granting user privileges is as follows:

```
GRANT PRIVILEGE ON database.table TO 'username'@'host';
```

The `PRIVILEGE` value in this example syntax defines what actions the user is allowed to perform on the specified `database` and `table`. You can grant multiple privileges to the same user in one command by separating each with a comma. You can also grant a user privileges globally by entering asterisks (`*`) in place of the database and table names. In SQL, asterisks are special characters used to represent “all” databases or tables.

To illustrate, the following command grants a user global privileges to `CREATE`, `ALTER`, and `DROP` databases, tables, and users, as well as the power to `INSERT`, `UPDATE`, and `DELETE` data from any table on the server. It also grants the user the ability to query data with `SELECT`, create foreign keys with the `REFERENCES` keyword, and perform `FLUSH` operations with the `RELOAD` privilege. However, you should only grant users the permissions they need, so feel free to adjust your own user’s privileges as necessary.

You can find the full list of available privileges in [the official MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#privileges-provided-summary).

Run this `GRANT` statement, replacing `sammy` with your own MySQL user’s name, to grant these privileges to your user:

```
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
```

Note that this statement also includes `WITH GRANT OPTION`. This will allow your MySQL user to grant any permissions that it has to other users on the system.

**Warning**: Some users may want to grant their MySQL user the `ALL PRIVILEGES` privilege, which will provide them with broad superuser privileges akin to the **root** user’s privileges, like so:

```
GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
```

Such broad privileges **should not be granted lightly**, as anyone with access to this MySQL user will have complete control over every database on the server.

Many guides suggest running the `FLUSH PRIVILEGES` command immediately after a `CREATE USER` or `GRANT` statement in order to reload the grant tables to ensure that the new privileges are put into effect:

```
FLUSH PRIVILEGES;
```

However, according to the [official MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/privilege-changes.html), when you modify the grant tables indirectly with an account management statement like `GRANT`, the database will reload the grant tables immediately into memory, meaning that the `FLUSH PRIVILEGES` command isn’t necessary in our case. On the other hand, running it won’t have any negative effect on the system.

If you need to revoke a permission, the structure is almost identical to granting it:

```
REVOKE type_of_permission ON database_name.table_name FROM 'username'@'host';
```

Note that when revoking permissions, the syntax requires that you use `FROM`, instead of `TO` which you used when granting the permissions.

You can review a user’s current permissions by running the `SHOW GRANTS` command:

```
SHOW GRANTS FOR 'username'@'host';
```

Just as you can delete databases with `DROP`, you can use `DROP` to delete a user:

```
DROP USER 'username'@'localhost';
```

After creating your MySQL user and granting them privileges, you can exit the MySQL client:

```
exit
```

In the future, to log in as your new MySQL user, you’d use a command like the following:

```
mysql -u pbexpress -p
```

The `-p` flag will cause the MySQL client to prompt you for your MySQL user’s password in order to authenticate.
