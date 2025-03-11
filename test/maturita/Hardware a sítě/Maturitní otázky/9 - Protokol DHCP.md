#### 1) Význam služby DHCP

##### DHCP (Dynamic Host Configuration Protocol)
- Konfiguruje síťová rozhraní uzlů v místní síti, odbourává ruční nastavení IP adresy, masky
- Vznik 1993, nástupce protokolu BOOTP
- Přiděluje údaje nutné pro síťovou komunikaci (IP adresa, maska podsítě, výchozí brána, název DNS domény, IP adresy DNS serverů...)
- Využívá broadcastů na protokolu UDP:
	- DHCP klient odesílá z portu 68
	- DHCP server naslouchá na portu 67
##### Další vlastnosti protokolu DHCP
- Klient obdrží konfiguraci jen na určitou dobu, poté musí požádat o znovupřidělení nastavení (nebo uvolnit zprávou DHCPRELEASE)
- DHCP agenty pro obsluhu více sítí, zprostředkují komunikaci mezi serverem a klienty
- Použitelný nejen pro pracovní stanice, je přímo nezbytný pro mobilní a bezdrátová zařízení
- Lze nakonfigurovat i servery a aktivní prvky sítě, většinou rezervací dle MAC adres

##### Vlastnosti protokolu DHCPv6
- Konfiguruje síťová rozhraní IPv6 uzlů v místní síti (obdoba mechanismu pro IPv4)
- Doplňuje funkčnost mechanismu SLAAC:
	- Umožňuje nastavení dalších údajů (DNS servery, NTP...)
- Klient používá UDP port 546 (zasílá na multicast adresu ALL_DHCP_Relay_AGENTS_and_Servers)
- Server používá UDP port 547 a link-local adresy (zasílá na link-local adresy klienta) 
#### 2) Průběh komunikace v DHCPv4

##### Princip činnosti DHCPv4
1) Klient vyzve server o přidělení IP adresy (DHCPDISCOVER)
2) Server zvolí vhodnou adresu a nabídne ji (DHCPOFFER)
3) Klient z nabídky vybere a požádá o ni (DHCPREQUEST)
4) Server výběr zhodnotí a případně jej akceptuje (DHCPACK / DHCPNAK)
#### 3) Průběh komunikace v DHCPv6

##### Způsoby nastavení IPv6 rozhraní
- Link-local adresa
	- Nastavení IID pomocí EUI-64 nebo náhodně
	- Statická konfigurace správcem
- Global Unicast adresa, výchozí brána
	- Nastavení pomocí NDP (IID s EUI-64 nebo obráceně)
	- Nastavení pomocí DHCPv6 (stavové DHCP)
	- Statická konfigurace správcem
- Adresy DNS serverů, NTP serverů...
	- Statická konfigurace správcem
	- Nastavení pomocí NDP (ne všechna zařízení podporují)
	- Nastavení pomocí DHCPv6 (bezestavové DHCP)
##### Stateful DHCPv6
1) Klient vyzve server k přidělení IP adresy (Solicit)
2) Server zvolí vhodné IP adresy a nabídne je (Advertise)
3) Klient z nabídky vybere IP adresu a požádá o ni (Request)
4) Server výběr zhodnotí a případně jej akceptuje (Reply)

##### Stateless DHCPv6
1) Klient požádá o konfigurační údaje (Information-Request)
2) Server poskytne konfigurační údaje klientovy (Reply)

##### DHCP Unique Identifier
- Jedinečný identifikátor DHCP klienta a serveru
- DHCP server dle něj vybírá konfiguraci k nabídce
- DHCP klient dle něj určuje identitu DHCP serveru
- Čtyři druhy:
	- Link-layer address plus time (DUID-LLT)
	- Vendor-assigned unique ID based on Enterprise Number (DUID-EN)
	- Link-layer address (DUID-LL)
	- UUID-based DUID (DUID-UUID)

##### SLAAC (Stateless Address Autoconfiguration)
- Hostitel si vygeneruje a nastaví IPv6 GUA sám dle zaslaného prefixu
- Prefix GUA adresy udává router ve zprávě RA protokolu NDP
- Kombinace se Stateless (Bezestavovým) DHCPv6:
	- SLAAC + hostitel navíc kontaktuje DHCP server pro společné konfigurační údaje (doménový suffix, DNS servery...)
- Kombinace se Stateful (Stavovým) DHCPv6: 
	- Hostitel kontaktuje DHCP server k získání IPv6 GUA včetně dalších údajů
- SLAAC + DHCPv6 - Součinnost routeru a hostitele:
	- Router Solicitation (zasílá hostitel)
	- Router Advertisement (zasílá router)
	- DHCPv6 Solicit:
		- Zprávu zasílá hostitel na základě údajů obsažených ve zprávě Router Advertisement
		- Může být buď Stateful (Stavový) nebo Stateless (Bezestavový) režim DHCPv6