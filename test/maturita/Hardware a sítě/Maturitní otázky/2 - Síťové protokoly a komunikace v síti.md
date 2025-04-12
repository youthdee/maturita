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
3) **Broadcast**:
	- Z jednoho zdroje ke všem dostupným cílům (bez IPv6)
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
	- Flow control (zajišťuje, aby odesílatel neposílal více dat, než je příjemce schopen zpracovat)
	- Congestion control (zabraňuje přetížení sítě)
7) **Šifrování a zabezpečení**:
	- Protokoly jako `SSL` a `TLS` chrání data během přenosu, např. při komunikaci přes `HTTPS`
	- Autentizace a šifrování chrání před útoky jako odposlech nebo útoky typu MitM
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
5) **Rychlost a timing (časování) zpráv**:
	1) **Řízení toku (flow control)**:
		- Spravuje rychlost přenosu dat, definuje kolik dat lze odesílat a jak rychle po sobě tak, aby nedošlo k zahlcení příjemce
	2) **Response timeout**:
		- Spravuje, jak dlouho zdroj čeká na odpověď od cíle
	3) **Přístupová metoda (access method)**:
		- Určuje, kdy může zdroj odeslat zprávu tak, aby jeho zpráva nekolidovala s jinými zprávami a nepoškodila se (při použití sdíleného přenosového prostředku)
#### 3) Síťové modely ISO/OSI a TCP/IP a jejich protokoly
##### Referenční model OSI obecně
- Přijat v roce **1984**
- Definuje **sedm vrstev**, které byly vytvořeny tak, aby počet interakcí přes rozhraní mezi vrstvami byl co nejmenší
- **Spodní tři vrstv**y jsou zaměřeny na **přenos dat**
- **Horní tři vrstvy** jsou zaměřeny na **aplikace**
- **Prostřední** vrstva vyrovnává rozdíly (**transportní**)
- Fyzická a linková vrstva řeší nezbytné postupy pro přístup k médiím a fyzické prostředky pro odesílání dat přes síť
##### Vrstvy Referenčního modelu OSI
1) **Aplikační vrstva**:
	- Obsahuje aplikační protokoly zajišťující spolupráci prostřednictvím komunikačního kanálu
	- `HTTP`, `HTTPS`, `FTP`, `DNS`, `DHCP`, `POP3`, `SSH`, `Telnet`, `TFTP`
2)  **Prezentační vrstva**
	- Transformuje data do tvaru, který aplikace používají (šifrování, konvertování, komprimace)
	- `SMB`
3)  **Relační vrstva**
	- Funkcí této vrstvy je organizovat a synchronizovat komunikaci mezi spolupracujícími relačními vrstvami obou systémů a řídit výměnu dat mezi nimi. (Vytvoření a ukončení relačního spojení)
	- `NetBIOS`, `RPC`
4)  **Transportní vrstva**
	- Zajišťuje přenos dat mezi koncovými uzly, jejím účelem je poskytnout takovou kvalitu přenosu, jakou požadují vyšší vrstvy
	- `TCP` (segment) a `UDP` (datagram)
5)  **Síťová vrstva**
	- Smyslem této vrstvy je směrování v sítí a síťové adresování, poskytuje spojení mezi systémy, které spolu přímo nesousedí, pracuje s pakety
	- Na této vrstvě pracují routery (směrovače)
	- `IP`, `ICMP`
6)  **Linková (spojová) vrstva**
	- Poskytuje spojení mezi dvěma sousedními uzly, uspořádává data z fyzické vrstvy do logických celků (rámce)
	- Na této vrstvě pracují huby a switche (přepínače)
	- `Ethernet`
7)  **Fyzická vrstva**
	- Specifikuje fyzickou komunikaci, aktivuje, udržuje a deaktivuje fyzické spoje, popisuje jakým způsobem budou data převedeny na bity, které jsou pak přenositelné přes fyzické médium
	- `DSL`, `Wi-Fi`
##### Referenční model TCP/IP
- Na rozdíl od modelu OSI neurčuje, jaké protokoly se mají použít při přenosu přes fyzické médium
##### Vrstvy Modelu TCP/IP
1) **Aplikační vrstva**
	- Vrstva aplikací, jedná se o protokoly, které slouží ke konkrétnímu přenosu dat
	- `HTTP`, `HTTPS`, `FTP`, `DNS`, `DHCP`, `POP3`, `SSH`, `Telnet`, `TFTP`
2) **Transportní vrstva**
	- Poskytuje transportní služby pro kontrolu celistvosti dat, je implementována až v koncových uzlech a umožňuje přizpůsobit chování sítě potřebám aplikace
	- `TCP` a `UDP`
3) **Síťová vrstva**
	- Zajišťuje především síťovou adresaci, směrování a předávání datagramů
	- `IP`, `ARP`, `ICMP`, `IPSec`
	- Je implementována ve všech prvcích sítě
4) **Vrstva síťového rozhraní**
	- Nejnižší vrstva umožňuje přístup k fyzickému přenosovému médiu, je specifická pro každou síť v závislosti na její implementaci
	- `Ethernet`, `Token Ring`, `FDDI`
#### 4) Standardizační organizace
##### Nejvlivnější standardizační organizace
1) **IEEE (Institute of Electrical and Electronics Engineers)**
	- Fyzická, linková vrstva
2) **ISO (International Organization for Standardization)**
	- Určuje, jak má síť fungovat
3) **IEC (International Electrotechnical Commision)**
	- Tvoří mezinárodní standardy pro elektrotechniku, elektroniku a komunikační technologie
4) **IANA (Internet Assigned Numbers Authority)**
	- Spravuje IP adresy, porty, DNS záznamy a protokoly na globální úrovni
5) **ICANN (Interent Corporation for Assigned Names and NUmbers)**
	- Řídí domény a IP adresy, DNS záznamy
6) **IETF (Internet Engineering Task Force)**
	- Spravuje protokoly internetu (TCP/IP, `HTTP`)