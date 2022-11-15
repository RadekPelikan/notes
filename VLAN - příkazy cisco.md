# VLAN - příkazy cisco

## Mod

> **interface `port`** *f0/1*
> - **switchport** \
>   - **mode `mod`** nastavení mod[^1] portu
> 
> #### Konfigurace access portu
> 
> - **switchport** \
>   - **mode access**
>   - **access vlan `n`** která VLAN
> 
> #### Konfigurace trunk portu
> 
> - **switchport** \
>   - **mode trunk**
>   - **nonegotiate**
>   - **trunk** \
>     - **allowed vlan `n`** povolené VLANy, které mohou[^2] proházet tímto portem
>     - **native vlan `n`** Kam jdou netagované rámce, např z internetu

[^1]: Port mody na switchi: [[Cisco#VLAN|access, trunk, transparent]]
[^2]: Číslo nebo rozsah pro určení, které VLANy mohou procházet

## VTP

> **vtp** \
> - **mode** \
>   - **server** nastavuje VLANy pro klienty, ze základu
>   - **client** užívá VLANy z serveru
>   - **transparent** nepoužívá VTP, používá lokální konfiguraci
> - **domain `doména`** ze základu NULL *spsmb.local*

## STP

> **interface `port`** *f0/1*
> - **spanning-tree** \
>   - **portfast** vypne STP, doporučuje se to nastavit na portech kde se vyskytují koncová zařízení

#