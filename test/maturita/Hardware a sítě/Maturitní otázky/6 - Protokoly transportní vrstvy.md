#### 1) Účel, funkce transportní vrstvy, protokoly transportní vrstvy

##### Účel transportní vrstvy
- Poskytování komunikačních služeb point-to-point nejen mezi hostiteli, ale i mezi aplikacemi hostitelů
- Čtvrtá vrstva modelu ISO/OSI (L4)
	- Poskytuje služby vrstvě relační (L5)
- Jednotkou dat (PDU) je segment či datagram
	- Zapouzdřuje data protokolů aplikační vrstvy
- Doručování jednotek může být garantováno
	- Záleží na daném protokolu L4, zda doručení garantuje nebo ne
##### Funkce transportní vrstvy
- Komunikace orientovaná na spojení či zprávy
	- Spojení se chovají jako obousměrný datový proud
- Spolehlivé doručování dat
	- Typický rys proudového protokolu transportní vrstvy (ne každý protokol to garantuje)
- Řízení toku dat
	- Proudově orientovaný protokol se přizpůsobuje podle aktuální propustnosti přenosové cesty
- Sdružování komunikace (Multiplexing)
	- Z jednoho počítače může komunikovat více aplikací

##### TCP (Transmission Control Protocol)
- Zajišťuje spolehlivou, spojovanou komunikaci
	- Nejprve musí být navázáno spojení
- Identifikátorem koncového bodu je port
	- 16 bitové číslo v rozsahu 0 až 65535
- Datovou jednotkou je segment
	- Odpovídá úseku dat přenášených v proudu
- Součástí sady Internet Protocol Suite
- Vhodný pro přenos souvislých datových celků (webové stránky, dokumenty, terminálový přístup)
- Poskytuje spolehlivé, plně-duplexní spojení (řešeno pomocí pozitivního potvrzování přijetí dat)
- Doručuje se dle aktuálního stavu síťové cesty (to může přinést delší prodlevy v doručování)
- Není-li potvrzení přijetí dat přijato v časovém limitu, segment je odeslán znovu (upoždění komunikace)
- Řízení toku dat (flow control)
	- Povrzování po skupinách segmentů umožňuje regulovat objem dat odeslaný naráz a zároveň snižuje režii potvrzování
- Stavová komunikace
	- Pro zahájení komunikace je třeba provést 3-way handshake
	- Pro ukončení komunikace je třeba z každé strany ukončit spojení
- Příklady použití v aplikačních protokolech:
	- HTTP, SMTP, SSH, TELNET, DNS
##### UDP (User Datagram Protocol)
- Zajišťuje nespolehlivou, nespojovanou komunikaci
	- Spojení se v tomto případě nenavazuje
- Identifikátorem koncového bodu je port
	- 16 bitové číslo v rozsahu 0 až 65535
- Datovou jednotkou je datagram
	- Odpovídá datům přenášených v podobě samostatné zprávy
- Příklady použití v aplikačních protokolech:
	- LDAP, DNS, NTP, RTP
- Součástí sady Internet Protocol Suite
- Jednoduchý, transakčně orientovaný protokol
	- Vhodný pro interakce typu požadavek-odpověď
- Bezestavový, pro velký počet klientů (např. pro video streaming)
- Podporuje boradcast i multicast
	- Vhodný pro účely detekce služeb v lokální síti
- Vlastnosti protokolu UDP:
	- Nenavazuje spojení (datagram je rovnou zaslán příjemci)
	- Nízká režie (přenáší se výhradně datagramy nesoucí data)
	- Nevyžaduje potvrzování (odesílatel nečeká na příjem potvrzovacích zpráv)
	- Neopakuje ztracená data (pokračuje se zasíláním dalších dat)
	- Nezaručuje data v pořadí (datagramy lze doručovat různými cestami v síti)
#### 2) Porty aplikací

##### Skupiny portů
- IANA (Internet Assigned Numbers Authority) je organizace, která definuje přiřazení čisel portů aplikacím
- Skupiny portů:
	- Well-known porty (0 až 1023):
		- Rezervovány pro služby a aplikace
		- Např. 21 (FTP), 25 (SMTP), 80 (HTTP)
	- Registrované porty (1024 až 49151):
		- Registrovány na vyžádání třetích stran
		- Např. 1433 (SQL), 3389 (RDP)
	- Dynamické/Privátní porty (49152 až 65535):
		- Přidělovány při navazování spojení (efemerální)
#### 3) 3-way handshake a ukončení spojení
##### Příznaky TCP segmentu
- SYN "SYNCHRONIZE" ('Navazování spojení)
- ACK "ACKNOWLEDGE" (Potvrzování)
- FIN "FINISH" (Ukončení spojení)
- PSH "PUSH" (Předání dat aplikací)
- RST "RESET" (Ukončení spojení)
- URG "URGNET" (Urgentní data)

##### Navázání TCP spojení (3-way handshake)
1) Klient zašle SYN segment s požadovaným sekvenčním číslem
2) Server odpoví SYN + ACK segmentem s požadovaným sekvenčním číslem
3) Klient zašle ACK segment, kterým serveru potvrdí přijetí

##### Ukončení TCP spojení
1) Klient zašle FIN segment
2) Server odpoví ACK segmentem, kterým klientovi potvrdí přijetí
3) Server zašle FIN segment
4) Klient zašle ACK segment, kterým serveru potvrdí přijetí