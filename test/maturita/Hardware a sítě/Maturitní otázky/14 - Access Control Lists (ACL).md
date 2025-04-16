#### 1) Účel a charakteristika ACL
##### Charakteristika ACL
1) **Sada pravidel pro filtrování paketů**:
	-  `permit` pro zajištění propuštění paketu
	- `deny` pro zajištění blokování paketu
2) `ACL` = **Access Control List**
3) `ACE` = **Access Control Entry**
4) Pokud `ACL` neobsahuje pravidla, blokuje všechny pakety
	- Výchozí politika všech `ACL` je `deny`
5) Ve výchozím stavu router `ACL`s nepoužívá
##### Použití ACLs
1) **Omezení síťového provozu pro zvýšení výkonu sítě**:
	- Např. blokování videopřenosů
2) **Řízení síťového provozu**:
	- Např. omezení směrovacího protokolu pouze na určitá rozhraní
3) **Definice základní úrovně zabezpečení sítě**:
	- Např. blokace přístupu do sítě pouze pro určité hostitele
4) **Filtrace podle jeho druhu**:
	- Např. blokace `TELNET` přístupu
5) **Omezení přístupu hostitelů ke službám sítě**:
	- Např. `FTP` přístup pouze z daného hostitele
6) **Prioritizace provozu**:
	- Např. upřednostnění `VoIP` paketů pro snížení latence jejich přenosu
##### ACL - Filtrování paketů
1) Pracuje na `L3` a `L4` modelu `ISO/OSI`
	- Filtrace `IPv4` a `IPV6` paketů
	- Filtrace `TCP` segmentů, `UDP` datagramů a `ICMP` paketů
2) **Vyhodnocuje údaje záhlaví paketů** / **segmentů** / **datagramů**
	- Router posuzuje, zda daný údaj vyhovuje příslušnému pravidlu `ACE`
3) Cisco routery podporují dva základní typy `ACL`
	1) `Standard ACLs`:
		- Umožňují filtrovat podle zdrojové `IP` adresy
	2) `Extended ACLs`
		- Umožňují filtrovat podle mnoha různých údajů
##### Princip činnosti ACLs
- `ACL` **lze přiřadit k rozhraní jako** `Inbound` nebo `Outbound`
	- Způsob přiřazení je zvolený dle druhu a účelu nasazení
- `ACL` **přiřazená k rozhraní se neaplikují na pakety routeru**
	- Pokud je router zdrojem paketů,` ACLs` tyto pakety nefitltruje
1) `Inbound ACLs`:
	- Filtrují příchozí pakety před jejich předáním na odchozí rozhraní
2) `Outbound ACLs`:
	- Filtrují odchozí pakety pro jejich předání na odchozí rozhraní
##### Wildcard Masky v ACL
- Invertovaná maska podsítě
- Význam bitových hodnot je opačný masce podsítě
	- Bit 0 vyjadřuje požadavek shody
	- Bit 1 vyjadřuje nevýznamný stav IP adresy
- `0.0.0.0 `= `host`
- `255.255.255.255` = `any`
##### Omezený počet ACLs na rozhraní
- Až dvě `ACLs` pro `IPv4`/`IPv6` provoz 
	- Jedno příchozí (`Inbound`) a jedno odchozí (`Outbound`)
##### Další kritéria umístění ACLs
1) **Hranice sítě spravované organizací**:
	- Umístění závisí na tom, jestli má organizace pod správou zdrojové či cílové hostitele, jejichž provoz potřebuje filtrovat
2) **Propustnost sítí skrze které provoz prochází**:
	- Ideální je filtrovat provoz co nejblíže jeho zdroji kvůli šetření přenosové kapacity sítě
3) **Jednoduchost konfigurace**:
	- Někdy je jednodušší určit pravidla filtrace co nejblíže cíli, ačkoliv to není optimální z hlediska využití přenosové kapacity sítě
#### 2) Standardní a rozšířené IPv4 ACL
##### Příprava na tvorbu ACLs obecně
1) **Definice požadavků** na síťový provoz
	- Zpravidla vyházejí z bezpečnostních politik organizace
2) **Formulace vlastností** `ACLs` dle sepsaných požadavků
	- Z logické topologie sítě a její adresního schématu
3) **Pro sestavení** `ACL` se doporučuje využít **textový editor**
	- Výsledné ACL lze uložit do souboru a verzovat jako zdrojový kód
4) `ACLs` se umisťují tak, aby bylo **zajištěno optimální využití** sítě
- Do `ACL` lze vložit komentáře pomocí `remark {text}`
- Přímé nasazení `ACL` ve skutečné síti může být **riskantní**, proto je vhodnější mít připravené **testovací prostředí**:
	- Při chybně definovaném ACL mohou uživatelé ztratit přístup ke službám
	- Může dojít k nechtěnému otevření portu útočníkovi
- Konfiguraci `ACL` lze zobrazit příkazy `show ip interface {interface}` a `show access-lists`
##### Standardní ACLs
- Umožňují **povolit či blokovat** `IP` pakety výhradně **na základě zdrojové** `IP` **adresy**
- Číslo `ACL` od **1 do 99 a 1300 až 1999**
- **Zpravidla umisťovány co nejblíže cíli**:
	- Např. pro filtraci provozu pro přístup do internetu volíme odchozí rozhraní hraničního routeru sítě připojené k ISP
- **Konfigurace**:
	- `access-list {number} {permit | deny} {host {source-ip} | {source-ip} {source-wildcard} | any}` pro vytvoření standardního číslovaného `ACL`
	- `ip access-list standard {name}` pro vytvoření standardního pojmenovaného `ACL`
		-`{permit | deny} {host {source-ip} | {source-ip} {source-wildcard} | any}` pro vytvoření jednotlivých pravidel (`ACE`)
	- `ip access-group {acl-number | acl-name} {in | out}` pro přiřazení `ACL` k rozhraní
##### Rozšířené (extended) ACLs
- Umožňují **povolit či blokovat** datové jednotky protokolů (`IP`, ``ICMP``, `TCP`, `UDP`...)
- Lze filtrovat podle **zdrojové či cílové** `IP` **adresy** a nebo `TCP`/`UDP` **portu** (i současně)
- Číslo `ACL` **od 100 do 199 a 2000 až 2699**
- **Zpravidla umisťovány co nejblíže zdroji**:
	- Např. při filtraci provozu určeného pro servery volíme odchozí rozhraní routeru připojené do místní sítě serverů
- **Konfigurace**:
	- `access-list {acl-number} {permit | deny} {proto} {source-ip} {source-wildcard} {oper port} ?{estabilished | log}` pro vytvoření rozšířeného číslovaného `ACL`
		- Klíčové slovo `estabilished` slouží k využití stavových služeb firewallu, umožňuje odchozí provoz z vnitřní sítě do internetu a zabrání požadavkům otevření spojení z internetu do vnitřní sítě
		- Např. `access-list 100 permit tcp any any eq www`
	- `access-list extended {acl-name}` pro vytvoření rozšířeného pojmenovaného `ACL`
		- Jednotlivá `ACE `se definují obdobným způsobem jako ve standardních ACLs, s použitím dalších parametrů
		- Např. `permit tcp any 192.168.10.0 0.0.0.255 established` nebo `permit tcp 192.168.10.0 0.0.0.255 any eq 80`
	- `ip access-group {acl-number | acl-name} {in | out}` pro přiřazení `ACL` k rozhraní
#### 3) ACL v IPv6.
##### Charakteristika IPv6 ACLs
- **Nelze jej zadat jako číslované**
- Nemají `Wildcard` masku, pracuje se zde přímo s `prefixy`
- Vyžadují explicitní povolení `ICMPv6` kvůli nezbytné funkčnosti `IPv6`
- Protokol `IPv6` obsahuje vestavěnou podporu pro `IPsec`, což umožňuje pokročilejší zabezpečení
##### Konfigurace
- `ipv6 access-list {name}` pro vytvoření `IPv6 ACL`
- `ipv6 traffic-filter {name} {in | out}` pro aplikaci `IPv6 ACL` na rozhraní
- `show ipv6 access-list` pro zobrazení a ověření `IPv6 ACL `
#### Kvízy
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUM09KSThCUzhGNkg4UEtPUk4wTzlYSFlYTC4u&route=shorturl
****https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUOTI4VTU0N0c3ME5LNEdOV0lGRzY4R1cwRS4u&route=shorturl
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUREhSOVJMWTZDTzhMSVdZOVZWNzBKWUMyOS4u&route=shorturl