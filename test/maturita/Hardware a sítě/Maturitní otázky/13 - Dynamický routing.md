#### 1) Charakteristika dynamických routovacích protokolů

##### Interior Gateway Protocol (IGP)  
- Směrování paketů v rámci dané směrovací domény

##### Link-state  
- Alternativa k distace-vector protokolu RIP (Routing Information Protocol)  
- Rychlejší konfigurace a lepší škálovatelnost pro větší sítě

##### OSPF  
- Využívá koncept oblastí (areas)  
  - Komplexní síť s mnoha routery lze pro zajištění efektivní výměny směrovacích údajů rozdělit na samostatné části (areas)  
- Jako spoj (link) routeru se chápe:  
  - Síťové rozhraní  
  - Síťový segment  
  - Koncová síť (stub network)  
- Stav spoje (link-state) zahrnuje:  
  - Adresu sítě  
  - Délku prefixu  
  - Cenu (cost)  
#### 2) OSPF – druhy, vlastnosti a možnosti nasazení

##### Součásti protokolu OSPF  
1) Zprávy (pakety)  
	- Pro výměnu směrovacích informací  
2) Datové struktury (databáze)  
	- Uchovávají informace pro další zpracování a vlastní činnost  
3) Směrovací algoritmus  
	- Umožňuje nalezení optimálních cest sítí  
##### Datové struktury protokolu OSPF  
- Adjacency Database a Neighbor Table  
  - Obsahuje všechny sousední routery  
  - Jedinečná pro každý router  
  - Lze zobrazit příkazem "show ip ospf neighbor"  
- Link-state Database (LSDB) a Topology Table  
  - Údaje o všech ostatních routerech v oblasti  
  - Reprezentuje topologii celé sítě  
  - Lze zobrazit příkazem "show ip ospf database"  
- Forwarding Database a Routing Table  
  - Obsahuje cesty sítí generovaných algoritmem dle obsahu LSDB, které jsou jedinečné pro každý router v síti  
  - Lze zobrazit příkazem "show ip route"  
##### Směrovcí algorytmus protokolu OSPF  
- Používá algoritmus SPF (Shortest Path First)  
  - Který vychází z Dijkstrova algoritmu  
- Vyhodnocuje kumulativní cesy k cíli  
  - Cena použití daného spoje může být určena automaticky nebo manuálně  
- Výsledkem algoritmu je strom moných cest sítí  
  - Aktální router je umístěn do jeho kořene  
  - Nejlepší cesty jsou vloženy do Forwarding Database  
  - Z nich jsou poté sestavena pravidla do směrovací tabulky

##### Metrika ceny cesty (path cost)
- Metrika určuje vhodnost cesty k zaslání paketu směrem k cíli, čím nižší cena, tím lepší cesta
- Cena cesty je určena výpočtem z rychlosti rozhraní
	- Cena = Referenční rychlost / Rychlost rozhraní
	- Výchozí referenční rychlost je 100 Mbit/s
	- Výsledná cena musí bát kladné celé číslo větší než nula (problém pro FastEthernet a GigabitEthernet a rychlejší, vyjde vždy 1)
##### Princip činnosti OSPF  
1) Stanovení vztahu sousednosti (Neighbor Adjacencies) 
	- Každý router pošle Hello paket se svým Router-ID multicastovou IP adresou 224.0.0.5
	- Router-ID je identifikátor routeru v OSPF oblasti jako 32 bitové číslo
	- Příjme-li router Hello paket s neznámým Router-ID, pokusí se s ním navázat vztah sousednosti (Pokud dané Router-ID zná tak vztah pouze udržuje)
2) Výměna údajů o stavu spojů (Link-state Advertisements)  
3) Sestavení databáze stavu spojů (Link-state Database, LSDB)  
4) Spuštění algoritmu SPF  
5) Výběr nejlepších cest sítí

##### Možnost implementace OSPF  
- OSPF podporuje hierarchické směrování pomocí oblastí  
  - Oblast (area) je skupina routerů sdílejících údaje o stavech spojů  
  - Všechny routery v dané oblasti mají totožný oblast LSDB  
- OSPF lze implementovat dvěma způsoby:  
  - Single-area OSPF  
    - Všechny routery v jediné oblasti (zpravidla 0)  
  - Multi-area OSPF  
    - Routery v různých oblastech, které jsou hierarchicky uspořádané  
    - Všechny oblasti musí být propojeny s páteřní (backbone) oblastí 0

##### Multi-area OSPF  
- Menší objem směrovacích tabulek, síťové adresy v jednotlivých oblastech mohou být sumarizovány, což je třeba explicitně povolit  
- Nižší režie aktualizace stavu spojů rozdělením sítě do oblastí, což snižuje nároky na výkon a pameť routerů  
- Nižší frekvence spouštění SPF lokalizací dopadu změn topologie v rámci dané oblasti, kde se LSA flooding zastaví na hranicích oblastí

##### Point-to-Point spoj
- Nedochází k vobě BR a BDR
- Implicitní typ spoje pro sérivové linky, platí pouze na rozhraních typu Serial (Zde není potřeba tento druh spoje nastavovat příkazem)
- U spojů Ethernet je třeba nastavit tento spoj explicitně

##### OSPFv2  
- Popdora pouze IPv4  
- Pro zájemnou komunikaci routerů se používá IPv4  
##### OSPFv3  
- Podporuje IPv6 i IPv4 s použitím funkce Address Families  
- Pro zájemnou komunikaci routerů používá IPv6  
- Běží nezávisle na OSPFv2  
- Příkazy na konfiguraci jsou velmi podobné OSPFv2

##### Provozní stavy OSPF
- Down
	- Router odesílá Hello pakety na daném rozhraní
	- Router přijímá Hello paket od souseda
- Init
	- Router odesílá pakety s RID daného souseda
	- Router přijímá Hello Paket s vlastním RID
	- Pokud router příjme Hello paket od neznámého Router-ID přidá svůj Router-ID do seznamu sousedů a odešle jej
	- Pokud router příjme Hello paket obsahující jeho Router-ID v seznamu sousedů, přidá Router-ID souseda do datbáze a přejde do stavu Two-Way
- Two-way (v tomto stavu zůstavájí sousední routery, které nejsou DR ani BDR)
	- Routery si vzájemně vyměňují Hello pakety
	- Pokud jsou oba routery propojeny spojem Point-to-Point, přejdou do stavu ExStart
	- Pokud jsou oba routery propojeny Ethernet spojem, dojde k volbě DR a BDR:
		- Router, který má nejvyšší prioritu nebo Router-ID se stane DR
		- Router, který má druhou nejvyšší prioritu nebo Router-ID se stane BDR
- ExStart (pouze pro Point-to-Point sítě)
	- Routery si vzájemně vyměňují DBD pakety s příznaky
	- Dojde k dohodě, kdo první pošle DBD a s jakým sekvenčním číslem
- Exchange
	- Routery si vzájemně vyměňují DBD pakety s LSA
	- Dojde ke vzájemné výměně záznamů LSDB
	- Po stavu Two-Way routery přejdou do stavů synchronizace svých databází, který se skládá ze třech kroků:
		- Určení pořadí (Router s nejvyšším Router-ID pošlé své DBD první)
		- Výměna DBD paketů (příjemce odpoví LSAck)
		- Aktualizace LSDB (router porovná přijaté DBD se svou databází a v případě rozdílů přejde do stavu Loading a vyžádá si potřebné bloky LSA odesláním LSR paketu)
	- Poté, co byly všechny pakety LSR vyřízeny, se LSDB obou routerů nachází v konzistentním stavu (Pakety LSU jsou i nadále zasílány, avšak jen tehdy, když routery zjistí změny stavu spoje anebo uplynutí 30 minut)
- Loading (Pouze pokud je třeba získat podrobnosti o určitém spoji)
	- Routery si vyměňují LSR, LSU a LSAck pakety, SPF algoritmus určí cesty
	- Dojde k získání konzistentní podoby LSDB mezi oběma routery
- Full
	- LSDB je mezi routery plně synchronizována
	- Pokud nepříjde Hello paket c časovém limitu, přejde do stavu Down

##### Význam role Designated Router (DR)
- Multiaccess sítě přinášejí dvě výzvy: 
	- Existenci mnoha vztahů sousednosti
	- Negativní dopady LSA floodingu
- Pokud selže DR, router v roli BDR se stane novým DR a je zvolen nový router v roli BDR
##### Routery v roli DR a BDR
- Přijímají aktualizace stavu spojů od ostatních routerů
- Zasílají aktualizace stavu spojů ostatním routerům

##### Ostatní Routery (DROTHER)
- Zasílají aktualizace stavů spojů pouze routerů DR a BDR
- Přijímají aktualizace stavu spojů výhradně od DR nebo BDR


#### 3) OSPF pakety

##### Zprávy protokolu OSPF  
- Hello Packet (Hello)  
  - Informuje o přítomnosti daného routeru na síťovém segmentu  
- Database Description Packet (DBD)  
  - Shrnuje aktuální stav link-state databáze (LSDB)  
- Link-state Request Packet (LSR)  
  - Žádost o poskytnutí údajů o stavu daného spoje  
- Link-state update Packet (LSU)  
  - Předává údaje o stavu daného spoje  
- Link-state Acknowledgment Packet (LSAck)  
  - Potvrzení přijetí údajů o stavu daného spoje
##### Link-State Update (LSU) Paket
- Používá se také pro zasílání aktualizací stavu spojů, v tomto případě mu LSR paket nepředchází
- LSU může obsahovat až 11 různých druhů LSA (Link-State Advertisement) bloků

##### Hello Pakety
- OSPF Type 1 Paket, jeho příjem se nepotvrzuje
- Zajišťuje zjištění OSPF sousedů, předává parametry nutné pro vzájemnou spolupráci a pokud se neshodují, vztah nevznikne
- Volba routeru v roli DR (Designated Router) a BDR (Backup Designated Router), netýká se spojů Point-to-Point


#### 4) OSPF konfigurace

##### Režim konfigurace routeru pro OSPF
- Příkaz "router ospf {id procesu}", platí pouze v rámci daného routeru a je vhodné si zvolit stejné ID pro všechny routery v oblasti
- Router-ID lze nastavit explicitně příkazem "router-id {id}" nebo se nastavuje automaticky:
	- Dle nejvyšší IP adresy loopback rozhraní
	- Dle nejvyšší IP adresy aktivního rozhraní
- Ověřit Router-ID lze příkazem "show ip protocols"
- Router-ID lze měnit kdykoliv, změna se však projeví až po resetu OSPF procesu na daném routeru příkazem "celar ip ospf process"
##### Konfigurace sítě Point-to-Point a Multi-Access
- Dva základní způsoby přiřazení rozhraní routeru k oblasti:
	- Příkaz "network {subnet-ip} {wildcard-mask} area {area}"
		- V režimu konfigurace OSPF procesu
		- IP adresa sítě s wildcard maskou určuje rozhraní (lze sumarizovat)
		- Lze zadat přímo rozhraní bez s wildcard maskou 0.0.0.0 což je nejjednodušší způsob konfigurace
	- Příkaz "ip ospf {process-id} area {area-id}"
		- Zadáván v režimu konfigurace jednotlivých rozhraní
		- Musí být zadán pro každé rozhraní, které je součástí nějaké oblasti
- Pasivní rozhraní:
	- Rozhraní, které nekomunikuje s dalšími OSPF routery, např. rozhraní koncových sítí (stub networks) nebo spoje routery cizích
	- Pasivní rozhraní zabraňuje hledání sousedních OSPF routerů
	- Nasazením pasivního rozhraní se omezí zátěž sítě a sníží se bezpečnostní rizika vyplývající z nasazení OSPF
	- Příkaz "passive-interface {interface}" v režimu konfigurace OSPF procesu
	- Ověřit lze příkazem "show ip protocols"
- Příkaz "ip sopf network point-to-point" v režimu konfigurace rozhraní
- Příkaz "show ip ospf interface {interface}" pro zobrazení podrobností o daném rozhraní
- Příkaz "show ip ospf neighbor" zobrazí stavy a role sousedních routerů včetně připojených rozhraní
	- FULL/DROTHER (místní DR/BDR router sousedí s DROTHER)
	- FULL/DR (místní BDR/DROTHER router sousedí s DR)
	- FULL/BDR (místní DR/DROTHER router sousedí s BDR)
	- 2-WAY/DROTHER (místní DROTHER sousedí s DROTHER)
- Příkaz "ip ospf priority" v konfiguračním režimu pro nastavení OSPF priority
- Příkaz "auto-cost reference-bandwidth {rychlost v Mbit/s}" v konfiguračním režimu pro nastavení referenční rychlosti ceny nebo příkaz "ip ospf cost {cena}"
- Příkaz "ip ospf hello-interval {s}" v konfiguračním režimu pro nastavení Hello intervalu (výchozí hodnoty jsou optimálni)
- Příkaz "ip ospf-dead-interval" v konfiguračním režimu pro nastavení Dead intervalu (výchozí hodnoty jsou optimálni)
- Příkaz "default-information originate" v konfiguračním režimu pro autoamtický přenos výchozí cecsty v rámci OSPF

##### Konfigurace sítě Multi-Access
### Kvízy  
[HS (I4.D) – 1.1. Vlastnosti a možnosti využití OSPF]([https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQVFNODVXNzYzRjFOQ0dJSEYzNTFEMFRCNi4u&route=shorturl)](https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQVFNODVXNzYzRjFOQ0dJSEYzNTFEMFRCNi4u&route=shorturl\) "https://forms.office.com/pages/responsepage.aspx?id=iw_r_ignr0ifnafpxpzo2vxvcnwt1thbn0p9mknr0-puqvfnodvxnzyzrjfoq0djseyzntfemfrcni4u&route=shorturl)")
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUM01UM0dWOTdWRFFLOEgwMkkyVVkzQks5QS4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUNjRMUEJDQVhEVkZFOFRVMFo0UkFRRlc1Ni4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUMUFMUzJTUENVMUtBUk5QNVM5Mko5M0lYRi4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUOFlSNURYUzE3MDVBVUw4QTNSVDdNUTRETC4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUQlJaMzYwRzNRSkVCWDNGQ00zVjYxQ0JVSy4u&route=shorturl