#### 1) Účel, funkce transportní vrstvy, protokoly transportní vrstvy
##### Účel transportní vrstvy
- Poskytování **komunikačních služeb point-to-point** nejen mezi hostiteli, ale i mezi aplikacemi hostitelů
- **Čtvrtá vrstva modelu** `ISO/OSI` (`L4`)
	- Poskytuje služby vrstvě relační (L5)
- **Jednotkou dat (PDU) je segment či datagram**:
	- Zapouzdřuje data protokolů aplikační vrstvy
- **Doručování jednotek může být garantováno**:
	- Záleží na daném protokolu L4, zda doručení garantuje nebo ne
##### Funkce transportní vrstvy
1) **Komunikace orientovaná na spojení či zprávy**:
	- Spojení se chovají jako obousměrný datový proud
2) **Spolehlivé doručování dat**:
	- Typický rys proudového protokolu transportní vrstvy (ne každý protokol to garantuje)
3) **Řízení toku dat**:
	- Proudově orientovaný protokol se přizpůsobuje podle aktuální propustnosti přenosové cesty
4) **Sdružování komunikace** (`Multiplexing`):
	- Z jednoho počítače může komunikovat více aplikací
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
#### 2) Porty aplikací
##### Skupiny portů
- **IANA** (Internet Assigned Numbers Authority) je organizace, která definuje přiřazení čísel portů aplikacím
- Porty jsou 16-bitová čísla (rozsah 0-65535) identifikující síťové procesy na zařízení
- Kombinace IP adresy a čísla portu vytváří síťový socket
- **Skupiny portů**:
    1. **Well-known porty** (`0 až 1023`):
        - Rezervovány pro standardizované služby a aplikace
        - Vyžadují oprávnění správce pro naslouchání
        - Nejčastěji používané porty:
            - `20/21` (FTP) - přenos souborů
            - `22` (SSH) - zabezpečené připojení
            - `23` (Telnet) - nezabezpečené připojení
            - `25` (SMTP) - odesílání e-mailů
            - `53` (DNS) - překlad doménových jmen
            - `67/68` (DHCP) - automatická konfigurace IP
            - `80` (HTTP) - webové stránky
            - `110` (POP3) - příjem e-mailů
            - `143` (IMAP) - správa e-mailů
            - `443` (HTTPS) - zabezpečené webové stránky
            - `989/990` (FTPS) - zabezpečený přenos souborů
    2. **Registrované porty** (`1024 až 49151`):
        - Registrovány na vyžádání třetích stran u IANA
        - Používány pro méně běžné nebo proprietární služby
        - Významné příklady:
            - `1433` (MS SQL Server)
            - `1521` (Oracle Database)
            - `3306` (MySQL)
            - `3389` (RDP - Remote Desktop Protocol)
            - `5060/5061` (SIP - VoIP komunikace)
            - `5222` (XMPP - instant messaging)
            - `8080` (alternativní HTTP port, proxy)
    3. **Dynamické/Privátní porty** (`49152 až 65535`):
        - Přidělovány při navazování spojení (efemerální)
        - Používány klientskými aplikacemi jako zdrojové porty
        - Nejsou registrovány u IANA ani pevně přiřazeny
        - Operační systém je dynamicky alokuje při komunikaci
##### Protokoly a porty
- **TCP porty** - používány pro spojovanou komunikaci s potvrzováním
    - Zajišťují spolehlivý přenos dat ve správném pořadí
    - Vhodné pro přenos souborů, webové stránky, e-maily
- **UDP porty** - používány pro nespojovanou komunikaci bez potvrzování
    - Rychlejší, ale méně spolehlivé
    - Vhodné pro streamování médií, online hry, VoIP
##### Bezpečnostní aspekty
- Porty mohou být filtrovány firewallem
- Skenování portů je běžnou technikou při zjišťování zranitelností
- Změna výchozích portů může zvýšit bezpečnost (security by obscurity)
- Mnoho útoků cílí na známé porty a zranitelné služby
#### 3) 3-way handshake a ukončení spojení
##### Příznaky TCP segmentu
1) `SYN` (synchronize):
    -  Slouží k navázání spojení a inicializaci číslování segmentů mezi klientem a serverem
2) `ACK` (acknowledge):
    - Slouží k potvrzování přijetí dat nebo jiných segmentů – včetně `SYN` nebo `FIN`
3) `FIN` (finish):
    - Označuje žádost o ukončení spojení; po jeho odeslání se připojení uzavře jedním směrem
4) `PSH` (push):
    - Zajišťuje okamžité doručení dat aplikační vrstvě bez čekání na zaplnění vyrovnávací paměti
5) `RST` (reset):
    - Používá se k **okamžitému ukončení spojení** nebo k odmítnutí neplatného požadavku, např. pokud cílový port není aktivní
6) `URG` (urgent):
    - Indikuje, že segment obsahuje **urgentní data**, která by měla být prioritně doručena aplikaci (např. přerušení)
##### Navázání TCP spojení (3-way handshake)
1) Klient zašle `SYN` segment s požadovaným sekvenčním číslem (např. `SEQ=100`)
2) Server odpoví `SYN + ACK` segmentem – potvrdí přijetí (`ACK=101`) a pošle své sekvenční číslo (např. `SEQ=300`)
3) Klient zašle `ACK` segment (`ACK=301`), kterým serveru potvrdí přijetí a připojení je navázáno

> Během tohoto procesu se vytvoří **virtuální spojení** mezi koncovými body a dojde ke **synchronizaci číslování segmentů**. TCP garantuje spolehlivý přenos díky potvrzením (`ACK`) a řízení přenosu pomocí oken.
##### Ukončení TCP spojení
1) Klient zašle `FIN` segment (např. `SEQ=400`)
2) Server odpoví `ACK` segmentem (`ACK=401`), čímž potvrdí ukončení přenosu ze strany klienta
3) Server následně zašle `FIN` segment (např. `SEQ=700`)
4) Klient odpoví `ACK` segmentem (`ACK=701`), čímž je spojení plně ukončeno

> Ukončení spojení probíhá **obousměrně** – každá strana musí zvlášť potvrdit ukončení. Po finálním `ACK` segmentu klient přechází do tzv. **TIME_WAIT** stavu, kde ještě krátce čeká pro případ, že by bylo nutné znovu odeslat potvrzení.