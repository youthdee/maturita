#### 1) Účel, funkce síťové vrstvy
##### Účel síťové vrstvy
1) **Umožňuje výměnu dat mezi uzly různých sítí**:
	- Oproti L2 nejen v místní síti, ale i mezi sítěmi
2) **Třetí vrstva modelu** `ISO/OSI` (`L3`):
	- Poskytuje služby transportní vrstvě (L4)
3) **Datovou jednotkou  je paket**
	- Zapouzdřuje datové jednotky vrstvy L4
4) **Doručení paketů není garantováno**
	- Běžně ji zajišťují protokoly na transportní vrstvě
##### Funkce síťové vrstvy
1) **Adresace koncových uzlů v příslušné síti**:
	- Každý uzel disponuje jedinečnou adresou
2) **Zapouzdření datových jednotek vrstvy L4**:
	- Doplní se adresy odesílatele a příjemce
3) **Předání paketu spojové vrstvě k odeslání**:
	- Spojová vrstva zajišťuje doručení v místní síti
4) **Směrování paketů mezi sítěmi**:
	- Zajišťováno routery (směrovači)
#### 2) Protokoly síťové vrstvy a jejich datové jednotky
##### Internet Protocol verze 4 (IPv4)
- Stávající protokol Internetu
- Adresy o délce **32 bitů**
##### Internet Protocol verze 6 (IPv6)
- Síťový protokol nové generace
- Adresy o délce **128 bitů**
##### Vlastnosti protokolu IP
1) **Bezestavový protokol**:
	- Před odesláním zprávy není vytvářeno spojení
2) **Bez záruky doručení** (`Best Effort`):
	- Všechny pakety nemusí dorazit do cíle
3) **Nezávislý na médiu**:
	- Místní sítě mohou být řešeny různým způsobem
##### ICMP (Internet Control Message Protocol)
- **Poskytuje zpětnou vazbu o problémech v síti**:
	- Nesnaží se  o zajištění spolehlivosti IP
- **Zprávy nemusí být zpracovány povinně**:
	- Často nejsou povoleny kvůli bezpečnosti sítě
- Dostupný jak pro `IPv4` tak pro `IPv6`
	- Funkce ICMPv6 nabízí některé funkce navíc
- Funkce společné pro `IPv4` a `IPv6`:
	1) `Echo request`/`Reply`
	2) `Destination`/`Service Unavailable`
	3) Time (`TTL`) exceeded
	4) `Route redirection`
1) **ICMP Destination Unreachable**:
	- Zasílán, pokud přijatý paket nelze doručit (odesílá přijímající hostitel, typicky router)
	- Oznamuje hostiteli, že cíl není dostupný, podrobnosti určuje kód zprávy:
		1) `Net unreachable` (0)
		2) `Host unreachable` (1)
		3) `Protocol unreachable` (2)
		4) `Port unreachable` (3)
2) **ICMP Time Exceeded**:
	- Zasílá router, pokud paket nelze předat (doba životnosti TTL klesne na nulu)
	- Při průchodu paketu se pole TTL sníží o 1 (při dosažení nuly se paket zahodí a zašle se zpráva)
	- ICMPv6 také nabízí tuto zprávu (TTL ~ Hop Limit)
	- Lze využít příkazem "traceroute"
##### Struktura IPv4 Paketu (Záhlaví)
1) Verze
2) Délka záhlaví
3) QoS
4) Celková délka
5) Idetifikace
6) Fragmentace
7) TTL
8) Protokol
	- `ICMP`, `TCP`, `UDP`
9) Kontrolní součet
10) Zdrojová adresa
11) Cílová adresa
##### Struktura IPv6 Paketu (Záhlaví)
1) Verze
2) Třída provozu
3) Flow Label
4) Délka obsahu
5) Další záhlaví
6) TTL
7) Zdrojová adresa
8) Cílová adresa
##### RIP (Routing Information Protocol)
- Jednoduchý směrovací protokol využívající směrování podle vzdálenosti
##### NDP (Neighbor Discovery Protocol)
- IPv6 náhrada ARP
- Zajišťuje zjišťování sousedů a měrovačů
#### 3) Princip paketového přenosu dat
##### Princip 
1) Data jsou **rozdělena do menších částí** (paketů), které jsou **nezávisle přenášeny** sítí
2) Každý paket **obsahuje header** (hlavičku) s informacemi o **zdrojové** a **cílové IP adrese** a **datovou část** (payload) obsahující přenášenou zprávu
3) Paketový přenos umožňuje **efektivnější využití** sítě než přepojování okruhů
	- Protože různé pakety můžou jít různými cestami
4) Zajišťuje **směrování** (routing) paketů **mezi sítěmi**
5) IP směrovače (routery) analyzují hlavičky paketů a **rozhodují o jejich cestě** v síti
6) Pokud paket putuje přes více sítí, může **být fragmentován a znovu sestaven**
