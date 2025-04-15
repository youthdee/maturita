#### 1) Druhy útoků v LAN
##### Průzkumné útoky (Reconnaissance Attacks)
- **Získání informací o síti** a jejích službách:
	- Mapování topologie sítě, objevování hostitelů a jejich služeb,
	- zjišťování údajů z veřejně dostupných zdrojů, zjišťování zranitelností a aplikace exploitů hostitelských služeb
- Předcházejí vlastním přístupovým (`access`) či `DoS` útokům
##### Přístupové útoky (Access Atacks)
1) **Zneužívají zranitelností síťových služeb**:
	- Autentizační služby, webové služby
2) **Umožňují získat přístup k datům či oprávněním pro správu**:
	- Citlivé záznamy v databázi či účtu správce domény Active Directory
3) **Password Attacks**:
	- Útočník se snaží získat hesla ke klíčovým uživatelským účtům
4) **Spoofing Attacks**:
	- Útočník se pokouší vystupovat na síti jako jiné známé zařízení
5) **Trust exploitations**, **Port redirections**, **MitM attacks**, **Buffer overflow attacks**
##### Útoky typu odepření služby
1) Dočasné či trvale brání užívání služeb legitimním subjektům
2) **Zákldaní přičiny síťových útoků odepření služby**:
	- Nadměrný objem síťového provozu
	- Pakety s podvrženými údaji
3) **Distribuované odepření služby**:
	- Prováděny s využitím mnoha současně působících zdrojů
	- Koordinované útoky realizovány pomocí botnetů
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
##### Firewall
- Síťová služba, počítačový systém či jejich skupina
- Zajišťuje politiku **síťového přístupu** mezi hostiteli a sítěmi
- Zabraňuje **expozici citlivých hostitelů** v síti, prověřuje **korektnost síťové komunikace**, **blokuje** nežádoucí provoz a **centralizuje implementaci** přístupových pravidel
- Pří nesprávné konfiguraci mohou být některé služby nepřístupné, v případě centrální role bývá firewall **single point of failure**, firewall může omezovat propustnost sítě kvůli výpočetním nárokům pravidel
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
##### Nastavení minimální délky hesla
- `security passwords min-length {length}`
	- Zařízení nedovolí nastavení hesla kratšího, než je stanovená mez
