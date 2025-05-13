#### 1) Účel, funkce síťové vrstvy
##### Účel síťové vrstvy
1. **Umožňuje výměnu dat mezi uzly různých sítí**:
    - Oproti L2 nejen v místní síti, ale i mezi sítěmi
    - Překonává hranice jednotlivých LAN sítí
    - Umožňuje komunikaci v rámci rozsáhlých WAN sítí
2. **Třetí vrstva modelu** `ISO/OSI` (`L3`):
    - Poskytuje služby transportní vrstvě (L4)
    - Využívá služeb spojové vrstvy (L2)
    - Klíčová pro funkci internetu a propojených sítí
3. **Datovou jednotkou je paket**
    - Zapouzdřuje datové jednotky vrstvy L4 (segmenty/datagramy)
    - Obsahuje hlavičku s řídícími informacemi a datovou část
    - Maximální velikost paketu je definována MTU (Maximum Transmission Unit)
4. **Doručení paketů není garantováno**
    - Běžně ji zajišťují protokoly na transportní vrstvě
    - Pracuje na principu best-effort delivery
    - Ztracené pakety musí řešit vyšší vrstvy (pokud je to vyžadováno)
##### Funkce síťové vrstvy
1. **Adresace koncových uzlů v příslušné síti**:
    - Každý uzel disponuje jedinečnou adresou
    - Využívá globálně jedinečné adresy (např. IPv4, IPv6)
    - Umožňuje identifikaci zařízení bez ohledu na jeho fyzickou lokaci
2. **Zapouzdření datových jednotek vrstvy L4**:
    - Doplní se adresy odesílatele a příjemce
    - Přidávají se další řídící informace (TTL, QoS, fragmentace)
    - Vytváří se hlavička síťového protokolu (např. IP hlavička)
3. **Předání paketu spojové vrstvě k odeslání**:
    - Spojová vrstva zajišťuje doručení v místní síti
    - Provádí se mapování síťových adres na linkové adresy (ARP)
    - Rozdělení velkých paketů na menší části (fragmentace) pokud je nutné
4. **Směrování paketů mezi sítěmi**:
    - Zajišťováno routery (směrovači)
    - Určování optimální cesty k cíli pomocí směrovacích protokolů
    - Podporuje statické i dynamické směrování (RIP, OSPF, BGP)
5. **Kontrola zahlcení a řízení toku dat**:
    - Prevence přehlcení sítě při vysokém provozu
    - Prioritizace paketů podle typu služby (QoS)
    - Omezení šíření vysílání (broadcast) mezi sítěmi
6. **Překlad adres a tunelování**:
    - NAT (Network Address Translation) pro sdílení veřejných IP adres
    - VPN tunely pro bezpečnou komunikaci přes veřejné sítě
    - Řešení kompatibility mezi IPv4 a IPv6 sítěmi
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
		    - Informuje o tom, že cílová síť není dostupná, typicky z důvodu chybějící směrovací cesty nebo výpadku sítě.
		2) `Host unreachable` (1)
		    - Informuje o tom, že cílový hostitel v síti není dostupný, přestože síť samotná je dosažitelná.
		3) `Protocol unreachable` (2)
		    - Informuje o tom, že cílový hostitel nepodporuje požadovaný protokol uvedený v IP datagramu.
		4) `Port unreachable` (3)
		    - Informuje o tom, že cílový port na hostiteli není dostupný nebo na něm neběží žádná služba, která by mohla požadavek zpracovat.
2) **ICMP Time Exceeded**:
	- Zasílá router, pokud paket nelze předat (doba životnosti TTL klesne na nulu)
	- Při průchodu paketu se pole TTL sníží o 1 (při dosažení nuly se paket zahodí a zašle se zpráva)
	- ICMPv6 také nabízí tuto zprávu (TTL ~ Hop Limit)
	- Lze využít příkazem "traceroute"
##### Struktura IPv4 Paketu (Záhlaví)
1. **Verze** (4 bity)
    - Identifikuje verzi IP protokolu, pro IPv4 hodnota 4
2. **Délka záhlaví** (4 bity)
    - Udává délku záhlaví ve 32-bitových slovech (obvykle 5, což odpovídá 20 bajtům)
    - Rozsah 5-15 slov (20-60 bajtů) včetně volitelných položek
3. **QoS** (8 bitů) / **Typ služby** (ToS)
    - Určuje prioritu a způsob zpracování paketu
    - Obsahuje hodnoty pro zpoždění, propustnost, spolehlivost
    - Novější implementace používají DSCP (Differentiated Services Code Point)
4. **Celková délka** (16 bitů)
    - Celková délka paketu v bajtech (záhlaví + data)
    - Maximální velikost 65535 bajtů
5. **Identifikace** (16 bitů)
    - Jednoznačný identifikátor datagramu
    - Používá se při fragmentaci k označení fragmentů patřících ke stejnému datagramu
6. **Fragmentace** (16 bitů)
    - Obsahuje příznaky fragmentace a offset fragmentu
    - Příznaky: DF (Don't Fragment), MF (More Fragments)
    - Offset: pozice fragmentu v původním datagramu
7. **TTL** (8 bitů) / **Time To Live**
    - Maximální počet směrovačů, kterými může paket projít
    - Zabraňuje nekonečnému bloudění paketů v síti
    - Každý směrovač hodnotu sníží o 1, při dosažení 0 je paket zahozen
8. **Protokol** (8 bitů)
    - Identifikuje protokol vyšší vrstvy zapouzdřený v datové části
    - Běžné hodnoty: `ICMP` (1), `TCP` (6), `UDP` (17)
9. **Kontrolní součet** (16 bitů)
    - Kontroluje integritu záhlaví (ne dat)
    - Přepočítává se na každém směrovači kvůli změně TTL
10. **Zdrojová adresa** (32 bitů)
    - IP adresa odesílatele paketu
11. **Cílová adresa** (32 bitů)
    - IP adresa příjemce paketu
12. **Volitelné položky** (proměnlivá délka)
    - Nepovinné rozšíření záhlaví pro speciální účely
    - Může obsahovat časová razítka, bezpečnostní informace, směrovací pokyny
##### Struktura IPv6 Paketu (Záhlaví)
1. **Verze** (4 bity)
    - Identifikuje verzi IP protokolu, pro IPv6 hodnota 6
2. **Třída provozu** (8 bitů)
    - Ekvivalent QoS/ToS v IPv4
    - Určuje prioritu paketu a typ služby
3. **Flow Label** (20 bitů)
    - Označuje sekvenci paketů patřících ke stejnému datovému toku
    - Umožňuje speciální zpracování určitých datových toků
4. **Délka obsahu** (16 bitů)
    - Délka dat následujících za základním záhlavím v bajtech
    - Nezahrnuje délku základního záhlaví (40 bajtů)
5. **Další záhlaví** (8 bitů)
    - Identifikuje typ následujícího záhlaví (rozšiřující záhlaví nebo protokol vyšší vrstvy)
    - Umožňuje řetězení rozšiřujících záhlaví
6. **Hop Limit** (8 bitů)
    - Ekvivalent TTL v IPv4
    - Maximální počet směrovačů, kterými může paket projít
7. **Zdrojová adresa** (128 bitů)
    - IPv6 adresa odesílatele
8. **Cílová adresa** (128 bitů)
    - IPv6 adresa příjemce
9. **Rozšiřující záhlaví** (volitelné)
    - Obsahuje dodatečné informace a funkce
    - Typické rozšiřující záhlaví: Hop-by-Hop Options, Routing, Fragment, Destination Options, Authentication, ESP
##### RIP (Routing Information Protocol)
- Jednoduchý směrovací protokol využívající směrování podle vzdálenosti
- Používá metodu počtu přeskoků (hop count) s maximem 15 skoků
- Snadno konfigurovatelný, vhodný pro malé sítě
##### NDP (Neighbor Discovery Protocol)
- IPv6 náhrada ARP používaná v IPv4
- Zajišťuje zjišťování sousedů a směrovačů
- Používá zprávy ICMPv6 (typy 133-137)
- Hlavní funkce:
    - Objevování směrovačů (Router Discovery)
    - Autokonfigurace adres (Stateless Address Autoconfiguration)
    - Zjišťování duplicitních adres (Duplicate Address Detection)
    - Určení parametrů sítě (např. MTU)
    - Překlad IP adres na MAC adresy
    - Monitorování dostupnosti sousedů (Neighbor Unreachability Detection)
- Používá multicastové adresy pro efektivnější komunikaci
- Nabízí zvýšenou bezpečnost oproti ARP díky možnosti využití IPsec
#### 3) Princip paketového přenosu dat
##### Princip
1) Data jsou **rozdělena do menších částí** (paketů), které jsou **nezávisle přenášeny** sítí
    - Umožňuje paralelní přenos dat po různých cestách
    - Maximální velikost paketu je omezena hodnotou MTU (Maximum Transmission Unit)
    - Při výpadku je nutné znovu poslat pouze poškozené pakety, ne celou zprávu
2) Každý paket **obsahuje header** (hlavičku) s informacemi o **zdrojové** a **cílové IP adrese** a **datovou část** (payload) obsahující přenášenou zprávu
    - Hlavička obsahuje také řídící informace pro směrování a správu paketu
    - Součástí je TTL (Time To Live) nebo Hop Limit určující maximální počet skoků
    - Obsahuje také identifikační údaje pro správné sestavení a kontrolní součty
3) Paketový přenos umožňuje **efektivnější využití** sítě než přepojování okruhů
    - Protože různé pakety můžou jít různými cestami
    - Umožňuje sdílení přenosové kapacity mezi více komunikacemi
    - Zvyšuje odolnost sítě proti výpadkům (redundantní cesty)
    - Eliminuje plýtvání šířkou pásma při nečinnosti (na rozdíl od vyhrazených okruhů)
4) Zajišťuje **směrování** (routing) paketů **mezi sítěmi**
    - Využívá směrovací tabulky založené na síťových adresách
    - Podporuje statické i dynamické směrovací protokoly (RIP, OSPF, BGP)
    - Umožňuje automatické přesměrování při výpadku části sítě
5) IP směrovače (routery) analyzují hlavičky paketů a **rozhodují o jejich cestě** v síti
    - Používají síťové masky pro určení příslušnosti k síti
    - Provádějí směrování na základě nejdelšího shodného prefixu (longest prefix match)
    - Udržují směrovací tabulky s informacemi o dostupných sítích
    - Mohou prioritizovat pakety podle QoS (Quality of Service) požadavků
6) Pokud paket putuje přes více sítí, může **být fragmentován a znovu sestaven**
    - Fragmentace nastává, když je MTU cílové sítě menší než velikost paketu
    - Každý fragment má vlastní hlavičku pro správné směrování
    - Opětovné sestavení provádí až cílové zařízení nebo hraniční směrovač
    - V IPv6 fragmentaci provádí pouze výchozí uzel, ne směrovače
7) **Nezaručuje spolehlivé doručení** ani zachování pořadí paketů
    - Pracuje na principu "best effort delivery"
    - Spolehlivost a správné pořadí zajišťuje vyšší vrstva (typicky TCP)
    - Pakety mohou být zahozeny při přetížení sítě nebo vypršení TTL
8) Podporuje různé **typy přenosu**
    - Unicast (jeden odesílatel, jeden příjemce)
    - Multicast (jeden odesílatel, více příjemců)
    - Broadcast (jeden odesílatel, všichni příjemci v dané síti)
    - Anycast (jeden odesílatel, nejbližší uzel z množiny příjemců)
