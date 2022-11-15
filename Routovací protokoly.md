# Routovací protokoly

#SIT

## Statické

- Definované z bodu A do bodu B
- 
- Pokud je spojení přerušeno, cesta zanikne
- Použito jen na malé sítě

## Dynamické

- Nejpoužívanější
- Reaguje na změnu topologie
- Pokud je cesta přerušena, najde se nová

### Exterior gateway protocol (EGP)

- BGP
- Path vector
- Propojuje autonomní systémy
- Velké sítě (O2, Vodafon, ...)

### Interior gateway prototocol (IGP)

- Vně autonomních sítí

#### Distance vector

- Hledá co nejnižší počet hopů
- RIP, RIP2, RIPNG
- IGRP, EIGRP

#### Link state

- Hledá nejlepší cestu
- OSPF
- IS-IS

## Default

- Používá se na přestup do internetu
- Samé nuly