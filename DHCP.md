# DHCP

#SIT #OPS 

[learniit.text](https://learniit.tech/site/dhcp-server-linux)


![[DHCP-1.excalidraw]]


### Zprávy

#### DHCPNAK

Zamítne request, když nové zařízení žádá o obnovu
Posílá server

#### DHCP DECLINE

Klient odmítá nabídnutou IP adresu
Odmítá, když IP adresa je už obsazená v dané síti

#### DHCP RELEASE

Klient vrací IP adresu, kterou už nepotřebuje
Když klient uvolní IP adresu


#### DHCPINFORM

Zpráva s dodatečnými informace
Posílá klient


###

#### DHCP RELAY

Služba na routeru
Router překládá broadcast na unicast
A posílá informace o síti

![[DHCP-2.excalidraw]]



### Linux

Nainstalovat balíček `isc-dhcp-server`

Soubor `/etc/default/isc-dhcp-server`
```
INTERFACESv4="eth1"
#INTERFACESv6=""
```

Soubor `/etc/dhcp/dhcpd.conf`
```
#option domain-name "example.org";
#option domain-name-servers nsi.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-stule none;

authoritative;

log-facility local7;

subnet 10.0.0.0 netmask 255.255.255.0 {
	range 10.0.0.21 10.0.0.50;
	option domain-name-servers 8.8.8.8,8.8.4.4;
	# Pokud je nakonfigurovan DNS server
	#option domain-name-servers 10.0.0.1;
	option domain-name "radkon.local";
	option routers 10.0.0.1;
	default-lease-time 600;
	max-lease-time 7200;

	# rezevace
	host klient {
		hardware ethernet `MAC ADRESA`;
		fixed-address 10.0.0.10;
	}
}
```

local7 je úroveň logovaných informací

#### Příkazy

```
- restart
systemctl restart isc-dhcp-server.service
- status
systemctl status isc-dhcp-server.service

```