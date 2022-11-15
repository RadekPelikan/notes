# DNS

- Domain name system
- Mapování jmenných názvů na IP adresy a obráceně
 - Stromová struktura
 - Doménová jména se skládají z jednotlivých úrovní
 - Hledání v systému DNS probíhá rekurzivně
 - Hledání probíhá v jednotlivých DNS serverech, každý server má část stromu
![[DNS-1.excalidraw]]
![[DNS-2.excalidraw]]

### Servery

- [[DNS#Kořenové|Kořenové]]
- [[DNS#Autoritativní|Autoritativní]]
- [[DNS#Rekurzivní|Rekurzivní (cashovací)]]

#### Kořenové

- Starají se o kořenovou doménu `.` - záznamy o serverech, které mají na starosti domény 1. úrovně
- Celkem je jich 13 (logický počet[^1])

[^1]: Fyzicky jich je mnohem více, jsou mezi sebou zrcadlené

- 13 je jich proto, aby se všechny servery v dotazy vešly do 1 UDP packetu (512 B)
- Označují se písmeny abecedy A-M
- Dotaz je směrován pomocí anycastu
- Směrován je na nejbližší fyzický server

#### Autoritativní

- Obsluhují záznamy z kokretní části DNS stromu (domény)
- Informace jsou uloženy v zónových souborech

#### Rekurzivní

- Rekurzivní dotazy v DNS stromu
- Dotazy se ukládají do cache
- Snižují zátěž především kořenových serverů


### Zóny


#### Dopředná

- Forward zóna
- Mapuje jmenné názvy na IP adresy
- SOA, NS, A, AAAA, CNAME, MX


#### Zpětná

- Reverse zóna
- Mapuje IP adresy na doménové názvy
- SOA, NS, PTR
- 2 typy:
	- [[DNS#Zpětná zóna#IPv4|IPv4]]
	- [[DNS#Zpětná zóna#IPv6|IPv6]]


##### IPv4

- `in-addr.arpa`

##### IPv6

- `ip6.arpa`


### Záznamy

#### A

- Mapuje název na IP adresu
- www - IN - A - 10.0.0.1
- IPv4


#### AAAA

- Jako [[DNS#Záznamy#A|A]], ale slouží pro IPv6


#### CNAME

- Alias
- Jiný název pro již existující název
- `server    IN    CNAME    www`

#### MX

- Mail eXchange
- Směřuje elektronickou poštu
- `seznam.cz    IN    MX    10    poštovní_server`
- Číslo 10[^2]

[^2]: Priorita
vyšší - nejniší priorita
nižší - vyšší priorita

#### NS

- Nam server
- Záznamy o autoritativních serverech pro danou doménu
- `seznam.cz    IN    NS    adresa_DNS_serveru`

#### PTR

- Pointer
- Mapuje IP adresu na jmenná název
- Pouze v [[DNS#Zóny#Zpětná|reverzní zóně]]
- `10    IN    PTR    jmenný_název`

#### SOA

- Start of Authority
- Označuje začátek zóny v zónovém souboru
```
Zóna IN SOA primární_jemmý_server email_správce
	serial   - seriové číslo zóny (id)
	refresh  - jak často si mají zónu stahovat
				sekundární DNS servery  
	retry    - pokus se nepodaří refresh, za 
				jak dlouho se má refresh opakovat   
	expire   - pokud se nepodaří sekundární server
				zaktualizovat, ádaje po vypršení 
				expire na sec. serveru budou neplatné    
	ttl      - cachování dotazů 
				(u bind serveru v linux jde o negativní cache)
```

### Nástroje

- nslookup - windows
- host - linux
- dig - linux


### Konfigurace Linux

Ip adresa: 10.0.0.0/24

Nainstalovat balíčky `bind9`, `bind9utils`, `bind9-doc`

##### Vysvětlivka
```
192.168.5.0/24
5.168.192.in-addr.arpa

10.5.5.0/16
5.10.in-addr.arpa
```

#####

Soubor `/etc/default/bind9`
```
RESOLVCONF=yes
OPTIONS="-u bind"
#OPTIONS="-u bind -4"
```

Jít do složky `/etc/bind`
Vytvořit složku zones
```
mkdir zones
```

Zkopírovat defaultní db do zones
```
cp db.empty zones/db.radkon.local
cp db.empty zones/db.10.0.0
```

Upravit `named.conf.options`
```
acl "povoleno" {
	127.0.0.0/8;
	10.0.0.0/24;	
};

options {
	directory "/var/cache/bind";

	forwarders {
		8.8.8.8;
		8.8.4.4;
	}
	dnssec-validation no;
	listen-on-v6 { none; };
	listen-on { 127.0.0.1; 10.0.0.1; };
	allow-recursion { povoleno; };
	allow-transfer { none; };
	auth-nxdomain yes;
};
```

Upravit `named.conf.local`
```
zone "radkon.local" {
	type master;
	file "/etc/bind/zones/db.radkon.local";
	allow-transfer { none; };	
};

zone "0.0.10.in-addr.arpa" {
	type master;
	file "/etc/bind/zones/db.10.0.0"
	allow-transfer { none; };
};
```

Jít do složky `zones`
Upravit `db.radkon.local`
```
$TTL    86400
@       IN      SOA     ns1.radkon.local. admin.radkon.local. (
				     2022100701         ; Serial
						 604800         ; Refresh
						  86400         ; Retry
						2419200         ; Espire
						  86400 )       ; Negative Cache TTL
;
@       IN      NS      ns1.radkon.local.
ns1     IN      A       10.0.0.1

test    IN      CNAME   ns1
```

Upravit `db.10.0.0`
```
$TTL    86400
@       IN      SOA     ns1.radkon.local. admin.radkon.local. (
				     2022100701         ; Serial
						 604800         ; Refresh
						  86400         ; Retry
						2419200         ; Espire
						  86400 )       ; Negative Cache TTL
;
@       IN      NS      ns1.radkon.local. 
1       IN      PTR     ns1.radkon.local.
```
#### Příkazy

```
- Syntaxe
named-checkconf
named-checkzone radkon.local db.radkon.local
named-checkzone 0.0.10.in-addr.arpa db.10.0.0

- restart
systemctl restart bind9
- status
systemctl status bind9
```