# Vzdálený přístup - příkazy cisco

## SVI

> Nastaví IP adresu na virtální rozhraní/port
> **interface vlan `n`**
> - **ip address `ip` `maska`**

## Telnet

> **line vty `n` `n`** *0, 1*
> - **password `text`** *cisco*
> 
> **enable secret `text`** *cisco*[^1]
> **enable password `text`** *cisco*

[^1]: Secret a password dělají dost podobnou věc, akorát secret "zahashuje" to heslo

## SSH

> **line vty `n` `n`** *0, 1*
> - **password `text`** *cisco*
> 
> **enable secret `text`** *cisco*[^1]
> **enable password `text`** *cisco*
> **username `text` secret `text`** *cisco, cisco*
> **ip ssh** \
> - **time-out `n`** *60*
> - **authentication-retries `n`** *3*
> - **version `n`** *2*  
> 
> **ip domain name `text`** *spsmb.local*
> **hostname `text`**
> **crypto key generate rsa**6

## Vypnout Telnet

> **line vty `n` `n`** *0, 1*
> - **transport input ssh**

## Router připojení k LAN s VLANy

> **interface `port`.`port`** *g0/0, 10*
> - **encapsulation dot1Q**[^2]
> - **encapsulation dot1Q `n` native** *10*
> - **ip address `ip` `maska`**
> 
> **interface `port`** *g0/0*
> - **no shutdown**
> 
> #### Privilegovaný mod
> 
> **show ip interface brief**

[^2]: native napíšeme jen zda-li je určitá VLANa nativní v dané LANce

#
