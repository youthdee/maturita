#### 1) Princip přenosu dat v počítačové síti
##### Prvky komunikace
- Zdroj (odesílatel zprávy)
- Cíl (příjemce zprávy)
- Komunikační kanál (poskytující cestu pro přenos zprávy od zdroje k cíli)
##### Možnosti doručení zpráv
- Unicast:
	- Z jednoho zdroje k jednomu cíli
- Multicast:
	- Z jednoho zdroje k více cílům, ale ne ke všem dostupným
- Broadcast:
	- Z jednoho zdroje ke všem dostupným cílům (bez IPv6)
##### Základní principy přenosu dat
- Segmentace dat
	- Data jsou rozdělena na menší části (paket nebo rámec)
- Adresace a směrování
	- Každé zařízení v síti má svou MAC adresu na L2 a IP adresu na L3
- Metody přenosu
	- Unicast, Multicast, Broadcast
- Protokoly pro spolehlivý přenos dat
	- TCP (Zajišťuje spolehlivý přenos dat s kontrolou chyb a potvrzením přijetí, pracuje se segmenty)
	- UDP (méně spolehlivý, ale rychlejší přenos dat bez kontroly chyb, pracuje s datagramy)
- Kontrola chyb a oprava
	- Data prochází kontrolou integrity pomocí kontrolních součtů
	- V případě ztráty nebo poškození paketu je požádáno o přeposlání
- Synchronizace a řízení toku dat
	- Flow control (zajišťuje, aby odesílatel neposílal více dat, než je příjemce schopen zpracovat)
	- Congestion control (zabraňuje přetížení sítě)
- Šifrování a zabezpečení
	- Protokoly jako SSL a TLS chrání data během přenosu, např. při komunikaci přes HTTPS
	- Autentizace a šifrování chrání před útoky jako odposlech nebo útoky typu MitM

#### 2) Komunikační protokoly a jejich funkce
##### Komunikační protokoly
- Protokoly jsou pravidla, kterými se komunikace řídí
	- Obě strany používají stejný protokol
- Různé protokoly obsahují různá komunikační pravidla

##### Funkce komunikačních protokolů
- Identifikace odesílatele a příjemce
- Kódování a dekódování zprávy:
	- Proces převodu zprávy do podoby vhodné pro přenos po přenosovém prostředku a naopak
- Formátování a zapouzdření zprávy
	- Před odesláním musí mít zpráva formát a strukturu
	- Každý protokol, který se podílí na odeslání zprávy má svůj vlastní formát
	- Formát a struktura zprávy závisí i na vlastnostech komunikačního kanálu
- Určení velikosti zprávy
	- Velikost zprávy musí být taková, aby ji komunikační kanál dokázal přenést tak, aby šla dekódovat
- Rychlost a timing (časování) zpráv
	- Řízení toku (flow control):
		- Spravuje rychlost přenosu dat, definuje kolik dat lze odesílat a jak rychle po sobě tak, aby nedošlo k zahlcení příjemce
	- Response timeout:
		- Spravuje, jak dlouho zdroj čeká na odpověď od cíle
	- Přístupová metoda (access method):
		- Určuje, kdy může zdroj odeslat zprávu tak, aby jeho zprává nekolidovala s jinými zprávami a nepoškodila se (při použití sdíleného přenosového prostředku)
#### 3) Síťové modely ISO/OSI a TCP/IP a jejich protokoly

##### Referenční model OSI obecně
- Přijat v roce 1984
- Definuje sedm vrstev, které byly vytvořeny tak, aby počet interakcí přes rozhraní mezi vrstvami byl co nejmenší
- Spodní tři vrstvy jsou zaměřeny na přenos dat
- Horní tři vrstvy jsou zaměřeny na aplikace
- Prostřední vrstva vyrovnává rozdíly (transportní)
- Fyzická a linková vrstva řeší nezbytné postupy pro přístup k médiím a fyzické prostředky pro odesílání dat přes síť

##### Vrstvy Referenčního modelu OSI
- Aplikační vrstva:
	- Obsahuje aplikační protokoly zajišťující spolupráci prostřednictvím komunikačního kanálu
	- HTTP, HTTPS, FTP, DNS, DHCP, POP3, SSH, Telnet, TFTP
-  Prezentační vrstva
	- Transformuje data do tvaru, který aplikace používají (šifrování, konvertování, komprimace)
	- SMB
-  Relační vrstva
	- Funkcí této vrstvy je organizovat a synchronizovat komunikaci mezi spolupracujícími relačními vrstvami obou systémů a řídit výměnu dat mezi nimi. (Vytvoření a ukončení relačního spojení)
	- NetBIOS, RPC
-  Transportní vrstva
	- Zajišťuje přenos dat mezi koncovými uzly, jejím účelem je poskytnout takovou kvalitu přenosu, jakou požadují vyšší vrstvy
	- TCP (segment) a UDP (datagram)
-  Síťová vrstva
	- Smyslem této vrstvy je směrování v sítí a síťové adresování, poskytuje spojení mezi systémy, které spolu přímo nesousedí, pracuje s pakety
	- Na této vrstvě pracují routery (směrovače)
	- IP, ICMP
-  Linková (spojová) vrstva
	- Poskytuje spojení mezi dvěma sousedními uzly, uspořádává data z fyzické vrstvy do logických celků (rámce)
	- Na této vrstvě pracují huby a switche (přepínače)
	- Ethernet
-  Fyzická vrstva
	- Specifikuje fyzickou komunikaci, aktivuje, udržuje a deaktivuje fyzické spoje, popisuje jakým způsobem budou data převedeny na bity, které jsou pak přenositelné přes fyzické médium
	- DSL, Wi-Fi

##### Referenční model TCP/IP
- Na rozdíl od modelu OSI neurčuje, jaké protokoly se mají použít při přenosu přes fyzické médium

##### Vrstvy Modelu TCP/IP
- Aplikační vrstva
	- Vrstva aplikací, jedná se o protokoly, které slouží ke konkrétnímu přenosu dat
	- HTTP, HTTPS, FTP, DNS, DHCP, POP3, SSH, Telnet, TFTP
- Transportní vrstva
	- Poskytuje transportní služby pro kontrolu celistvosti dat, je implementována až v koncových uzlech a umožňuje přizpůsobit chování sítě potřebám aplikace
	- TCP a UDP
- Síťová vrstva
	- Zajišťuje především síťovou adresaci, směrování a předávání datagramů
	- IP, ARP, ICMP, IPSec
	- Je implementována ve všech prvcích sítě
- Vrstva síťového rozhraní
	- Nejnižší vrstva umožňuje přístup k fyzickému přenosovému médiu, je specifická pro každou síť v závislosti na její implementaci
	- Ethernet, Token Ring, FDDI
#### 4) Standardizační organizace

##### Nejvlivnější standardizační organizace
- IEEE (Institute of Electrical and Electronics Engineers)
	- Fyzická, linková vrstva
- ISO (International Organization for Standardization)
	- Určuje, jak má síť fungovat
- IEC (International Electrotechnical Commision)
	- Tvoří mezinárodní standardy pro elektrotechniku, elektroniku a komunikační technologie
- IANA (Internet Assigned Numbers Authority)
	- Spravuje IP adresy, porty, DNS záznamy a protokoly na globální úrovni
- ICANN (Interent Corporation for Assigned Names and NUmbers)
	- Řídí domény a IP adresy, DNS záznamy
- IETF (Internet Engineering Task Force)
	- Spravuje protokoly internetu (TCP/IP, HTTP)