# OPS příkazy

#SIT #OPS

**ifconfig**
**ip a**
**ipconfig** - windows
**route -n** routovací tabulka
**route print** - windows
**netstat -r** - obě
**ping**

## Linux

ifconfig
ip a
route -n
netstat -r
ping
traceroute
ifdown `rozhraní`
ifup `rozhraní`

## Windows

ipconfig
route print
netstat -r
ping
tracert

## Konfigurační soubory

#### /etc/network/interfaces
 
síťové rozhraní
- inet je protokol

**Obsahuje:**
``` 
source /etc/network/interfaces.d/*

auto lo
iface lo inet loopback

allow-hotplug eth0
iface eth0 inet dhcp

allow-hotplug eth1
iface eth1 inet static
	address 10.0.0.1/24
```



#### /etc/resolv.conf - dns
#### /etc/hosts  - překlad názvů
#### /etc/nsswitch.conf  - nastavuje z jakých zdrujů se čerpají informace

## Statusové příkazy

`nslookup ns1`

## Práva souborů

```
chmod nnn soubor
chmod u=...,g=...,o=... soubor
chmod u+-...,g+-...,o+-... soubor

chown novy_vlastnik soubor
chown novy_vlastnik:nova_sk soubor
chown :nova_sk soubor
chgrp nova_sk soubor
```