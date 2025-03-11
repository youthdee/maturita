#### 1) Účel, funkce síťové vrstvy
##### Účel síťové vrstvy
- Umožňuje výměnu dat mezi uzly různých sítí
	- Oproti L2 nejen v místní síti, ale i mezi sítěmi
- Třetí vrstva modelu ISO/OSI (L3)
	- Poskytuje služby transportní vrstvě (L4)
- Datovou jednotkou (PDU) je paket
	- Zapouzdřuje datové jednotky vrstvy L4
- Doručení paketů není garantováno
	- Běžně ji zajišťují protokoly na transportní vrstvě

##### Funkce síťové vrstvy
- Adresace koncových uzlů v příslušné síti
	- Každý uzel disponuje jedinečnou adresou
- Zapouzdření datových jednotek vrstvy L4
	- Doplní se adresy odesílatele a příjemce
- Předání paketu spojové vrstvě k odeslání
	- Spojová vrstva zajišťuje doručení v místní síti
- Směrování paketů mezi sítěmi
	- Zajišťováno routery (směrovači)
#### 2) Protokoly síťové vrstvy a jejich datové jednotky
##### Internet Protocol verze 4 (IPv4)
- Stávající protokol Internetu
- Adresy o délce 32 bitů
##### Internet Protocol verze 6 (IPv6)
- Síťový protokol nové generace
- Adresy o délce 128 bitů
##### Vlastnosti protokolu IP
- Bezestavový protokol
	- Před odesláním zprávy není vytvářeno spojení
- Bez záruky doručení (Best Effort)
	- Všechny pakety nemusí dorazit do cíle
- Nezávislý na médiu
	- Místní sítě mohou být řešeny různým způsobem
##### ICMP (Internet Control Message Protocol)
- Poskytuje zpětnou vazbu o problémech v síti
	- Nesnaží se  o zajištění spolehlivosti IP
- Zprávy nemusí být zpracovány povinně
	- Často nejsou povoleny kvůli bezpečnosti sítě
- Dostupný jak pro IPv4 tak pro IPv6
	- Funkce ICMPv6 nabízí některé funkce navíc
- Funkce společné pro IPv4 a IPv6:
	- Echo request/Repoly
	- Destination/Service Unavailable
	- Time (TTL) exceeded
	- Route redirection
- ICMP Destination Unreachable:
	- Zasílán, pokud přijatý paket nelze doručit (odesílá přijímající hostitel, typicky router)
	- Oznamuje hostiteli, že cíl není dostupný, podrobnosti určuje kód zprávy:
		- Net unreachable (0)
		- Host unreachable (1)
		- Protocol unreachable (2)
		- Port unreachable (3)
- ICMP Time Exceeded:
	- Zasílá router, pokud paket nelze předat (doba životnosti TTL klesne na nulu)
	- Při průchodu paketu se pole TTL sníží o 1 (při dosažení nuly se paket zahodí a zašle se zpráva)
	- ICMPv6 také nabízí tuto zprávu (TTL ~ Hop Limit)
	- Lze využít příkazem "traceroute"

##### Struktura IPv4 Paketu (Záhlaví)
- Verze
- Délka záhlaví
- QoS
- Celková délka
- Idetifikace
- Fragmentace
- TTL
- Protokol
	- ICMP, TCP, UDP
- Kontrolní součet
- Zdrojová adresa
- Cílová adresa
##### Struktura IPv6 Paketu (Záhlaví)
- Verze
- Třída provozu
- Flow Label
- Délka obsahu
- Další záhlaví
- TTL
- Zdrojová adresa
- Cílová adresa

##### RIP (Routing Information Protocol)
- Jednoduchž směrovací protokol využívající směrování podle vzdálenosti
##### NDP (Neighbor Discovery Protocol)
- IPv6 náhrada ARP
- Zajišťuje zjišťování sousedů a měrovačů
#### 3) Princip paketového přenosu dat

##### Princip 
- Data jsou rozdělena do menších částí (paketů), které jsou nezávisle přenášeny sítí
- Každý paket obsahuje header (hlavičku) s informacemi o zdrojové a cílové IP adrese a datovou část (payload) obsahující přenášenou zprávu
- Paketový přenos umožňuje efektivnější využití sítě než přepojování okruhů, protože různé pakety můžou jít různými cestami
- Zajišťuje směrování (routing) paketů mezi sítěmi
- IP směrovače (routery) analyzují hlavičky paketů a rozhodují o jejich cestě v síti
- Pokud paket putuje přes více sítí, může výt fragmentován a znovu sestaven
