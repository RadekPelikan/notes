 #SIT #networking #server #linux #windows 

- Nastavování přístupových práv
	- Složky
	- Tiskárny
- Založeno na LDAP
- Od WIN 2000[^1]
- Závislé na DNS
- Stromová struktura[^2]

[^1]: Server
[^2]: AD schema


![[AD-1.excalidraw]]
![[AD-2.excalidraw]]

### OPERATION MASTER ROLES

- Správa AD schématu
- Schéma master
- Operations naming[^3] master
- RID[^4] master
- PDC[^5] emulator
- Infrastracture master[^6]

[^3]: Přidává a odebírá domény z lesa
[^4]: Relative Identifier - pro generování SID
[^5]: Primary domain Controller - komunikace s historickými systémy
[^6]: Řídí vztahy mezi storomy na základě katalogu GC (Global catalog)


## Nástroje

### Active Directory User nad Computers

- Kontejnery
	- [[#Builtin]]
	- [[#Computers]]
	- [[#Domain Controllers]]
	- [[#ForeignSecurityPrincipals]]
	- [[#Managed Service Account]]
	- [[#Users]]


#### Builtin

- Výchozí skupiny zabezpečení, které se vytváří při instalaci automaticky
- Nemění se, jen se přidává

#### Computers

- Pracovní stanice, které jsou čerstvě přidané do domény

#### Domain Controllers

- Doménové řadiče

#### ForeignSecurityPrincipals

- Objekty zabezpečení z jiných domén

#### Managed Service Account

- Speciální účty pro určité služby
- Např. SQL server

#### Users

- Výchozí uživatelé při instalaci systému
- Správa uživatelů

### Konfigurace Windows

Nainstalovat `Active Diretory Domain Services`
![[AD-img-1.png]]
![[AD-img-2.png]]
![[AD-img-3.png]]
Pokud je zelená fajfka, všechno cajk
![[AD-img-4.png]]
![[AD-img-5.png]]

Zjistit informace o [[#OPERATION MASTER ROLES]]
![[AD-img-6.png]]

Vytvoření nové kontejneru
![[AD-img-7.png]]
![[AD-img-8.png]]


