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
