#### 1) Charakteristika Ethernetu, rámec Ethernetu

##### Charakteristika Ethernetu
- Standardizován jako IEEE 802.3
- Podporuje různá fyzická média (Souosý kabel, kroucená dvojlinka, optické vlákno)
##### Ethernet na souosém kabelu
- Souosý kabel je sdíleným médiem:
	- Fyzická topologie je sběrnice (bus)
	- Charakter komunikace je half-duplex
- Kabel musí být správně zakončen terminátory (jinak by docházelo ke zpětnému odrazu signálů)
- Výhodou je absence dalších aktivních síťových prvků (pouze síťové adaptéry a kabel s terminátory)
- Nevýhodou je obtížná diagnostika poruch (problém může být po celé délce sdíleného kabelu)

##### Thick Ethernet
- Přenosová rychlost 10 Mb/s
- Médiem je souosý kabel o průměru 9,5mm
- Segment o délce až 500 metrů a až 100 uzlů
##### Ethernet na kroucené dvoulince
- Kroucená dvoulinka je vyhrazeným médiem:
	- Fyzickou topologií je hvězda
	- Charakter komunikace je full-duplex
- Výhodou je levná a dostupná kabeláž
- Nevýhodou je nutnost použití aktivních prvků (propojení více stanic vyžaduje switch)
##### Thin Ethernet
- Přenosová rychlost 10 Mb/s
- Médiem je souosý kabel o průměru 6mm
- Segment o délce až 185 metrů a až 30 uzlů
##### Rámec Ethernetu
- Druhy rámců:
	- Ethernet II
		- Nejčastejiší a dnes užívaný (s polem EtherType)
		- Výhodou je payload o délce až 1500 oktetů
	- Novell Raw
		- Nestandardní, dříve využívaný s protokolem IPX
	- IEE 802.2 Logical Link Control (LLC)
		- Používán pouze ve spojení s protokoly ISO/OSI
	- IEE 802.2 Subnetwork Access Protocol
		- Používán s protokoly TCP/IP
		- Kvůli výhodám Ethernet II se prakticky nevyužívá
	- Délky rámců:
		- Běžná rámec:
			- Délka 64 až 1518 oktetů (1522 pro VLAN tagging)
		- Runt rámec
			- Méně než 64 oktetů
			- Neplatný rámec, odstraňuje se
		- Jumbo rámec
			- Více jež 1518 (1522 pro VLAN tagging)
			- Nestandardní délka rámce (typicky až 9 KB)
			- Podporován pouze některými síťovými prvky
- Rámec IEEE 802.3 LLC/SNAP
	- Od začátku používán současně s ostatními typy rámců
	- Destination Address (6B)
	- Source Address (6B)
	- Length (2B)
	- Packet (64-1500B)
- Rámec Ethernet II
	- Doplněn do standardu až v roce 1997
	- MAC Header (14B):
		- Destination MAC address
		- Source MAC address
		- EtherType
	- Data (46 - 1500B)
	- CRC Checksum (4B)
- Možný souběžný provoz všech typů rámců
#### 2) MAC adresy – formát, druhy

##### Mac Adresa - Charakteristika
- Fyzická adresa protokolů spojové vrstvy
- Délka adresy 48 bitů
- Přiřazena zařízení během výroby
- Určena k použití na místním sdíleném médiu (Mimo místní síť nemá význam)
- Není hierarchická (nelze dle ní směrovat)
- Zapisována jako skupina bajtů
- Rozdělena na dvě části:
	- Část OUI (24 bitů) je přidělována organizací IEEE
	- Část EUI-48 (24 bitů) je přidělována výrobcem
- Umístěna v záhlaví rámce Ethernet (Cílová a zdrojová adresa)

##### Formáty MAC adresy
- Délka 48 bitů (6 bajtů)
- Nejčastěji zapisována hexadecimálně, rozděleno do skupin
- Lze zapsat:
	- Dvojtečky: `00:1A:2B:3C:4D:5E`
	- Pomlčky: `00-1A-2B-3C-4D-5E`
	- Bez oddělovačů: `001A2B3C4D5E`
	- Cisco styl (čtveřice): `001A.2B3C.4D5E`

##### Druhy MAC adresy
- Rozlišení typu v bitech prvního oktetu (b1)
	- Universally Administered Addresses (b1 = 0)
	- Locally Administered Adresses (b1 = 1)
- Rozlišení typu v bitech prvního oktetu (b0)
	- Unicast (b0 = 0)
	- Multicast (b0 = 1)
- Adresy spojové a síťové vrstvy korespondují
- Unicast:
	- Příklad IPv4 adresy (192.168.1.200)
	- Příklad MAC adresy (00:11:22:33:44:55)
- Broadcast:
	- Příklad IPv4 adresy (192.168.1.255)
	- Příklad MAC adresy (FF:FF:FF:FF:FF:FF)
- Multicast:
	- Příklad IPv4 adresy (224.0.0.200)
	- Příklad MAC adresy (01:00:5E:00:00:C8)
#### 3) ARP

##### Charakteristika protokolu ARP
- Zjišťuje MAC adresu zařízení v LAN pokud zná IP adresu tohoto zařízení
- Pro cílový uzel v LAN překládá IP adresu na MAC adresu
- Údaje o přeložených adresách se zapisují do ARP tabulky, kterou spravuje a která je uložena v RAM zprostředkujícího zařízení
- Záznam typu IP adresa cíle a jeho MAC adresa
- Princip fungování:
	- Před zapouzdřením odesílaného rámce se prohledá ARP tabulka, zda-li tam není záznam shodný s cílovou IPv4 adresou v paketu a k ní patřící MAC adresa
	- Pokud odesílatel takový záznam v ARP tabulce má, tak použije odpovídající MAC adresu jako cílovou MAC adresu v odesílaném rámci
	- Pokud tam potřebný záznam není, musí ARP protokol zajistit jeho doplnění do ARP tabulky
##### Struktura rámců protokolu ARP
- ARP požadavek: (Request)
	- Destination je Broadcast
	- Opcode je 1
	- Target MAC není
	- Switchem zreplikován na všechny porty kromě příchozího
	- Všechny uzly v LAN jsou povinny tento broadcast příjmout a předat ho ke zpracování ARP protokolu
- ARP odpověď: (Reply)
	- Destination je Unicast
	- Opcode je 2
	- Target MAC je tazatel
	- Dozující si povinně přidá záznam do ARP tabulky
	- Pokud žádné zařízení neodpoví na ARP request, tak je paket zahozen
##### ARP Tabulka
- Záznamy nejsou loženy trvale
- Hodnota délky uložení lze nastavit (standardně na koncových uzlech 1 minuta, na Cisco routerech až 4 hodiny)
- Lze vkládat statické záznamy nebo záznamy manuálně smazat


#### 4) Switch – základní principy, metody předávání rámců
##### Základní principy přepínání (switch)
- Pracuje na spojové vrstvě L2
	- Nezohledňuje datový obsah přenášených rámců
- Přijímá rámce a předává je na vhodné porty
	- Vyhodnocuje pole zdrojové a cílové MAC adresy
- Učí se příslušnosti zařízení k portům
	- MAC adresy a čísla portů ukládá do MAC tabulky
- Princip činnosti:
	- Po zapnutí switche je MAC tabulka prázdna
##### Princip činnosti switche (přepínače)
- Po zapnutí switche (přepínače) je MAC tabulka prázdná, switch (přepínač) určitou dobu pracuje jako hub
- Záznamy tabulky se tvoří dle přijatých rámců, uloží se MAC adresa odesílatele a číslo portu
- Rámce se následně rozesílají dle MAC tabulky, podle cílové MAC adresy se vyhledá číslo portu
- Záznamy tabulky po určité době expirují, při odpojení portu se položky tabulky vymažou

##### Metoda Store-and-Forward
- Switch (přepínač) nejprve příjme celý rámec, ověří délku a kontrolní součet (nevyhovující rámec vyřadí)
- Switch (přepínač) zaznamená číslo portu odesílatele pokud v tabulce MAC adres příslušný záznam není
- Switch (přepínač) odešle rámec na příslušný port pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
- Úplné přijetí rámce před odesláním (vyšší zpoždění), umožňuje vyloučit vadné rámce

##### Metoda Cut-through
- Switch (přepínač) přijme alespoň cílovou MAC adresu rámce, zahájí jeho zpracování, příjem rámce pokračuje
- Switch (přepínač) zahájí odeslání rámce na port pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
- Switch (přepínač) zaznamená číslo portu odesílatele, nejdříve však po přijetí zdrojové MAC adresy rámce a pokud v tabulce MAC adres příslušný záznam není
- Varianty Metody Cut-Trough:
	- Fast-forward
		- Zahájí odesílání rámce ihned po přijetí cílové MAC
		- Nejmenší přenosové zpoždění
		- Typická varianta
	- Fragment-free
		- Zahájí odesílání rámce po přijetí 64 oktetů
		- Nejvíce kolizí nastává právě v této části rámce
		- Kompromis mezi mírou integrity a zpoždění
- Rámec odesílán ihned po přijetí záhlaví (menší zpoždění), vadné rámce se tak předávají dále po síti

