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


