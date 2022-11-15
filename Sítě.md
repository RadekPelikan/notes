# Sítě

#SIT

> Port je 16ti bitové číslo
> IPv4 je 32 bitové číslo
> IPv6 je 64 bitové číslo

### Užitečné odkazy

> [Toolkit](http://toolkit.g6.cz)
> [Wintelguy](https://wintelguy.com)
> [Samuraj](https://samuraj-cz.com)

### [[VLAN]]

> [Vlany samuraj](https://www.samuraj-cz.com/clanek/vlan-virtual-local-area-network/)

### Rozdělení switchu

> **L2 switch** Linková vrstva
> **L3 switch** Síťová vrstva (switch umí i routovat) 

## Routování

> Aplikuje se na síťové vrstvě OSI modelu - 3.

> ### IPv4
> 
> 4 miliardy adres $2^{32}$
> Adresy musí být jedinečné
> **Oktet** je jedna 8mi bitová část adresy
> 3 privátní rozsahy adres: #privatniAdresy
	> - 10.0.0.0/8
	> - 172.16.0.0/12
	> - 192.168.0.0/16
> 	
> ### [[IPv6]] 

> ### Routovací protokoly
> 
> [[Statické routovací protokoly|Statické]]
> [[Dynamické routovací protokoly]]
> Defaultní
	> - Všechno nuly
	> - Dříve připojoval k internetu

### VLSM

> Variabilní délka masky
> Potřebná kvůli nedostatku adres

### Podsítě

> Počítání použitelných IP adres
> **První a poslední** adresy **nelze** použít pro **hosta**
> Použitelných adres je vždy o 2-3[^1] méně
> Začínáme podsítí s největším počtem hostů
> Zvětšením prefixu o 1 půlíme počet možných adres
> Poslední reálně použitelný prefix je 30
> Pro **propojení routerů** vždy prefix **30**

[^1]: 2-3 protože 2 jsou vyhrazeny pro adresu sítě a adresu broadcastu ta třetí by mohla být obsazena [[Default gateway|default gateway]]

Prefix | Počet adres | Použitelné adresy[^2]
-- | -- |--
30 | 4    | 2
29 | 8    | 6
28 | 16   | 14
27 | 32   | 30
26 | 64   | 62
25 | 128  | 126
24 | 256  | 254
23 | 512  | 510
22 | 1024 | 1022
21 | 2048 | 2046
20 | 4096 | 4094

[^2]: Jen adresa sítě a adresa broadcastu, takže **-2** od **Počet adres**

## [[Cisco]]
#