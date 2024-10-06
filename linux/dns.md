# DNS

# Install DNS
install bind9
```
apt install bind9
```

# Configure DNS
## Configure Forward
enter bind
```
cd /etc/bind/
```
copy db.local to db.forward
```
cp db.local db.forward
```
configure forward 
```
vim db.forward
```
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     academy.id. root.academy.id. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@         IN      NS      academy.id.
@         IN      A       172.23.15.150
www       IN      A       172.23.15.150
blog      IN      A       172.23.15.150
```

## Configure Reverse
copy file db.127 to db.reverse
```
cp db.127 db.reverse
```
configure reverse
```
vim db.reverse
```
```
; BIND reverse data file for local loopback interface
;
$TTL    604800
@       IN      SOA     academy.id. root.academy.id. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      academy.id.
150     IN      PTR     academy.id.
```
## Configure Zone
```
vim named.conf.default-zones
```
```
zone "academy.id" {
        type master;
        file "/etc/bind/db.forward";
};

zone "15.23.172.in-addr.arpa" {
        type master;
        file "/etc/bind/db.reverse";
};
```
## Install Resolvconf
install tools resolvconf
```
apt install resolvonf
```
## Configure Resolvconf
configure nameserver
```
vim /etc/resolvconf/resolv.conf.d/head
```
```
nameserver 172.23.15.150
```
update nameserver
```
resolvconf -u
```

## Bind9 Testing
restart service bind9
```
systemctl restart bind9
```
check with nslookup
```
nslookup 172.23.15.150
nslookup academy.id
```
check with ping 
```
ping academy.id
ping blog.academy.id
```
