#### 1) Druhy útoků v LAN
##### Průzkumné útoky (Reconnaissance Attacks)
- **Získání informací o síti a jejích službách:**
    - Mapování topologie sítě, objevování hostitelů a jejich služeb
    - Zjišťování údajů z veřejně dostupných zdrojů (OSINT - Open Source Intelligence)
    - Zjišťování zranitelností a aplikace exploitů hostitelských služeb
- Předcházejí vlastním přístupovým (`access`) či `DoS` útokům
- **Nejčastější nástroje a techniky**:
    - `Port scanning` : 
	    - Zjišťování otevřených portů (Nmap, Zenmap)
    - `Ping sweeping` :
	    - Identifikace aktivních zařízení v síti
    - `DNS enumeration` : 
	    - Získávání informací o doménách a serverech
    - `Banner grabbing` : 
	    - Zjišťování verzí služeb a operačních systémů
    - `Social engineering` : 
	    - Získávání informací od zaměstnanců organizace
##### Přístupové útoky (Access Attacks)
1. **Zneužívají zranitelností síťových služeb**:
    - Autentizační služby, webové služby, databázové služby
    - Neaktualizované systémy s veřejně známými zranitelnostmi
    - Zero-day exploity (využití dosud neopravených zranitelností)
2. **Umožňují získat přístup k datům či oprávněním pro správu**:
    - Citlivé záznamy v databázi či účtu správce domény Active Directory
    - Přístup k síťovým úložištím a dokumentům
    - Eskalace oprávnění v systému
3. **Password Attacks**:
    - `Brute force` : 
	    - Systematické zkoušení všech možných kombinací hesel
    - `Dictionary attack` : 
	    - Zkoušení slov ze slovníku jako možná hesla
    - `Rainbow tables` :
	    - Předpočítané hash hodnoty hesel pro rychlejší prolomení
    - `Credential stuffing` : 
	    - Zkoušení uniklých přihlašovacích údajů z jiných služeb
    - `Keylogging` : 
	    - Zachycení stisknutých kláves uživatele s cílem získat heslo
4. **Spoofing Attacks**:
    - `IP spoofing` :
		 - Podvržení zdrojové IP adresy v paketu
    - `MAC spoofing` :
	    - Změna MAC adresy zařízení pro obejití filtrů
    - `ARP spoofing` :
	    - Manipulace s ARP tabulkami pro přesměrování provozu
    - `DNS spoofing` :
	    - Manipulace DNS odpovědí pro přesměrování na falešné stránky
    - `Email spoofing` :
	    - Falšování odesílatele e-mailových zpráv
5. **Trust exploitations**:
    - Zneužití důvěryhodných vztahů mezi systémy
    - Využití toho, že některé systémy implicitně důvěřují jiným systémům
    - Příklad: zneužití důvěry mezi servery v doméně
6. **Port redirections**:
    - Přesměrování síťového provozu na neoprávněné porty nebo služby
    - Vytvoření tunelu pro přenos dat skrz firewall
    - Obcházení bezpečnostních kontrol pomocí přesměrování portů
7. **MitM attacks** (Man-in-the-Middle):
    - Útočník se umístí mezi dvě komunikující strany
    - Může odposlouchávat, upravovat nebo blokovat komunikaci
    - Realizace pomocí:
	    - `ARP spoofing` (podvržení `MAC` adresy)
	    - `DNS spoofing` (podvržení `DNS` záznamu)
	    - `SSL stripping` (odstranění šífrování `HTTPS`)
8. **Buffer overflow attacks**:
    - Útok na aplikaci zasláním většího množství dat, než očekává
    - Přepsání paměti programu může vést k vykonání škodlivého kódu
##### Útoky typu odepření služby (DoS - Denial of Service)
1. Dočasně či trvale brání užívání služeb legitimním subjektům:
    - **Cíle útoků**: webové servery, DNS servery, e-mailové servery, síťová infrastruktura
    - **Dopady**: finanční ztráty, poškození reputace, nespokojenost zákazníků
2. **Základní příčiny síťových útoků odepření služby**:
    - **Nadměrný objem síťového provozu**:
        - **Volumetrické útoky** - zahlcení sítě velkým množstvím dat
        - **Amplifikační útoky** - zneužití protokolů k zesílení útoku (DNS, NTP)
    - **Pakety s podvrženými údaji**:
        - **TCP SYN flood** - zahlcení serveru polovičními TCP spojeními
        - **ICMP flood** - zahlcení ping požadavky
        - **UDP flood** - zahlcení UDP pakety
3. **Distribuované odepření služby** (DDoS - Distributed Denial of Service):
    - Prováděny s využitím mnoha současně působících zdrojů
    - Koordinované útoky realizovány pomocí botnetů (sítě kompromitovaných počítačů)
    - **Typy DDoS útoků**:
        - **Layer 3-4 útoky** - zaměřené na síťovou a transportní vrstvu (SYN flood, UDP flood)
        - **Layer 7 útoky** - zaměřené na aplikační vrstvu (HTTP flood, Slowloris)
    - **Známé DDoS nástroje**: LOIC, HOIC, Mirai botnet, Memcached amplification
#### 2) Druhy útoků na L2, Možnosti předcházení útokům na LAN
##### Druhy útoků na L2
1) **ARP Spoofing** (Poisoning):
    - Pro IP adresu je užita `MAC` adresa útočníka, původní adresát je z doručení rámce vyloučen.
    - Lze řešit statickými záznamy v `ARP` tabulce, softwarem pro detekci `ARP` útoku nebo bezpečnostním nastavením operačního systému.
2) **MAC Spoofing**:
    - Útočník padělá `MAC` adresu jiného zařízení, aby obešel `MAC` filtraci nebo získal neoprávněný přístup do sítě.
    - Lze řešit funkcí `Port Security` na switchi nebo filtrováním na úrovni `NAC` (Network Access Control).
3) **VLAN Hopping**:
    - Útočník obchází segmentaci sítě a získává neoprávněný přístup do jiné `VLAN`.
    - Možné metody:
        - **Switch Spoofing**:
	        - Útočník se vydává za trunkový port.
        - **Double Tagging**:
	        - Rámec obsahuje dvě VLAN značky, což umožní jeho přesměrování.
    - Lze řešit omezením `trunk` portů a správným nastavením VLAN tagování.
4) **STP Attack** (Root Bridge Manipulation):
    - Útočník podvrhne `BPDU` zprávy a stane se root bridge, čímž přesměruje provoz přes svůj uzel.
    - Lze řešit aktivací BPDU Guard, Root Guard a správným nastavením `STP` priority.
5) **DHCP Starvation Attack**:
    - Útočník odešle velké množství falešných `DHCP DISCOVER` zpráv s různými `MAC` adresami, aby vyčerpal dostupné IP adresy.
    - Lze řešit aktivací `DHCP` Snooping a omezením počtu `MAC` adres na portu (Port Security).
6) **DHCP Spoofing**:
    - Útočník provozuje falešný `DHCP` server a přiděluje klientům podvržené IP adresy, bránu nebo DNS.
    - Lze řešit aktivací `DHCP` Snooping, který filtruje neautorizované `DHCP` odpovědi.
7) **CAM Table Overflow Attack**:
    - Útočník zaplaví switch obrovským množstvím `MAC` adres, což způsobí přetečení `CAM` tabulky a přepnutí switche do hub režimu (všechny rámce jsou rozesílány všem).
    - Lze řešit Port Security a omezením dynamických `MAC` adres na portu.
8) **BPDU Spoofing**:
    - Útočník falšuje `BPDU` zprávy, aby zmanipuloval `STP` topologii a způsobil přerušení provozu.
    - Lze řešit `BPDU` Guard, Root Guard a deaktivací `STP` na přístupových portech.
##### Možnosti předcházení útokům na LAN
- **Omezení možnosti fyzického připojení k LAN**:
	1) Standard `IEEE 802.1x`
	2) Autentizace na `WLAN`
- **Filtrace** `TCP/UDP` **portů na hostitelích**:
	- Platí jak pro servery, tak pro stanice
- Umístění serverů veřejných služeb do **demilitarizované zóny**
- Nastavení systému `IDS/IPS` nebo **Cisco Web Security Appliance** (WSA) nebo **Cisco E-mail Security Appliance** (ESA)
	1) **Intrusion Detection/Prevention System**:
		- Systém vyhodnocující příchozí pakety na základě definovaných politik
		- V případě útoku IPS zasílá zprávu do správcovské konzole, paket zahodí a zabrání probíhajícímu útoku
		- Jedná se o systémy umožňující detekci či zabránění útokům, sledují a vyhodnocují síťový provoz, identifikují vzory či signatury dle průběžně aktualizovaných pravidel a umožňují rychle reagovat na právě probíhající útoky
		- Lze nasadit na Cisco IOS Router, Hardwarové zařízení specificky určené jako IDS/IPS senzor nebo modul instalovaný v ASA (Adaptive Security Appliance)
	2) **Cisco Web Security Appliance**:
		- Firewall předá podezřelou stránku WSA, která vyhodnotí a určí, zda se jedná o známou stránku v blacklistu
		- V případě shody požadavek zablokuje a uživateli vrátí chybovou zprávu
	3) **Cisco Email Security Appliance**:
		- Firewall předá veškeré přijaté zprávy ESA, která identifikuje podezřelou zprávu, událost zaznamená a zprávu odstraní
- **Sběr a vyhodnocování žurnálových záznamů**:
	- Auditní logy, systémové logy, aplikační logy
- **Zálohování nejen dat, ale i celých systémů**:
	- Snadné vytváření a obnova obrazů virtuálních počítačů
- **Pravidelná bezpečnostní školení uživatelů LAN**:
	- Obvykle největší bezpečnostní hrozbou v LAN je neznalý uživatel
##### Ochrana proti průzkumným útokům:
- Implementace IDS/IPS systémů (Intrusion Detection/Prevention System)
- Skrytí síťové topologie a omezení veřejně dostupných informací
- Monitoring neobvyklého síťového provozu (skenování portů)
- Správná konfigurace firewallů pro blokování nežádoucích připojení
##### Ochrana proti přístupovým útokům:
- **Silná autentizace**:
	- Vícefaktorová autentizace (2FA/MFA)
	- Komplexní hesla a jejich pravidelná obměna
	- Biometrické metody ověřování
- **Správa zranitelností**:
	- Pravidelné aktualizace a patche systémů
	- Penetrační testování a bezpečnostní audity
- **Síťová segmentace**:
	- Oddělení kritických systémů do vlastních VLAN
	- Řízení přístupu mezi segmenty pomocí ACL
    - **Ochrana proti spoofingu**:
        - IP Source Guard - ochrana proti IP spoofingu
        - DHCP Snooping - ochrana proti falešným DHCP serverům
        - Dynamic ARP Inspection - ochrana proti ARP spoofingu
        - 802.1X - autentizace zařízení před připojením do sítě
##### Ochrana proti DoS a DDoS útokům:
- **Redundance systémů**:
	- Geografická distribuce serverů
	- Load balancing pro rozložení zátěže
- **Rate limiting a filtering**:
	- Omezení počtu připojení z jedné IP adresy
	- Filtrování známých škodlivých IP adres
- **Anti-DDoS služby**:
	- Cloudflare, AWS Shield, Akamai
	- Scrubbing centers pro čištění provozu
- **Border Gateway Protocol (BGP) failover**:
	- Přesměrování provozu v případě útoku
##### Úrovně zabezpečení počítače
1) **Fyzická bezpečnost**:
	- Zajištění chráněného fyzického přístupu
	- Např. Uzamčení místnosti s počítačem, uzamčení počítačové skříně, nasazení elektronického zámku a přístupového systému, kamerový systém...
2) **Bezpečnost operačního systému**:
	- Zajištění bezpečného provozu a užívání operačního systému
	- Autentizace (Prokázání totožnosti uživatele)
	- Autorizace (Řízení přístupu k prostředkům uživatele)
	- Např. Pravidlo nejmenší nutné úrovně přístupu, dostatečně silná hesla, pravidelné aktualizace operačního systému, nasazení firewallu a antivirového systému
3) **Bezpečnost aplikací**:
	- Zajištění bezpečného provozu a užívání aplikací
	- Zranitelnost aplikací díky chybám vývojářů
	- Např. Pravidlo nejmenší nutné úrovně přístupu, dostatečně silná hesla, pravidelné aktualizace aplikací, omezení síťového přístupu
#### 3) Zabezpečení přístupu na switche a routery
##### Druhy přístupu k Cisco síťovým prvkům
1) **Konzolový přístup** (port `CONSOLE`):
	- Správa pomocí rozhraní RS-232 nebo USB
2) **Pomocný přístup** (port `AUXILIARY`):
	- Správa přes modemové připojení
3) **Virtuální přístup** (linky `VTY`):
	- Správa pomocí `TELNET` a `SSH` spojení
##### Zabezpečení konzolového přístupu
- `line console 0`
- `login`
- `password {password}`
##### Zabezpečení virtuálních linek
- `line vty 0 15`
- `login`
- `password {password}`
##### Zabezpečení privilegovaného režimu
1) `Enable Password {password}`
	- Heslo uložené reverzibilním kódováním
	- Méně bezpečné
2) `Enable Secret {Password}`
	- Využívá hashované (MD5) varianty hesla"
	- Nahrazuje heslo z předchozího režimu
##### Zabezpečení uložených hesel
- `service password-encryption`
	- Zašifruje v zařízení hesla uložená v původní textové formě
##### Nastavení doby nečinnosti sezení (session)
- `exec-timeout 5 20` v `line console 0`
	- Po uplynutí zadaného času nečinnosti se sezení (session) automaticky odhlásí
