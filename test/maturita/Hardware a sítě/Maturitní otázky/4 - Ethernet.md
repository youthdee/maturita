#### 1) Charakteristika Ethernetu, rámec Ethernetu
##### Charakteristika Ethernetu
- Standardizován jako `IEEE 802.3`
- Podporuje **různá fyzická média**:
	- Souosý kabel, kroucená dvojlinka, optické vlákno
##### Ethernet na souosém kabelu
- Souosý kabel je **sdíleným médiem**:
	- Fyzická topologie je sběrnice (bus)
	- Charakter komunikace je half-duplex
- Kabel musí být správně zakončen terminátory (jinak by docházelo ke zpětnému odrazu signálů)
- Výhodou je absence dalších aktivních síťových prvků (pouze síťové adaptéry a kabel s terminátory)
- Nevýhodou je obtížná diagnostika poruch (problém může být po celé délce sdíleného kabelu)
##### Thick Ethernet
- Přenosová rychlost `10 Mb/s`
- Médiem je **souosý kabel** o průměru 9,5mm
- Segment o délce až **500 metrů** a až **100 uzlů**
##### Ethernet na kroucené dvoulince
- Kroucená dvoulinka je **vyhrazeným médiem**:
	- Fyzickou topologií je hvězda
	- Charakter komunikace je full-duplex
- Výhodou je **levná** a **dostupná** kabeláž
- Nevýhodou je nutnost použití **aktivních prvků**
##### Thin Ethernet
- Přenosová rychlost `10 Mb/s`
- Médiem je **souosý kabel** o průměru 6mm
- Segment o délce až **185 metrů** a až **30 uzlů**
##### Rámec Ethernetu
- Druhy rámců:
	1) `Ethernet II`
		- Nejčastejiší a dnes užívaný (s polem EtherType)
		- Výhodou je payload o délce až 1500 oktetů
		- Doplněn do standardu až v roce 1997
		- MAC Header (14B):
		- Destination MAC address
		- Source MAC address
		- EtherType
		- Data (46 - 1500B)
		- CRC Checksum (4B)
	2) `Novell Raw`
		- Nestandardní, dříve využívaný s protokolem IPX
	3) `IEE 802.2` **Logical Link Control** (`LLC`)
		- Používán pouze ve spojení s protokoly ISO/OSI
	4) `IEE 802.2` **Subnetwork Access Protoco**l
		- Používán s protokoly TCP/IP
		- Kvůli výhodám Ethernet II se prakticky nevyužívá
	5) `IEEE 802.3` `LLC`/`SNAP`
		- Od začátku používán současně s ostatními typy rámců
		- Destination Address (6B)
		- Source Address (6B)
		- Length (2B)
		- Packet (64-1500B)
	- **Délky rámců**:
		1) **Běžný rámec**:
			- Délka 64 až 1518 oktetů (1522 pro VLAN tagging)
		2) **Runt rámec**:
			- Méně než 64 oktetů
			- Neplatný rámec, odstraňuje se
		3) **Jumbo rámec**:
			- Více jež 1518 (1522 pro VLAN tagging)
			- Nestandardní délka rámce (typicky až 9 KB)
			- Podporován pouze některými síťovými prvky
#### 2) MAC adresy – formát, druhy
##### Mac Adresa - Charakteristika
- **Fyzická adresa** protokolů spojové vrstvy
- Délka adresy **48 bitů**
- Přiřazena zařízení **během výroby**
- Určena k použití na **místním sdíleném médiu** (Mimo místní síť nemá význam)
- **Není hierarchická** (nelze dle ní směrovat)
- Zapisována jako **skupina bajtů**
- Rozdělena na dvě části:
	1) `OUI` (24 bitů):
		- Přidělována organizací IEEE
	2) `EUI-48` (24 bitů):
		- Přidělována výrobcem
- Umístěna v **záhlaví rámce Ethernet** (Cílová a zdrojová adresa)
##### Formáty MAC adresy
- Délka **48 bitů** (6 bajtů)
- Nejčastěji zapisována **hexadecimálně**, rozděleno do skupin
- Lze zapsat:
	1) Dvojtečky: 
		- `00:1A:2B:3C:4D:5E`
	2) Pomlčky:
		- `00-1A-2B-3C-4D-5E`
	3) Bez oddělovačů:
		- `001A2B3C4D5E`
	4) Cisco styl (čtveřice):
		- `001A.2B3C.4D5E`
##### Druhy MAC adresy
1) **Rozlišení typu v bitech prvního oktetu** (b1)
	1) Universally Administered Addresses:
		- `b1 = 0`
	2) Locally Administered Adresses:
		- `b1 = 1`
2) **Rozlišení typu v bitech prvního oktetu** (b0)
	1) Unicast:
		- `b0 = 0`
	2) Multicast:
		- `b0 = 1`
3) **Adresy spojové a síťové vrstvy korespondují**
	1) `Unicast`:
		- Příklad IPv4 adresy:
			- `192.168.1.200`
		- Příklad MAC adresy:
			- `00:11:22:33:44:55`
	2) `Broadcast`:
		- Příklad IPv4 adresy:
			- `192.168.1.255`
		- Příklad MAC adresy:
			- `FF:FF:FF:FF:FF:FF`
	3) `Multicast`:
		- Příklad IPv4 adresy:
			- `224.0.0.200`
		- Příklad MAC adresy:
			- `01:00:5E:00:00:C8`
#### 3) ARP
##### Charakteristika protokolu ARP
- Zjišťuje **MAC adresu** zařízení v LAN pokud zná **IP adresu** tohoto zařízení
- Pro cílový uzel v LAN překládá **IP adresu na MAC adresu**
- Údaje o přeložených adresách se zapisují do **ARP tabulky**, kterou spravuje a která je uložena v **RAM zprostředkujícího zařízení**
- **Princip fungování**:
	1) Před zapouzdřením odesílaného rámce se prohledá ARP tabulka, zda-li tam není záznam shodný s cílovou IPv4 adresou v paketu a k ní patřící MAC adresa
	2) Pokud odesílatel takový záznam v ARP tabulce má, tak použije odpovídající MAC adresu jako cílovou MAC adresu v odesílaném rámci
	3) Pokud tam potřebný záznam není, musí ARP protokol zajistit jeho doplnění do ARP tabulky
##### Struktura rámců protokolu ARP
1) **ARP požadavek**: (`Request`)
	- Destination:
		- `Broadcast`
	- Opcode:
		- `1`
	- Target MAC **není**
	- Switchem zreplikován na všechny porty kromě příchozího
	- Všechny uzly v LAN jsou povinny tento broadcast příjmout a předat ho ke zpracování ARP protokolu
2) **ARP odpověď**: (`Reply`)
	- Destination:
		- `Unicast`
	- Opcode:
		- `2`
	- Target MAC je **tazatel**
	- Dozující si povinně přidá záznam do ARP tabulky
	- Pokud žádné zařízení neodpoví na ARP request, tak je paket zahozen
##### ARP Tabulka
- Záznamy **nejsou uloženy trvale**
- Hodnota délky uložení lze nastavit (standardně na koncových uzlech 1 minuta, na Cisco routerech až 4 hodiny)
- Lze vkládat **statické záznamy** nebo záznamy manuálně smazat
#### 4) Switch – základní principy, metody předávání rámců
##### Základní principy přepínání (switch)
1) **Pracuje na spojové vrstvě L2**:
	- Nezohledňuje datový obsah přenášených rámců
2) **Přijímá rámce a předává je na vhodné porty**:
	- Vyhodnocuje pole zdrojové a cílové MAC adresy
	- Následně rozesílá na vhodné porty dle MAC tabulky
3) **Učí se příslušnosti zařízení k portům**:
	- MAC adresy a čísla portů ukládá do MAC tabulky
	- Záznamy jsou dočasné
4) **Princip činnosti**:
	- Po zapnutí switche je MAC tabulka prázdna, určitou dobu pracuje jako hub
##### Metoda Store-and-Forward
1) Nejprve příjme **celý rámec**, **ověří délku** a **kontrolní součet**
2) **Zaznamená** číslo portu odesílatele pokud v tabulce MAC adres příslušný záznam není
3) **Odešle rámec na příslušný port** pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (**flood**)
4) Úplné přijetí rámce před odesláním (**vyšší zpoždění**), umožňuje **vyloučit vadné rámce**
##### Metoda Cut-through
1) **Přijme alespoň cílovou MAC adresu** rámce, zahájí jeho zpracování, příjem rámce pokračuje
2) **Zahájí odeslání rámce na port** pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
3) **Zaznamená číslo portu odesílatele**, nejdříve však po přijetí zdrojové MAC adresy rámce a pokud v tabulce MAC adres příslušný záznam není
- **Varianty** Metody Cut-Trough:
	1) **Fast-forward**
		- Zahájí odesílání rámce ihned po přijetí cílové MAC
		- Nejmenší přenosové zpoždění
		- Typická varianta
	2) **Fragment-free**
		- Zahájí odesílání rámce po přijetí 64 oktetů
		- Nejvíce kolizí nastává právě v této části rámce
		- Kompromis mezi mírou integrity a zpoždění
- Rámec odesílán **ihned po přijetí záhlaví** (**menší zpoždění**), **vadné rámce se tak předávají dále** po síti

