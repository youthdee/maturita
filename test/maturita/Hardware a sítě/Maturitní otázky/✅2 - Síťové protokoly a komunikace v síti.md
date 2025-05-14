#### 1) Princip přenosu dat v počítačové síti
##### Prvky komunikace
1) **Zdroj**:
	- Odesílatel zprávy
2) **Cíl**:
	- Příjemce zprávy
3) **Komunikační kanál**:
	- Poskytující cestu pro přenos zprávy od zdroje k cíli
##### Možnosti doručení zpráv
1) **Unicast**:
	- Z jednoho zdroje k jednomu cíli
2) **Multicast**:
	- Z jednoho zdroje k více cílům, ale ne ke všem dostupným
	- IPv6 používá jako broadcast, např `ff02::1` pro LAN
3) **Broadcast**:
	- Z jednoho zdroje ke všem dostupným cílům (bez IPv6)
 4) **Anycast** (`IPv6`):
	 - Paket je doručen nejbližšímu zařízení ze skupiny se stejnou anycast adresou.
		 - Anycast adresa je adresa, která se sdílí mezi více uzly
##### Základní principy přenosu dat
1) **Segmentace dat**:
	- Data jsou rozdělena na menší části (paket nebo rámec)
2) **Adresace a směrování**:
	- Každé zařízení v síti má svou MAC adresu na L2 a IP adresu na L3
3) **Metody přenosu**:
	- Unicast, Multicast, Broadcast
4) **Protokoly pro spolehlivý přenos dat**:
	- `TCP` (Zajišťuje spolehlivý přenos dat s kontrolou chyb a potvrzením přijetí, pracuje se segmenty)
	- ``UDP`` (méně spolehlivý, ale rychlejší přenos dat bez kontroly chyb, pracuje s datagramy)
5) **Kontrola chyb a oprava**:
	- Data prochází kontrolou integrity pomocí kontrolních součtů
	- V případě ztráty nebo poškození paketu je požádáno o přeposlání
6) **Synchronizace a řízení toku dat**:
	1) **Flow control**:
		- Zajišťuje, aby odesílatel neposílal více dat, než je příjemce schopen zpracovat
		- `TCP`
	2) **Congestion control**:
		- Zabraňuje přetížení sítě, které může způsobit ztrátu paketů
		- Principem fungování je přizpůsobení rychlosti přenosu podle aktuálního stavu sítě
		- `TCP`
7) **Šifrování a zabezpečení**:
	- Protokoly jako `SSL` a `TLS` chrání data během přenosu, např. při komunikaci přes `HTTPS`
		- Využívá se asymetrické (`RSA`) nebo symetrické (`AES`) kryptografie
	- Zajišťují autentizaci, šifrování a integritu dat.
	- Chrání před útoky jako odposlech nebo útoky typu MitM
#### 2) Komunikační protokoly a jejich funkce
##### Komunikační protokoly
- Protokoly jsou **pravidla**, kterými se komunikace řídí:
	- Obě strany používají stejný protokol
- Různé protokoly obsahují různá komunikační pravidla
##### Funkce komunikačních protokolů
1) **Identifikace odesílatele a příjemce**
2) **Kódování a dekódování zprávy**:
	- Proces převodu zprávy do podoby vhodné pro přenos po přenosovém prostředku a naopak
3) **Formátování a zapouzdření zprávy**:
	- Před odesláním musí mít zpráva formát a strukturu
	- Každý protokol, který se podílí na odeslání zprávy má svůj vlastní formát
	- Formát a struktura zprávy závisí i na vlastnostech komunikačního kanálu
4) **Určení velikosti zprávy**:
	- Velikost zprávy musí být taková, aby ji komunikační kanál dokázal přenést tak, aby šla dekódovat
5) **Rychlost a časování zpráv**:
	1) **Flow control**:
		- Zajišťuje, aby odesílatel neposílal více dat, než je příjemce schopen zpracovat
		- `TCP`
	2) **Congestion control**:
		- Zabraňuje přetížení sítě, které může způsobit ztrátu paketů
		- Principem fungování je přizpůsobení rychlosti přenosu podle aktuálního stavu sítě
		- `TCP`
6) **Response timeout**:
	- Spravuje, jak dlouho zdroj čeká na odpověď od cíle
7) **Přístupová metoda (access method)**:
	- Určuje, kdy může zdroj odeslat zprávu tak, aby jeho zpráva nekolidovala s jinými zprávami a nepoškodila se (při použití sdíleného přenosového prostředku)
	- `CSMA/CD` (Koaxial)
	- `CSMA/CA` (WLAN)
#### 3) Síťové modely ISO/OSI a TCP/IP a jejich protokoly
##### Referenční model OSI obecně
- Přijat v roce **1984**
- Definuje **sedm vrstev**, které byly vytvořeny tak, aby počet interakcí přes rozhraní mezi vrstvami byl co nejmenší
- **Spodní tři vrstv**y jsou zaměřeny na **přenos dat**
- **Horní tři vrstvy** jsou zaměřeny na **aplikace**
- **Prostřední** vrstva vyrovnává rozdíly (**transportní**)
- Fyzická a linková vrstva řeší nezbytné postupy pro přístup k médiím a fyzické prostředky pro odesílání dat přes síť
##### Vrstvy Referenčního modelu OSI
1. **Fyzická vrstva**
    - Specifikuje fyzickou komunikaci, aktivuje, udržuje a deaktivuje fyzické spoje, popisuje jakým způsobem budou data převedeny na bity, které jsou pak přenositelné přes fyzické médium
    - `DSL`, `Wi-Fi`
2. **Linková (spojová) vrstva**
    - Poskytuje spojení mezi dvěma sousedními uzly, uspořádává data z fyzické vrstvy do logických celků (rámce)
    - Na této vrstvě pracují huby a switche (přepínače)
    - `Ethernet`
3. **Síťová vrstva**
    - Smyslem této vrstvy je směrování v sítí a síťové adresování, poskytuje spojení mezi systémy, které spolu přímo nesousedí, pracuje s pakety
    - Na této vrstvě pracují routery (směrovače)
    - `IP`, `ICMP`
4. **Transportní vrstva**
    - Zajišťuje přenos dat mezi koncovými uzly, jejím účelem je poskytnout takovou kvalitu přenosu, jakou požadují vyšší vrstvy
    - `TCP` (segment) a `UDP` (datagram)
5. **Relační vrstva**
    - Funkcí této vrstvy je organizovat a synchronizovat komunikaci mezi spolupracujícími relačními vrstvami obou systémů a řídit výměnu dat mezi nimi. (Vytvoření a ukončení relačního spojení)
    - `NetBIOS`, `RPC`
6. **Prezentační vrstva**
    - Transformuje data do tvaru, který aplikace používají (šifrování, konvertování, komprimace)
    - `SLL`, `TLS`, `MP3`, `MP4`, `JPEG`, `GIF`
7. **Aplikační vrstva**
    - Obsahuje aplikační protokoly zajišťující spolupráci prostřednictvím komunikačního kanálu
    - `HTTP`, `HTTPS`, `FTP`, `DNS`, `DHCP`, `POP3`, `SSH`, `Telnet`, `TFTP`
##### Referenční model TCP/IP
- Na rozdíl od modelu OSI neurčuje, jaké protokoly se mají použít při přenosu přes fyzické médium
- Zaměřuje se více na praktické použití v reálných sítích a neimplementuje každý krok modelu OSI samostatně
- Praktičtější a jednodušší pro implementaci
##### Vrstvy Modelu TCP/IP
- **Vrstva síťového rozhraní**
    - Nejnižší vrstva umožňuje přístup k fyzickému přenosovému médiu, je specifická pro každou síť v závislosti na její implementaci
    - `Ethernet`, `Token Ring`, `FDDI`
- **Síťová vrstva**
    - Zajišťuje především síťovou adresaci, směrování a předávání datagramů
    - `IP`, `ARP`, `ICMP`, `IPSec`
    - Je implementována ve všech prvcích sítě
- **Transportní vrstva**
    - Poskytuje transportní služby pro kontrolu celistvosti dat, je implementována až v koncových uzlech a umožňuje přizpůsobit chování sítě potřebám aplikace
    - `TCP` a `UDP`
- **Aplikační vrstva**
    - Vrstva aplikací, jedná se o protokoly, které slouží ke konkrétnímu přenosu dat
    - `HTTP`, `HTTPS`, `FTP`, `DNS`, `DHCP`, `POP3`, `SSH`, `Telnet`, `TFTP`
#### 4) Standardizační organizace
##### Princip činnosti standardizačních organizací
- Vytvářejí jednotné normy a protokoly
- Zajišťují kompatibilitu zařízení různých výrobců
- Umožňují bezproblémovou komunikaci mezi sítěmi
- Eliminují technologickou roztříštěnost
- Zvyšují bezpečnost a spolehlivost
- Podporují globální technologický pokrok
- Definují "společný jazyk" pro síťová zařízení
- Stanovují technické specifikace a postupy
##### IEEE (Institute of Electrical and Electronics Engineers)
- **Zaměření:** Fyzická a linková vrstva
- **Popis:** Největší profesní organizace na světě zaměřená na rozvoj technologií. Vytváří standardy pro široké spektrum elektronických a elektrotechnických technologií včetně počítačových sítí.
- **Příklady standardů:**
    - IEEE 802.3 (Ethernet) - definuje technologie pro kabelové LAN sítě
    - IEEE 802.11 (Wi-Fi) - standard pro bezdrátové LAN sítě
    - IEEE 802.15 (Bluetooth, ZigBee) - standard pro bezdrátové PAN sítě
    - IEEE 802.1Q - standard pro VLAN
    - IEEE 802.1D - standard pro STP (Spanning Tree Protocol)
##### ISO (International Organization for Standardization)
- **Zaměření:** Určuje, jak má síť fungovat
- **Popis:** Mezinárodní organizace pro normalizaci, která vytváří a publikuje mezinárodní standardy ve všech technických a netechnických oblastech. V oblasti sítí definuje referenční modely a protokoly.
- **Příklady standardů:**
    - ISO/OSI model (Open Systems Interconnection) - sedmivrstvý referenční model pro síťovou komunikaci
    - ISO 8877 - standard pro konektor RJ-45
    - ISO/IEC 11801 - standard pro strukturovanou kabeláž
    - ISO 9001 - standard pro systémy řízení kvality (včetně síťových služeb)
    - ISO 27000 - série standardů pro bezpečnost informací
##### IEC (International Electrotechnical Commission)
- **Zaměření:** Tvoří mezinárodní standardy pro elektrotechniku, elektroniku a komunikační technologie
- **Popis:** Mezinárodní organizace, která vytváří a publikuje standardy pro všechny elektrické, elektronické a příbuzné technologie. Často spolupracuje s ISO na vývoji společných standardů.
- **Příklady standardů:**
    - IEC 60793 - standardy pro optická vlákna
    - IEC 61131 - standardy pro průmyslové sítě
    - IEC 60950 - bezpečnost IT zařízení
    - IEC 62061 - standardy pro průmyslové komunikační sítě
    - IEC 61508 - standardy pro funkční bezpečnost elektronických systémů
##### IANA (Internet Assigned Numbers Authority)
- **Zaměření:** Spravuje IP adresy, porty, DNS záznamy a protokoly na globální úrovni
- **Popis:** Organizace odpovědná za koordinaci některých klíčových prvků fungování internetu. Spravuje globální přidělování IP adres, správu DNS kořenových zón a přidělování čísel protokolů.
- **Příklady standardů a správy:**
    - Správa IPv4 a IPv6 adresních prostorů
    - Spravování registru čísel portů (0-1023 dobře známé porty, 1024-49151 registrované porty)
    - Přidělování čísel autonomních systémů (AS)
    - Správa kořenové zóny DNS
    - Správa parametrů protokolů jako MIME typy, URI schémata
##### ICANN (Internet Corporation for Assigned Names and Numbers)
- **Zaměření:** Řídí domény a IP adresy, DNS záznamy
- **Popis:** Nezisková organizace odpovědná za koordinaci údržby a postupů několika databází spojených s jmennými prostory internetu. Dohlíží na přidělování IP adres a správu systému doménových jmen.
- **Příklady činností a standardů:**
    - Správa generických TLD (Top-Level Domains) jako .com, .org, .net
    - Dohled nad ccTLD (Country Code TLD) jako .cz, .sk, .de
    - Zavedení nových TLD (např. .shop, .tech, .app)
    - Dohlíží na provoz kořenových DNS serverů
    - Správa systému WHOIS pro registraci domén
    - Implementace DNSSEC (DNS Security Extensions)
##### IETF (Internet Engineering Task Force)
- **Zaměření:** Spravuje protokoly internetu
- **Popis:** Otevřená mezinárodní komunita síťových odborníků, která vyvíjí a podporuje internetové standardy. Vydává dokumenty RFC (Request for Comments), které popisují metody, výzkumy nebo inovace aplikovatelné na fungování internetu.
- **Příklady standardů:**
    - TCP/IP - základní protokoly internetu
    - HTTP/HTTPS - protokoly pro webovou komunikaci
    - SMTP, POP3, IMAP - protokoly pro e-mailovou komunikaci
    - FTP - protokol pro přenos souborů
    - DNS - systém doménových jmen
    - BGP - protokol pro směrování mezi autonomními systémy
    - TLS/SSL - protokoly pro zabezpečení komunikace