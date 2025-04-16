#### 1) Charakteristika dynamických routovacích protokolů
##### Interior Gateway Protocol (IGP)  
- Směrování paketů v rámci **dané směrovací domény**
##### Link-state  
- Alternativa k **distace-vector protokolu RIP** (Routing Information Protocol)  
- Rychlejší **konfigurace a lepší škálovatelnost** pro větší sítě
##### RIP (Routing Information Protocol)
- Možnost **smyček**, **špatně škálovatelné** pro větší sítě
- **Distance vector**
- Každých 30 sekund posílá **celou routovací tabulku**, **omezený maximální počet skoků**
##### OSPF  (Open Shortest Path First)
1) **Využívá koncept oblastí** (`areas`)  
  - Komplexní síť s mnoha routery lze pro zajištění efektivní výměny směrovacích údajů rozdělit na samostatné části (`areas`)  
1) **Jako spoj** (`link`) **routeru se chápe**:  
  - Síťové rozhraní  
  - Síťový segment  
  - Koncová síť (`stub network`)  
1) **Stav spoje** (`link-state`) **zahrnuje**:  
  - Adresu sítě  
  - Délku prefixu  
  - Cenu (`cost`)  
#### 2) OSPF – druhy, vlastnosti a možnosti nasazení
##### Součásti protokolu OSPF  
1) **Zprávy** (pakety):
	- Pro výměnu směrovacích informací  
2) **Datové struktury** (databáze):  
	- Uchovávají informace pro další zpracování a vlastní činnost  
3) **Směrovací algoritmus**:
	- Umožňuje nalezení optimálních cest sítí  
##### Datové struktury protokolu OSPF  
1) **Adjacency Database a Neighbor Table**:
  - Obsahuje všechny sousední routery  
  - Jedinečná pro každý router  
  - Lze zobrazit příkazem `show ip ospf neighbor`  
2) **Link-state Database** (`LSDB`) **a Topology Table**:  
  - Údaje o všech ostatních routerech v oblasti  
  - Reprezentuje topologii celé sítě  
  - Lze zobrazit příkazem `show ip ospf database`  
3) **Forwarding Database a Routing Table**:  
  - Obsahuje cesty sítí generovaných algoritmem dle obsahu `LSDB`, které jsou jedinečné pro každý router v síti  
  - Lze zobrazit příkazem `show ip route`
##### Směrovcí algoritmus protokolu OSPF  
1) **Používá algoritmus** `SPF` (**Shortest Path First**):  
  - Který vychází z Dijkstrova algoritmu  
2) **Vyhodnocuje kumulativní cesy k cíli**:
  - Cena použití daného spoje může být určena automaticky nebo manuálně  
3) **Výsledkem algoritmu je strom možných cest sítí**:  
  - Aktuální router je umístěn do jeho kořene  
  - Nejlepší cesty jsou vloženy do `Forwarding Database`  
  - Z nich jsou poté sestavena pravidla do směrovací tabulky
##### Metrika ceny cesty (path cost)
- Metrika určuje **vhodnost cesty** k zaslání paketu směrem k cíli, **čím nižší cena, tím lepší cesta**
- Cena cesty je určena **výpočtem z rychlosti rozhraní**
	- `Cena = Referenční rychlost / Rychlost rozhraní`
	- Výchozí referenční rychlost je `100 Mbit/s`
	- Výsledná cena musí bát kladné celé číslo větší než nula (problém pro `FastEthernet` a `GigabitEthernet` a rychlejší, vyjde vždy 1)
##### Princip činnosti OSPF  
1) **Stanovení vztahu sousednosti** (`Neighbor Adjacencies`) 
	- Každý router pošle` Hello paket` se svým `Router-ID` na multicastovou adresu `224.0.0.5`
	- `Router-ID` je identifikátor routeru v ``OSPF`` oblasti jako `32 bitové` číslo
	- Příjme-li router `Hello paket` s neznámým `Router-ID`, pokusí se s ním navázat vztah sousednosti (Pokud dané `Router-ID` zná tak vztah pouze udržuje)
2) **Výměna údajů o stavu spojů** (`Link-state Advertisements`)  
3) **Sestavení databáze stavu spojů** (`Link-state Database`, `LSDB`)  
4) **Spuštění algoritmu** `SPF`
5) **Výběr nejlepších cest sítí**
##### Možnost implementace OSPF  
1) `OSPF` podporuje **hierarchické směrování** pomocí oblastí  
  - Oblast (area) je skupina routerů sdílejících údaje o stavech spojů  
  - Všechny routery v dané oblasti mají totožný oblast LSDB  
2) `OSPF` **lze implementovat dvěma způsoby**:  
	1) `Single-area OSPF`:  
    - Všechny routery v jediné oblasti (zpravidla 0)  
	2) `Multi-area OSPF`:
    - Routery v různých oblastech, které jsou hierarchicky uspořádané  
    - Všechny oblasti musí být propojeny s páteřní (backbone) oblastí 0
##### Point-to-Point spoj
- Nedochází k volbě `BR` a `BDR`
- U spojů **Serial automaticky**
- U spojů **Ethernet explicitně**

##### Pasivní rozhraní
- Nekomunikuje s dalšími `OSPF` routery
	- Zabraňuje hledání sousedních OSPF routerů
	- Nasazením pasivního rozhraní se omezí zátěž sítě a sníží se bezpečnostní rizika vyplývající z nasazení OSPF
##### OSPFv2  
- Podpora **pouze** `IPv4`  
- Pro vzájemnou komunikaci routerů se používá `IPv4`  
##### OSPFv3  
- Podporuje `IPv6` i `IPv4`  
- Pro vzájemnou komunikaci routerů používá `IPv6`  
- Běží nezávisle na `OSPFv2`
- Příkazy na konfiguraci jsou velmi podobné ``OSPFv2``
##### Provozní stavy OSPF
1) **Down**:
	- Router odesílá `Hello pakety` na daném rozhraní
	- Router přijímá `Hello paket` od souseda
2) **Init**:
	- Router odesílá pakety s `RID` daného souseda
	- Router přijímá `Hello Paket` s vlastním `RID`
3) **Two-way** (v tomto stavu zůstávají sousední routery, které nejsou `DR` ani `BDR`):
	- Routery si vzájemně vyměňují `Hello pakety`
	- Pokud jsou oba routery propojeny spojem `Point-to-Point`, přejdou do stavu `ExStart`
	- Pokud jsou oba routery propojeny `Ethernet` spojem, dojde k volbě `DR` a `BDR`:
		- Router, který má nejvyšší prioritu nebo Router-ID se stane DR
		- Router, který má druhou nejvyšší prioritu nebo Router-ID se stane BDR
4) **ExStart** (pouze pro `Point-to-Point` sítě):
	- Routery si vzájemně vyměňují `DBD` pakety s příznaky
	- Dojde k dohodě, kdo první pošle `DBD` a s jakým sekvenčním číslem
5) **Exchange**:
	- Routery si vzájemně vyměňují `DBD` pakety s `LSA`
	- Dojde ke vzájemné výměně záznamů `LSDB`
	- Po stavu `Two-Way` routery přejdou do stavů synchronizace svých databází
6) **Loading** (Pouze pokud je třeba získat podrobnosti o určitém spoji)
	- Routery si vyměňují `LSR`, `LSU` a `LSAck` pakety, `SPF` algoritmus určí cesty
	- Dojde k získání konzistentní podoby `LSDB` mezi oběma routery
7) **Full**:
	- `LSDB` je mezi routery plně synchronizována
	- Pokud nepříjde `Hello paket` v časovém limitu, přejde do stavu `Down`
##### Význam role Designated Router (DR)
1) `Multiaccess` sítě přinášejí dvě výzvy: 
	- Existenci mnoha vztahů sousednosti
	- Negativní dopady LSA floodingu
2) Pokud selže `DR`, router v roli` BDR` se stane novým `DR` a je zvolen nový router v roli `BDR`
##### Routery v roli DR a BDR
- Přijímají aktualizace stavu spojů od ostatních routerů
- Zasílají aktualizace stavu spojů ostatním routerům
##### Ostatní Routery (DROTHER)
- Zasílají aktualizace stavů spojů pouze routerů DR a BDR
- Přijímají aktualizace stavu spojů výhradně od DR nebo BDR
#### 3) OSPF pakety
##### Zprávy protokolu OSPF  
1) **Hello Packet**:
  - Informuje o přítomnosti daného routeru na síťovém segmentu
  - Zajišťuje zjištění `OSPF` sousedů, předává parametry nutné pro vzájemnou spolupráci a pokud se neshodují, vztah nevznikne
  - Volba routeru v roli `DR` (Designated Router) a `BDR` (Backup Designated Router), netýká se spojů `Point-to-Point`
2) **Database Description Packet** (`DBD`)
  - Shrnuje aktuální stav link-state databáze (`LSDB`)  
3) **Link-state Request Packet** (`LSR`)
  - Žádost o poskytnutí údajů o stavu daného spoje  
4) **Link-state update Packet** (`LSU`)
  - Předává údaje o stavu daného spoje
  - Používá se také pro zasílání aktualizací stavu spojů, v tomto případě mu `LSR` paket nepředchází
  - LSU může obsahovat až 11 různých druhů `LSA` (Link-State Advertisement) bloků
5) **Link-state Acknowledgment Packet** (`LSAck`)  
  - Potvrzení přijetí údajů o stavu daného spoje
#### 4) OSPF konfigurace
##### Režim konfigurace routeru pro OSPF
1) Příkaz `router ospf {id procesu}`, platí pouze v rámci daného routeru a je vhodné si zvolit stejné ID pro všechny routery v oblasti
2) `Router-ID` lze nastavit explicitně příkazem `router-id {id}` nebo se nastavuje automaticky:
	1) Dle nejvyšší `IP` adresy loopback rozhraní
	2) Dle nejvyšší `IP` adresy aktivního rozhraní
	- Ověřit `Router-ID` lze příkazem `show ip protocols`
3) OSPF proces lze restartovat příkazem `clear ip ospf process`
##### Konfigurace sítě Point-to-Point a Multi-Access
- **Základní způsoby přiřazení rozhraní k oblasti**:
	1) `network {subnet-ip} {wildcard-mask} area {area}`
		- V režimu konfigurace `OSPF` procesu
		- IP adresa sítě s `wildcard` maskou určuje rozhraní (lze sumarizovat)
		- Lze zadat přímo rozhraní bez s `wildcard` maskou `0.0.0.0`
	2) `ip ospf {process-id} area {area-id}`
		- Zadáván v režimu konfigurace jednotlivých rozhraní
- **Pasivní rozhraní**:
	- `passive-interface {interface}` v režimu konfigurace OSPF procesu
	- Ověřit lze příkazem `show ip protocols`
- **Point-to-Point**:
	- `ip sopf network point-to-point` v režimu konfigurace rozhraní
- `show ip ospf interface {interface}` pro zobrazení podrobností o daném rozhraní
- `show ip ospf neighbor` zobrazí stavy a role sousedních routerů včetně připojených rozhraní
- `ip ospf priority` v konfiguračním režimu pro nastavení OSPF priority
- `auto-cost reference-bandwidth {rychlost v Mbit/s`" v konfiguračním režimu pro nastavení referenční rychlosti ceny nebo příkaz `ip ospf cost {cena}`
- `default-information originate` v konfiguračním režimu pro automatický přenos výchozí cesty v rámci OSPF
### Kvízy  
[HS (I4.D) – 1.1. Vlastnosti a možnosti využití OSPF]([https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQVFNODVXNzYzRjFOQ0dJSEYzNTFEMFRCNi4u&route=shorturl)](https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQVFNODVXNzYzRjFOQ0dJSEYzNTFEMFRCNi4u&route=shorturl\) "https://forms.office.com/pages/responsepage.aspx?id=iw_r_ignr0ifnafpxpzo2vxvcnwt1thbn0p9mknr0-puqvfnodvxnzyzrjfoq0djseyzntfemfrcni4u&route=shorturl)")
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUM01UM0dWOTdWRFFLOEgwMkkyVVkzQks5QS4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUNjRMUEJDQVhEVkZFOFRVMFo0UkFRRlc1Ni4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUMUFMUzJTUENVMUtBUk5QNVM5Mko5M0lYRi4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUOFlSNURYUzE3MDVBVUw4QTNSVDdNUTRETC4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQlJaMzYwRzNRSkVCWDNGQ00zVjYxQ0JVSy4u&route=shorturl