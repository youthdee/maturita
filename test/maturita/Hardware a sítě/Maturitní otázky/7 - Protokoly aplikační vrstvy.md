#### 1) Účel, funkce a charakteristika protokolů aplikační vrstvy
##### Účel aplikační vrstvy
- **7. vrstva** modelu síťové architektury OSI
- Poskytuje aplikacím **přístup ke komunikačnímu systému** a umožňuje jim tak jejich **spolupráci**
- Teoreticky řečeno umožňuje aplikacím komunikovat přes síť, aniž by se uživatel musel starat o detaily nižších vrstev
##### Funkce aplikační vrstvy
- Poskytuje **rozhraní mezi uživatelem a síťovými službami**
- Umožňuje **přenos dat** mezi aplikacemi na různých zařízeních
- Zajišťuje přístup k síťovým službám
- **Konkrétní funkce**:
	1) **Identifikace komunikace**:
		- Rozpoznání, která aplikace chce komunikovat
		- `HTTP`, `HTTPS`, `SMTP`
	2) **Autentizace a šifrování**:
		- Ověření identity uživatele a zabezpečení dat
		- `HTTPS`, `SSH`
	3) **Přenos souborů**:
		- Umožňuje stahování a nahrávání souborů přes síť
		- `FTP`, `TFTP`
	4) **Přenos e-mailů**:
		- Posílání a přijímání e-mailů
	5) **Překlad doménových jmen**:
		- `DNS`
	6) **Vzdálená správa**:
		- Bezpečné připojení k jinému zařízení na dálku
		- `SSH`, `Telnet`
##### Charakteristika protokolů aplikační vrstvy - FTP (File Transfer Protocol)
- Standardní komunikační protokol pro **přenos souborů** mezi počítači prostřednictvím počítačové sítě
- **Stavový protokol**, postaveno na architektuře **klient-server**
- Umožňuje **řízení přístupu**
- Port `TCP 21` slouží **k řízení** a jsou jím také přenášeny **příkazy FTP**
- Port `TCP 20` slouží k vlastnímu **přenosu dat**
##### Charakteristika protokolů aplikační vrstvy -  TFTP (Trivial Transfer Protocol)
- Jednoduchý protokol **pro přenos souborů** obsahující **pouze základní funkce protokolu FTP**
- Je vhodný pro případy, kdy FTP je nevhodný pro svou komplikovanost
- Používá `UDP port 69`
##### Charakteristika protokolů aplikační vrstvy -  HTTP (Hypertext Transfer Protocol)
- Slouží pro **přenos hypertextových dokumentů** ve formátu `HTML`, `XML` a dalších
- Internetový protokol určený **pro komunikaci** s `WWW` servery
- Protokol funguje způsobem **dotaz-odpověď**
- Samostatný `HTTP` protokol **neumožňuje šifrování** ani **zabezpečení integrity dat**
- Funguje na portu `TCP 80`
##### Charakteristika protokolů aplikační vrstvy -  HTTPS
- Stejné jako `HTTP`
- Opatřen **šifrováním**
- Funguje na portu `TCP 443`
##### Charakteristika protokolů aplikační vrstvy - IMAP (Internet Message Access Protocol)
- Slouží pro vzdálený **přístup k e-mailové schránce** prostřednictvím **e-mailového klienta**
- Na rozdíl od `POP3` nabízí pokročilejší možnosti vzdálené správy:
	- Práce se složkami a přesouvání zpráv mezi nimi,
	- Prohledávání na straně serveru a podobně
	- Práce v online a offline režimu
- Současně se používá `IMAP4`, na `TCP portech 143, 220 a 993` (**IMAP přes SSL**)
##### Charakteristika protokolů aplikační vrstvy - POP3
- Internetový protokol sloužící **pro stahování e-mailových** zpráv ze vzdáleného serveru z klienta
- Pracuje přes `TCP portu 110`
- V současnosti je používána zejména verze `POP3`
- Ze serveru se stáhnou **všechny zprávy**, bez ohledu na jejich prioritu
- Princip komunikace spočívá ve výměně zpráv mezi klientem a serverem
##### Charakteristika protokolů aplikační vrstvy - LDAP (Lightweight Directory Access Protocol)
- Definovaný protokol pro **ukládání a přístup k datům na adresářovém serveru**
- Položky jsou ukládány **formou záznamů** a uspořádány do stromové struktury
- Funguje na bázi **klient-server**
- Součástí `LDAP` je **autentizace klienta**
- Pracuje na portech `TCP/UDP 389` **nešifrovaně** a `TCP port 636` **šifrovaně**
##### Charakteristika protokolů aplikační vrstvy -  SMTP (Simple Mail Transfer Protocol)
- Protokol určený pro **přenos zpráv e-mailů mezi přepravci elektronické pošty** (MTA)
- Zajišťuje doručení emailů pomocí přímého spojení mezi odesílatelem a adresátem
	- Zpráva je doručena do poštovní schránky, ke které potom může uživatel kdykoli přistoupit
	- Buď přímo na serveru, nebo z jiného zařízení pomocí protokolů jako POP3 nebo IMAP
- Používá port TCP 25 pro komunikaci mezi poštovními servery a port `TCP 587` pro příjem emailů od e-mailových klientů
##### Charakteristika protokolů aplikační vrstvy -  DNS (Domain Name System)
- Slouží k překladu **doménových jmen na IP adresy**
- **Hierarchická struktura**
- Používá porty `TCP/UDP 53`
##### Charakteristika protokolů aplikační vrstvy - DHCP (Dynamic Host Configuration Protocol)
- Prostřednictvím DHCP serveru nastavuje stanicím v lokální síti **adresní parametry** nutných pro komunikaci pomocí IP protokolu:
	- IP adresa
	- Maska podsítě
	- Výchozí brána
	- DNS server
- **Zjednodušuje** a **centralizuje správu** počítačové sítě
- Klient komunikuje na `UDP portu 68`
- Server naslouchá na `UDP portu 67`
##### Charakteristika protokolů aplikační vrstvy -  SSH (Secure Shell)
- Zabezpečený komunikační protokol zajišťující bezpečnou **komunikaci mezi dvěma počítači**, která se využívá pro zprostředkování **přístupu k příkazovému řádku**, **kopírování souborů** a obecně **jakýkoliv přenos dat** (s využitím síťového tunelování)
- Navržen jako náhrada za `telnet`
- Pro autentizaci je možné použít **veřejný klíč**
- Klient se při navázání spojení připojuje k **SSH démonu**
- Pracuje běžně na portu `TCP 22`
##### Charakteristika protokolů aplikační vrstvy -  TELNET (Teletype Network)
- Umožňuje **připojení ke vzdálenému počítači** pomocí CLI
- Komunikace **není přenášena šifrovaně**
- Lze použít pro ruční komunikaci otevřenými protokoly jako `SMTP` a `HTTP`
- Používá se pro **realizaci spojení typu klient-server** na `TCP`, přičemž přenáší komunikaci duplexně
- Serverová část standardně naslouchá na portu `TCP 23`
##### Charakteristika protokolů aplikační vrstvy -  SNMP
- Standardně využívá `UDP port 161`
- Slouží k **potřebám správy sítí**, umožňuje **průběžný sběr nejrůznějších dat** pro potřeby správy sítě a jejich následné vyhodnocování
- Na tomto protokolu je založena **většina programů pro správu sítě**
- **Síť řízená pomocí SNMP se skládá ze tří částí**:
	1) Spravované zařízení
	2) Agent
		- Software, který běží na spravovaných zařízeních
	3) NMS (Network Management Station)
		- Software, který běží na správcovských zařízeních
#### 2) Přehled protokolů aplikační vrstvy

##### Webové aplikace a stránky
- `HTTP`
- `HTTPS`
##### Stahování, nahrávání souborů
- `FTP`
- `TFTP`
##### Připojení na dálku
- `SHH`
- `Telnet`
- `RDP`
##### Emailové služby
- `SMTP`
- `IMAP`
- `POP3`
##### Adresářové služby a autentizace
- `LDAP`
- `Kerberos`
- `RADIUS`
##### Doménová jména
- `DNS`
##### Síťová správa a monitoring
- `NTP`
- `SYSLOG`
##### Hlasová a multimediální komunikace
- `SIP`
- `RTP`
#### 3) Výběr transportního protokolu pro aplikace
##### Kritéria volby
- Požadavky na spolehlivost, rychlost a latenci přenosu
##### TCP (Transmission Control Protocol)
- **Zajišťuje spolehlivou, spojovanou komunikaci**:
	- Nejprve musí být navázáno spojení
- **Identifikátorem koncového bodu je port**:
	- 16 bitové číslo v rozsahu 0 až 65535
- **Datovou jednotkou je segment**:
	- Odpovídá úseku dat přenášených v proudu
- Součástí sady Internet Protocol Suite
- **Vhodný pro přenos souvislých datových celků**:
	- Webové stránky, dokumenty, terminálový přístup
- **Poskytuje spolehlivé, plně-duplexní spojení**:
	- Řešeno pomocí pozitivního potvrzování přijetí dat
- **Doručuje se dle aktuálního stavu síťové cesty**:
	- To může přinést delší prodlevy v doručování
- Není-li potvrzení přijetí dat přijato v časovém limitu, segment je odeslán znovu:
- **Řízení toku dat** (`flow control`):
	- Potvrzování po skupinách segmentů umožňuje regulovat objem dat odeslaný naráz a zároveň snižuje režii potvrzování
- **Stavová komunikace**:
	- Pro zahájení komunikace je třeba provést 3-way handshake
	- Pro ukončení komunikace je třeba z každé strany ukončit spojení
- **Příklady použití v aplikačních protokolech**:
	- `HTTP`, `SMTP`, `SSH`, `TELNET`, `DNS`
##### UDP (User Datagram Protocol)
- **Zajišťuje nespolehlivou, nespojovanou komunikaci**:
	- Spojení se v tomto případě nenavazuje
- **Identifikátorem koncového bodu je port**:
	- 16 bitové číslo v rozsahu 0 až 65535
- **Datovou jednotkou je datagram**:
	- Odpovídá datům přenášených v podobě samostatné zprávy
- **Příklady použití v aplikačních protokolech**:
	- `LDAP`, `DNS`, `NTP`, `RTP`
- Součástí sady Internet Protocol Suite
- **Jednoduchý**, **transakčně orientovaný protokol**:
	- Vhodný pro interakce typu požadavek-odpověď
	- Bezestavový, pro velký počet klientů
		- Video streaming
- **Podporuje boradcast i multicast**:
	- Vhodný pro účely detekce služeb v lokální síti
- Vlastnosti protokolu UDP:
	1) **Nenavazuje spojení**:
		- Datagram je rovnou zaslán příjemci
	2) **Nízká režie**:
		- Přenáší se výhradně datagramy nesoucí data
	3) **Nevyžaduje potvrzování**:
		- Odesílatel nečeká na příjem potvrzovacích zpráv
	4) **Neopakuje ztracená data**:
		- Pokračuje se zasíláním dalších dat
	5) **Nezaručuje data v pořadí**:
		- Datagramy lze doručovat různými cestami v síti