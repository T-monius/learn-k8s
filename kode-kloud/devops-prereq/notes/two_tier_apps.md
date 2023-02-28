# KodeKloud Ecommerce Applications

LAMP stack app

- Install firewall
- Install MariaDB
- Configure MariaDB
- Start MariaDB
- Configure Firewall
- Configure Database
- Load Data

## Install Firewall

```sh
sudo yum install firewalld
sudo service firewalld start
sudo systemctl enable firewalld
```

## Install MariaDB

```sh
sudo yum install mariadb-server
sudo vi /etc/my.cnf # configure the file with the right port
```

## Configure MariaDB

```sh
sudo service mariadb start
sudo systemctl enable mariadb
```

## Configure Firewall

```sh
sudo firewall-cmd --permanent --zone-public --add-port-3306/tcp
sudo firewall-cmd --r
```

## Configure Database

```sh
mysql
```

```sql
MariaDB> CREATE DATABASE ecomdb;
MariaDB> CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
MariaDB> GRANT ALL PRIVILEGES ON *.* TO 'ecom'@'localhost'
MariaDB> FLUSH PRIVILEGES;
```

## Load Data

```sh
mysql < db-load-script.sql
```

{Minute 3:30}
