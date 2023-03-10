# Web Servers

## Apache Web Server

Open source HTTP server
- Web server, generally used to serve web content
- Generally used in conjunction with an application server that is used for backend logic, like Apache Tomcat

Included in CentOS default software repository
- Simply install and start `httpd` service

```sh
yum install httpd
service httpd start
service httpd status
# httpd.service - The Apache HTTP Server
#   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; ...)

# If a firewal is configured, add a rule to allow http traffic
firewall-cmd --permanent --add-service=http
```

Every service has a log.

```sh
# Show log for httpd service
cat /var/log/httpd/access_log
# ::1 - - ...
cat /var/log/httpd/error_log
# [Sun Mar 22 ...]
```

Every server has a configuration file.

`/etc/httpd/conf/httpd.conf`
```
#
# Listen: Allows you to bind Apache to specific IP addresses and/or
# print...
Listen 80

# ...
DocumentRoot "/var/www/html"

# ...
SErverName www.houses.com:80

# ...

<VirtualHost *:80>
  ServerName www.houses.com
  DocumentRoot /var/www/houses
<VirtualHost>
```

- `Listen` defines on what port the server listens
- `DocumentRoot` defines where static content is stored.
- `ServerName` defines name of a server
  - Must define in DNS
  - Workaround, is to add an entry in `/etc/hosts`

A single apache server can host multiple websites
- To do so, the config file of each website is designed as as virtual host
- In Apache config file, a `VirtualHost` section defines additions
  - Relevant docs defined in `DocumentRoot` directories
- Requests directed to the same port (e.g. `80`) may reference different websites, but will be served from different repos depending on the name.

Any changes in the configuration require a restart (`service httpd restart`)

Each virtual host configuration can be moved to it's own configuration file.
- `Include` keyword would make external configuration files avaailable from main config file.

## Apache Tomcat

Provides an environment to host Java based web applications

Must have jave installed
Install Tomcat from [Apache Tomcat download page](http://tomcat.apache.org/download-80.cg)

```sh
wget http://tomcat.apache.org/tomcat/tomcat-8/v8.5.53/bin/apache-tomcat-8.5.53.tar.gz

tar xvf apache-tomcat-8.8.53.tar

# start server by running startup script in bin directory

./apache-tomcat-8.5.53/bin/startup.sh
```

Visit port 8080 to see built in webpage

In Tomcat directory,
- Within `bin`, `.bat` files are for Windows and `.sh` for linux
- In `conf` directory store multiple configurations
- `webapps` stores applications run by Tomcat

Before deploying, package w/ `war` instead of `jar` since it's a web application. Alternatively, build packages like Maven or Gradle can package.

If Tomcat is running when the `war` file is placed in the `webapps` directory, Tomcat will automatically detect it.

## Flask

Typical Python Project Structure

- application
  - LICENSE
  - README.md
  - requirements.txt
  - main.py
  - utils
  - tests
  - config
  - router
  - services
  - db
  - core

Starting a python app locally usually runs in on port 5000

Production deployment
- Gunicorn
  - `gunicorn main:app`
  - Gunicorn will host a serve that will send the app at port `8000` by default and can have multiple workers running the code.
- uWSGI
- Gevent
- Twisted Web

## Express.js

Project Structure
- my-application
  - LICENSE
  - README.MD
  - package.json
  - app.js
  - public
  - tests
  - config
  - routes
  - services
  - db
  - core

Production Run Tools

- supervisord
- forever
- pm2

### pm2

Processor manager
- Built in load balancer

cmds:
```sh
pm2 start app.js
# Run 4 instances
pm2 start app.js -i 4
```

## IP Addresses and Ports from a Wed Application Perspective

IP Address
- IP address is assigned to an interface
  - Wired interfaces to connect to a LAN network
  - Wireless interfaces to connect to a wifi
  - ETc.

A laptop (ex. enp0s3) connected to a switch via an ethernet port on a home network would get an IP address assigned (ex. 10.0.2.15)

```sh
ip addr show
#=> 2: enp0s3: ...
# state of UP group default qlen 1000
# ...
# inet 10.0.2.15/24 ...
```

Connecting the same laptop a difference interface like a wifi connection (wlp0s2), it would receive a separate IP address for the new interface (10.0.2.16).

```sh
ip addr show
#=> 2: enp0s3: ...
# state of UP group default qlen 1000
# ...
# inet 10.0.2.15/24 ...

# 3: wlp0s2 ...
# ...
# inet
# inet 10.0.2.16 ...
```

The same laptop now has two separate IP addresses on the same network.

Each network interface card is divided into multiple logical components called __ports__.

A server listens on a given port.

To make an application available on any connected interface, the _host must be declared on `0.0.0.0`_.

When no host is specified, the server listens automatically on the loop back interface (i.e. `127.0.0.1`)

Information about the _loop back interface_ is also available w/ `ip addr show` with name `lo`:

```sh
ip addr show
#=> 1: lo: <LOOPBACK,UP,LOWER,LOWER_UP>
# ...
# inet 127.0.0.1.0/8 scope hose lo
# ...
```

Every host has a loopback set up.
- Anything sent to loopback is like referencing one's self.
- From within the host, to tests one's own application, it can be references.
- Not available from any other host.
- `localhost` is the default name.
