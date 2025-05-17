#### 1) Význam služby DHCP
##### DHCP (Dynamic Host Configuration Protocol)
- Konfiguruje síťová rozhraní uzlů v místní síti, odbourává ruční nastavení IP adresy, masky
- Vznik 1993, nástupce protokolu **BOOTP**
- Přiděluje údaje nutné pro síťovou komunikaci (IP adresa, maska podsítě, výchozí brána, název DNS domény, IP adresy DNS serverů...)
> Využívá broadcastů na protokolu `UDP` 
> DHCP server naslouchá na portu `67`
> DHCP klient odesílá z portu `68`
##### Bezpečnostní aspekty:
- Zranitelnost vůči falešným DHCP serverům (DHCP spoofing)
- Možnost přetížení serveru (DHCP starvation)
- Kontrola podle MAC adres (MAC filtering)
- DHCP snooping na přepínačích (ochrana proti neautorizovaným DHCP serverům)
##### Další vlastnosti protokolu DHCP
- Klient obdrží konfiguraci jen na **určitou dobu**, poté musí požádat o znovupřidělení nastavení (nebo uvolnit zprávou `DHCPRELEASE`)
- DHCP agenty pro obsluhu více sítí, **zprostředkují komunikaci** mezi serverem a klienty
- Použitelný nejen pro pracovní stanice, je přímo nezbytný pro mobilní a bezdrátová zařízení
- Lze nakonfigurovat i servery a aktivní prvky sítě, většinou ale rezervací dle `MAC` adres

#### 2) Průběh komunikace v DHCPv4
##### Princip činnosti DHCPv4
1) **Discover - Klient vyzve server o přidělení IP adresy** (`DHCPDISCOVER`)
    - Vysílá se jako broadcast
    - Obsahuje MAC adresu klienta
    - Může obsahovat požadavek na specifickou IP adresu (pokud ji klient v minulosti používal)
2) **Offer - Server zvolí vhodnou adresu a nabídne ji** (`DHCPOFFER`)
    - Obsahuje veškeré adresní parametry nakonfigurované v tomto serveru
    - Server si označí adresu jako "nabídnutou"
3) **Request - Klient z nabídky vybere a požádá o ni** (`DHCPREQUEST`)
    - Opět se vysílá jako broadcast (aby ostatní DHCP servery věděly, že klient zvolil jiný server)
    - Obsahuje identifikaci zvoleného serveru (Server Identifier) a požadovanou adresu
4) **Acknowledge - Server výběr zhodnotí a případně jej akceptuje** (`DHCPACK` / `DHCPNAK`)
    - `DHCPACK` - potvrzení pronájmu IP adresy a dalších parametrů
    - `DHCPNAK` - zamítnutí požadavku (např. pokud byla adresa mezitím přidělena jinému klientovi)
##### Obnova pronájmu (Renewal)
- Klient se snaží obnovit pronájem po vypršení 50% doby pronájmu (T1)
- Pokud server neodpovídá, klient se pokouší o obnovu po vypršení 87.5% doby pronájmu (T2) u libovolného DHCP serveru
- Zasílá pouze `DHCPREQUEST` přímo serveru, který adresu přidělil
- Pokud klient nedostane žádnou odpověď, musí po vypršení pronájmu zahájit celý proces znovu
##### Uvolnění adresy - `DHCPRELEASE`
- Klient může adresu uvolnit před vypršením pronájmu zprávou `DHCPRELEASE`
- Server vrátí adresu zpět do poolu dostupných adres
##### DHCP relay agent (DHCP helper)**:
- Umožňuje obsluhu více sítí z jednoho centrálního DHCP serveru
- Zprostředkovává komunikaci mezi serverem a klienty v různých podsítích
- Přeposílá DHCP pakety mezi sítěmi, kde by jinak broadcast zprávy neprocházely
- Implementováno na směrovačích nebo dedikovaných serverech
#### 3) Průběh komunikace v DHCPv6

##### Vlastnosti protokolu DHCPv6
- Konfiguruje síťová rozhraní `IPv6` uzlů v místní síti (obdoba mechanismu pro IPv4)
- Doplňuje funkčnost mechanismu `SLAAC`:
	- Umožňuje nastavení dalších údajů (DNS servery, NTP...)
- Klient používá `UDP port 546`:
	- Zasílá na multicast adresu `ALL_DHCP_Relay_AGENTS_and_Servers`
- Server používá `UDP port 547` a link-local adresy:
	- Zasílá na link-local adresy klienta 
##### Způsoby nastavení IPv6 rozhraní
1. **Link-local adresa**:
    - Nastavení IID pomocí EUI-64 nebo náhodně
    - Statická konfigurace správcem
2. **Global Unicast adresa**, výchozí brána:
    - Nastavení pomocí NDP (IID s EUI-64 nebo náhodně)
    - Nastavení pomocí DHCPv6 (stavové DHCP)
    - Statická konfigurace správcem
3. **Adresy DNS serverů, NTP serverů**:
    - Statická konfigurace správcem
    - Nastavení pomocí NDP (ne všechna zařízení podporují)
    - Nastavení pomocí DHCPv6 (bezstavové DHCP)
##### Stateful DHCPv6 (Stavový režim)
1. Klient vyzve server k přidělení IP adresy (`Solicit`)
    - Vysílá se na multicast adresu FF02::1:2
    - Obsahuje DUID klienta a požadované parametry
2. Server zvolí vhodné IP adresy a nabídne je (`Advertise`)
    - Obsahuje DUID serveru
    - Obsahuje nabízené adresy a parametry
    - Může být více serverů s různými nabídkami
3. Klient z nabídky vybere IP adresu a požádá o ni (`Request`)
    - Obsahuje vybranou nabídku a server
    - Informuje ostatní servery o výběru
4. Server výběr zhodnotí a případně jej akceptuje (`Reply`)
    - Potvrzení přidělení adresy a parametrů
    - Obsahuje dobu pronájmu
##### Stateless DHCPv6 (Bezstavový režim)
1. Klient požádá o konfigurační údaje (`Information-Request`)
    - Používá se, když klient má adresu z SLAAC
    - Žádá pouze o doplňkové parametry (DNS, NTP...)
2. Server poskytne konfigurační údaje klientovi (`Reply`)
    - Neobsahuje IP adresy (ty jsou z SLAAC)
    - Pouze doplňkové parametry, které SLAAC neposkytuje
##### DHCP Unique Identifier (DUID)
- Jedinečný **identifikátor** DHCP klienta a serveru
- DHCP server dle něj vybírá konfiguraci k nabídce
- DHCP klient dle něj určuje identitu DHCP serveru
##### SLAAC (Stateless Address Autoconfiguration)
- Hostitel si vygeneruje a nastaví `IPv6 GUA` sám dle zaslaného prefixu
- Prefix GUA adresy udává router ve zprávě `RA` protokolu `NDP`
- Adresa se vytvoří spojením prefixu (64 bitů) a identifikátoru rozhraní (64 bitů)
##### Možné kombinace se SLAAC:
1. **Kombinace se Stateless (Bezstavovým) DHCPv6**:
    - SLAAC poskytuje adresu a výchozí bránu
    - Hostitel navíc kontaktuje DHCP server pro společné konfigurační údaje (doménový suffix, DNS servery...)
    - V RA zprávě: M=0, O=1
2. **Kombinace se Stateful (Stavovým) DHCPv6**:
    - Hostitel kontaktuje DHCP server k získání IPv6 GUA včetně dalších údajů
    - SLAAC se nepoužívá pro adresaci
    - V RA zprávě: M=1
3. **SLAAC + DHCPv6 - Součinnost routeru a hostitele**:
    - Router Solicitation (RS) - zasílá hostitel pro zjištění přítomnosti routeru
    - Router Advertisement (RA) - zasílá router s informacemi o síti a příznaky konfigurace
    - DHCPv6 Solicit - zprávu zasílá hostitel na základě údajů obsažených ve zprávě Router Advertisement
##### Příznaky v Router Advertisement (RA):
- **M-flag** (Managed Address Configuration Flag):
    - M=1: Použít Stateful DHCPv6 pro adresy-
    - M=0: Použít SLAAC pro adresy
- **O-flag** (Other Configuration Flag):
    - O=1: Použít DHCPv6 pro další parametry
    - O=0: Nepoužívat DHCPv6 pro další parametry
##### Proces konfigurace IPv6 adresy pomocí SLAAC:
1. Vytvoření link-local adresy a ověření její jedinečnosti (DAD)
2. Odeslání Router Solicitation zprávy
3. Přijetí Router Advertisement s prefixem sítě
4. Vytvoření globální IPv6 adresy (prefix + identifikátor rozhraní)
5. Ověření jedinečnosti globální adresy pomocí DAD
6. Případné získání dalších parametrů pomocí Stateless DHCPv6