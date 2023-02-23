# Databases

## MySQL

- Open Source
- Fast
- Reliable
- SQL

Two types
- Community
- Developer

### Install

```sh
wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
rpm -ivh mysql80-community-release-el7-3.noarch.rpm
yum install mysql-server
service mysqld stert
service mysqld status
```

Default directory on most Linux based systems: `/var/lib/mysql`

### Validate

```sh
# logs
cat /var/log/mysqld.log
#=> 2023-02-22 ...
# ... as process 4162
# 2023-02-22... temporary password ... : g/io%flE77m
```

Default listens on 3006

Temporary password automatically generated

You can find out MySQL root user password using command `sudo grep 'temporary password' /var/log/mysqld.log`

```sh
# Login w/ password.
# NOTE: no space after `-p` flag. Might try quoting, alternatively.
mysql -u root -pg/io%flE77m
#=> ...
```

Once logged in.
```sql
# Change default user otherwise no other operation can be performed
# NOTE: Script `mysql_secure_installation` ON command line changes user automatically.
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!'
mysql> SHOW DATABASES;
#+> +-----------------+
# | Database         |
# +------------------+
# ...


# Create a new database.
mysql> CREATE DATABASE school

# Switch to a particular db:
mysql> USE school;

# Create table.
mysql> CREATE TABLE persons;

# Show tables.
mysql> SHOW TABLES;

# Add data.
mysql> INSERT INTO persons values ( "John Doe", 45, "New York" );

# Query data.
mysql> SELECT * FROM persons;
```

### Dealing with Use Restrictions

Create User

Root user is the initial user created.
- Has access to all tables
Additional users with table access restrictions can be created.
- __MUST BE DONE IN A PRODUCTION ENVIRONMENT__

```sh
mysql -u root -pg/io%flE77m
```

```SQL
mysql> CREAE USER 'john'@'localhost' IDENTIFIED BY 'MyNewPass4!'
```

Meaning of `'john'@'localhost'`
              ^         ^
           'username'@'host'
If host is local user, 'John' can only connect from localhost and not another server.
- Access would be denied if connecting from another system.
- Allowing user to connect from any server would be done w/ `'%'`.

### Privileges

`Grant` cmd

```sql
mysql> GRANT <PERMISSION> ON <DB.TABLE> TO 'john'@'%';
mysql> GRANT SELECT ON school.persons TO 'john'@'%';
# Multiple permissions in a single command can be provided in a comma separated list.
mysql> GRANT SELECT, UPDATE ON school.persons TO 'john'@'%';
# Grant permission on all tables in a particular database done w/ asterisk
mysql> GRANT SELECT, UPDATE ON school.* TO 'john'@'%';
# Grant all privileges to all tables in all databases.
mysql> GRANT SELECT, UPDATE ON *.* TO 'john'@'%';
# Show privileges for a user
mysql> SHOW GRANTS FOR 'john'@'localhost';
```
