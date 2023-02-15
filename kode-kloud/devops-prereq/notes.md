# Notes

## Services

useful commands
```sh
systemctl start srvc
systemctl stop srvc
systemctl status srvc
systemctl enable
systemctl disable
systemctl daemon-reload
# or
service srvc start
# access a networked device
ssh root@xxx.xxx.xx.x.x
```

file locations
```sh
/etc/systemd/system
```

## Networking

useful commands

```sh
# show the routing table
route
ip addr
ip addr add xxx.xxx.x.xx/xx dev eth0
# configure a gateway for a device
ip route
ip route add xxx.xxx.x.x/xx via xxx.xxx.x.x
# set a default for any unknown destination
ip route add default via xxx.xxx.x.x
```

important file locations
```sh
# Default to 0 for non-forwarding. Optionally set to 1
/proc/sys/net/ipv4/ip_forward
# persist state like forwarding ^
/etc/systl.conf
# => net.ipv4.ip_forward = 1
```

## DNS

__Video__

Initial premise: like to `ping` a service on the network by an alias.
- How to add?
  - `/etc/hosts`
    - add entry
    - Source of truth for a given host
  ```sh
  ping db
  #=> ping unknown host db

  # After adding
  cat >> /etc/hosts
  #=> xxx.xxx.x.xx      db
  ping db
  #=> PING db (xxx.xx.x.xx) ... bytes of data
  ```
  - Can even overwrite a well-known site (i.e. www.google.com) in `/etc/hosts` and spoof
  - Arbitrary number of hosts can be stored in file
  - This type of host mapping called _name resolution__
- Managing large host files too difficult, inefficient
  - Knowledge of mappings moved to DNS servers
  - Hosts can be configured to contact a given DNS server
  - `/etc/resolv.conf`
    - stores DNS for
  - Entries can be stored in host file as well
  - Host priority set in separate file
    - `/etc/nsswitch.conf`
  - Unknown hosts can be set to be resolved as well
    - Example, `8.8.8.8` well known Google DNS
- Domain Names
  - translate ips to something human readable
  - Can have subdomains like `mail`, `drive`, `www`
- Search Domain
  - Can alias Domain Names by setting in `/etc/hosts` file:
    - `search     mycompany.com`
    - `ping web.mycompany.com #=> now resolves`
- Record Types
  | A | Web-server | 192.168.1.1 |
  | AAAA | web-server | 2001:0db8:85a3:0000:0000:8a2e:0370:7334 |
  | CNAME | food.web-server | eat.web-server, hungry:web-server |
- Alternative search tools
  - Besides `ping`
  - `nslookup`, queries local DNS
  - `dig`
