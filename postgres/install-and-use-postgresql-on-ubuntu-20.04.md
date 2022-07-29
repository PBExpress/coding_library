# Install and Use PostgreSQL on Ubuntu 20.04

#### Introduction <a href="#introduction" id="introduction"></a>

Relational database management systems are a key component of many web sites and applications. They provide a structured way to store, organize, and access information.

[PostgreSQL](https://www.postgresql.org/), or Postgres, is a relational database management system that provides an implementation of the [SQL](https://en.wikipedia.org/wiki/SQL) querying language. It’s standards-compliant and has many advanced features like reliable transactions and concurrency without read locks.

This guide demonstrates how to install Postgres on an Ubuntu 20.04 server. It also provides some instructions for general database administration.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

To follow along with this tutorial, you will need one Ubuntu 20.04 server that has been configured by following our [Initial Server Setup for Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04) guide. After completing this prerequisite tutorial, your server should have a non-**root** user with sudo permissions and a basic firewall.

You can also use an interactive terminal that is embedded on this page to experiment with installing and configuring PostgreSQL in this tutorial. Click the following `Launch an Interactive Terminal!` button to get started.

Launch an Interactive Terminal!

### Step 1 — Installing PostgreSQL <a href="#step-1-installing-postgresql" id="step-1-installing-postgresql"></a>

Ubuntu’s default repositories contain Postgres packages, so you can install these using the `apt` packaging system.

If you’ve not done so recently, refresh your server’s local package index:

```
sudo apt update
```

Then, install the Postgres package along with a `-contrib` package that adds some additional utilities and functionality:

```
sudo apt install postgresql postgresql-contrib
```

Ensure that the server is running using the `postgres start` command:

```
postgres -D /usr/local/pgsql/data >logfile 2>&1 &
```

Now that the software is installed and running, we can go over how it works and how it may be different from other relational database management systems you may have used.

### Step 2 — Using PostgreSQL Roles and Databases <a href="#step-2-using-postgresql-roles-and-databases" id="step-2-using-postgresql-roles-and-databases"></a>

By default, Postgres uses a concept called “roles” to handle authentication and authorization. These are, in some ways, similar to regular Unix-style accounts, but Postgres does not distinguish between users and groups and instead prefers the more flexible term “role”.

Upon installation, Postgres is set up to use _peer authentication_, meaning that it associates Postgres roles with a matching Unix/Linux system account. If a role exists within Postgres, a Unix/Linux username with the same name is able to sign in as that role.

The installation procedure created a user account called **postgres** that is associated with the default Postgres role. In order to use Postgres, you can log into that account.

There are a few ways to utilize this account to access Postgres.

#### Switching Over to the postgres Account <a href="#switching-over-to-the-postgres-account" id="switching-over-to-the-postgres-account"></a>

Switch over to the **postgres** account on your server by typing:

```
sudo -i -u postgres
```

You can now access the PostgreSQL prompt immediately by typing:

```
psql
```

From there you are free to interact with the database management system as necessary.

Exit out of the PostgreSQL prompt by typing:

```
\q
```

This will bring you back to the `postgres` Linux command prompt.

#### Accessing a Postgres Prompt Without Switching Accounts <a href="#accessing-a-postgres-prompt-without-switching-accounts" id="accessing-a-postgres-prompt-without-switching-accounts"></a>

You can also run the command you’d like with the **postgres** account directly with `sudo`.

For instance, in the last example, you were instructed to get to the Postgres prompt by first switching to the **postgres** user and then running `psql` to open the Postgres prompt. You could do this in one step by running the single command `psql` as the **postgres** user with `sudo`, like this:

```
sudo -u postgres psql
```

This will log you directly into Postgres without the intermediary `bash` shell in between.

Again, you can exit the interactive Postgres session by typing:

```
\q
```

Many use cases require more than one Postgres role. Read on to learn how to configure these.

### Step 3 — Creating a New Role <a href="#step-3-creating-a-new-role" id="step-3-creating-a-new-role"></a>

Currently, you just have the **postgres** role configured within the database. You can create new roles from the command line with the `createrole` command. The `--interactive` flag will prompt you for the name of the new role and also ask whether it should have superuser permissions.

If you are logged in as the **postgres** account, you can create a new user by typing:

```
createuser --interactive
```

If, instead, you prefer to use `sudo` for each command without switching from your normal account, type:

```
sudo -u postgres createuser --interactive
```

The script will prompt you with some choices and, based on your responses, execute the correct Postgres commands to create a user to your specifications.

```
OutputEnter name of role to add: sammy
Shall the new role be a superuser? (y/n) y
```

You can get more control by passing some additional flags. Check out the options by looking at the `man` page:

```
man createuser
```

Your installation of Postgres now has a new user, but you have not yet added any databases. The next section describes this process.

### Step 4 — Creating a New Database <a href="#step-4-creating-a-new-database" id="step-4-creating-a-new-database"></a>

Another assumption that the Postgres authentication system makes by default is that for any role used to log in, that role will have a database with the same name which it can access.

This means that if the user you created in the last section is called **sammy**, that role will attempt to connect to a database which is also called “sammy” by default. You can create the appropriate database with the `createdb` command.

If you are logged in as the **postgres** account, you would type something like:

```
createdb pbpostgres
```

If, instead, you prefer to use `sudo` for each command without switching from your normal account, you would type:

```
sudo -u postgres createdb pbpostgres
```

This flexibility provides multiple paths for creating databases as needed.

### Step 5 — Opening a Postgres Prompt with the New Role <a href="#step-5-opening-a-postgres-prompt-with-the-new-role" id="step-5-opening-a-postgres-prompt-with-the-new-role"></a>

To log in with peer authentication, you’ll need a Linux user with the same name as your Postgres role and database.

If you don’t have a matching Linux user available, you can create one with the `adduser` command. You will have to do this from your non-**root** account with `sudo` privileges (meaning, not logged in as the **postgres** user):

```
sudo adduser sammy
```

Once this new account is available, you can either switch over and connect to the database by typing:

```
sudo -i -u sammy
psql
```

Or, you can do this inline:

```
sudo -u sammy psql
```

This command will log you in automatically, assuming that all of the components have been properly configured.

If you want your user to connect to a different database, you can do so by specifying the database like this:

```
psql -d postgres
```

Once logged in, you can get check your current connection information by typing:

```
\conninfo
```

```
OutputYou are connected to database "sammy" as user "sammy" via socket in "/var/run/postgresql" at port "5432".
```

This is useful if you are connecting to non-default databases or with non-default users.

### Step 6 — Creating and Deleting Tables <a href="#step-6-creating-and-deleting-tables" id="step-6-creating-and-deleting-tables"></a>

Now that you know how to connect to the PostgreSQL database system, you can learn some basic Postgres management tasks.

The basic syntax for creating tables is as follows:

```
CREATE TABLE table_name (
    column_name1 col_type (field_length) column_constraints,
    column_name2 col_type (field_length),
    column_name3 col_type (field_length)
);
```

As you can see, these commands give the table a name, and then define the columns as well as the column type and the max length of the field data. You can also optionally add table constraints for each column.

You can learn more about [how to create and manage tables in Postgres](https://digitalocean.com/community/articles/how-to-create-remove-manage-tables-in-postgresql-on-a-cloud-server) here.

For demonstration purposes, create the following table:

```
CREATE TABLE playground (
    equip_id serial PRIMARY KEY,
    type varchar (50) NOT NULL,
    color varchar (25) NOT NULL,
    location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')),
    install_date date
);
```

This command will create a table that inventories playground equipment. The first column in the table will hold equipment ID numbers of the `serial` type, which is an auto-incrementing integer. This column also has the constraint of `PRIMARY KEY` which means that the values within it must be unique and not null.

The next two lines create columns for the equipment `type` and `color` respectively, neither of which can be empty. The line after these creates a `location` column as well as a constraint that requires the value to be one of eight possible values. The last line creates a `date` column that records the date on which you installed the equipment.

For two of the columns (`equip_id` and `install_date`), the command doesn’t specify a field length. The reason for this is that some data types don’t require a set length because the length or format is implied.

You can see your new table by typing:

```
\d
```

```
Output                  List of relations
 Schema |          Name           |   Type   | Owner 
--------+-------------------------+----------+-------
 public | playground              | table    | sammy
 public | playground_equip_id_seq | sequence | sammy
(2 rows)
```

Your playground table is here, but there’s also something called `playground_equip_id_seq` that is of the type `sequence`. This is a representation of the `serial` type which you gave your `equip_id` column. This keeps track of the next number in the sequence and is created automatically for columns of this type.

If you want to see just the table without the sequence, you can type:

```
\dt
```

```
Output          List of relations
 Schema |    Name    | Type  | Owner 
--------+------------+-------+-------
 public | playground | table | sammy
(1 row)
```

With a table at the ready, let’s use it to practice managing data.

### Step 7 — Adding, Querying, and Deleting Data in a Table <a href="#step-7-adding-querying-and-deleting-data-in-a-table" id="step-7-adding-querying-and-deleting-data-in-a-table"></a>

Now that you have a table, you can insert some data into it. As an example, add a slide and a swing by calling the table you want to add to, naming the columns and then providing data for each column, like this:

```
INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2017-04-28');
INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2018-08-16');
```

You should take care when entering the data to avoid a few common hangups. For one, do not wrap the column names in quotation marks, but the column values that you enter do need quotes.

Another thing to keep in mind is that you do not enter a value for the `equip_id` column. This is because this is automatically generated whenever you add a new row to the table.

Retrieve the information you’ve added by typing:

```
SELECT * FROM playground;
```

```
Output equip_id | type  | color  | location  | install_date 
----------+-------+--------+-----------+--------------
        1 | slide | blue   | south     | 2017-04-28
        2 | swing | yellow | northwest | 2018-08-16
(2 rows)
```

Here, you can see that your `equip_id` has been filled in successfully and that all of your other data has been organized correctly.

If the slide on the playground breaks and you have to remove it, you can also remove the row from your table by typing:

```
DELETE FROM playground WHERE type = 'slide';
```

Query the table again:

```
SELECT * FROM playground;
```

```
Output equip_id | type  | color  | location  | install_date 
----------+-------+--------+-----------+--------------
        2 | swing | yellow | northwest | 2018-08-16
(1 row)
```

Notice that the `slide` row is no longer a part of the table.

### Step 8 — Adding and Deleting Columns from a Table <a href="#step-8-adding-and-deleting-columns-from-a-table" id="step-8-adding-and-deleting-columns-from-a-table"></a>

After creating a table, you can modify it by adding or removing columns. Add a column to show the last maintenance visit for each piece of equipment by typing:

```
ALTER TABLE playground ADD last_maint date;
```

If you view your table information again, you will see the new column has been added but no data has been entered:

```
SELECT * FROM playground;
```

```
Output equip_id | type  | color  | location  | install_date | last_maint 
----------+-------+--------+-----------+--------------+------------
        2 | swing | yellow | northwest | 2018-08-16   | 
(1 row)
```

If you find that your work crew uses a separate tool to keep track of maintenance history, you can delete of the column by typing:

```
ALTER TABLE playground DROP last_maint;
```

This deletes the `last_maint` column and any values found within it, but leaves all the other data intact.

### Step 9 — Updating Data in a Table <a href="#step-9-updating-data-in-a-table" id="step-9-updating-data-in-a-table"></a>

So far, you’ve learned how to add records to a table and how to delete them, but this tutorial hasn’t yet covered how to modify existing entries.

You can update the values of an existing entry by querying for the record you want and setting the column to the value you wish to use. You can query for the `swing` record (this will match _every_ swing in your table) and change its color to `red`. This could be useful if you gave the swing set a paint job:

```
UPDATE playground SET color = 'red' WHERE type = 'swing';
```

You can verify that the operation was successful by querying the data again:

```
SELECT * FROM playground;
```

```
Output equip_id | type  | color | location  | install_date 
----------+-------+-------+-----------+--------------
        2 | swing | red   | northwest | 2018-08-16
(1 row)
```
