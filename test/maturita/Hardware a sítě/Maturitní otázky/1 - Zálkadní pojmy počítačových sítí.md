#### 1) Účel počítačových sítí 

##### Hlavní účel
- Propojení zařízení za účelem efektivní komunikace, sdílení dat, využívání společných zdrojů a zabezpečeného přístupu k informacím

##### Některé možnosti využití počítačových sítí
- Komunikace
	- Email (SMTP, POP3, IMAP)
	- Zprávy a videohovory (VoIP, SIP, RTP)
	- Webová komunikace (HTTP a HTTPS)
- Sdílení dat a prostředků
	- Sdílení souborů (FTP, SFTP)
	- Přístup k síťovým diskům (SMB, NFS)
	- Tiskárny v síti (IPP)
- Přístup k Internetu
	- Přenos dat (TCP/IP)
	- Adresování (IPv4, IPv6)
	- Překlad doménových jmen a naopak (DNS)
- Zabezpečení a správa
	- Ověření uživatelů (Kerberos, Radius)
	- Zabezpečené připojení (SSL/TLS, VPN)
	- Firewall (IPTables)
	- Automatické přidělení adresních parametrů (DHCP)
#### 2) Typy sítí
##### Podle logické struktury
- Client-Server:
	- Jeden vyhrazený server poskytuje službu klientům
	- Centralizovaný model fungování
	- Výpadek serveru znamená nedostupnost služby
- Peer-to-Peer
	- Každé koncové zařízení může poskytovat službu ostatním zařízením a také využívat služeb ostatních zařízení v síti
	- Decentralizovaný model fungování
- Hybridní síť
	- Model kombinující sítě typu Client-Server a Peer-to-Peer

##### Podle Fyzického média
- Metalická kabeláž
	- UTP, STP, koaxiální kabel
- Optické vlákno
- Bezdrátové sítě
	- Wi-Fi, Bluetooth
- Satelitní síť

##### Podle rozsahu
- LAN (Local Area Network)
- MAN (Metropolitan Area Network)
- WAN (Wide Area Network)
#### 3) Prvky používané v počítačových sítích

##### Router (Směrovač)
- Propojuje přímo nesousedící počítačové sítě
- Zajišťuje směrování paketů mezi různými sítěmi podle jejich IP adresy
- Rozhoduje o nejlepší cestě pro přenos dat
- Pracuje na L3 (paket)
##### Switch (Přepínač)
- Spojuje zařízení v rámci jedné lokální sítě
- Umožňuje efektivní přepínání rámců na základě MAC adresy
- Pracuje na L2

##### Access Point
- Poskytuje bezdrátový přístup k síti (Wi-Fi)
- Spojuje bezdrátové účastníky s drátovou sítí
- Pracuje na L2 (může mít funkcionalitu na vyšších vrstvách pro správu)

##### Modem
- Připojuje domácnost nebo firmu k internetu prostřednictvím telefonní linky, kabelu nebo optického vlákna
- Moduluje a demoduluje signály pro přenos dat
- Pracuje na L1

##### Bridge (Most)
- Spojuje dvě nebo více LAN do jedné větší sítě
- Provádí filtrace rámců mezi sítěmi na základě MAC adres
- Pomáhá rozdělit síť na menší segmenty a zlepšit výkon
- Pracuje na vrstvě L2

##### Hub (Rozbočovač)
- Spojuje zařízení v síti, ale na rozdíl od switche (přepínače) posílá všechny signály na všechny porty, což může vést k přetížení sítě
- Slouží k rozdělení síťového signálu na více zařízení, ale bez filtrování ani směrování
- Pracuje na L1

##### Firewall
- Ochrana sítě před neautorizovaným přístupem a hrozbami z vnější sítě
- Filtruje síťový provoz na základě předem definovaných pravidel
- Softwarový nebo hardwarový firewall
- Pracuje na vrstvách L3 a L4

##### Proxy Server
- Zprostředkovává přístup mezi klientem a serverem, obvykle pro zvýšení bezpečnosti a efektivity
- Maskuje skutečnou IP adresu klienta a zrychluje připojení prostřednictvím cache
- Pracuje na L7

##### IDS/IPS (Intrusion Detection/Prevention System)
- Detekce a prevence neautorizovaných pokusů o přístup nebo útoků na síť
- IDS detekuje útoky a IPS je schopný aktivně zablokovat podezřelý provoz v reálném čase
- Pracuje na vrstvách L3 až L7
#### 4) Trendy v oblasti počítačových sítí
##### Novější trendy
- Automatizace a programovatelnost sítí
	- Moderní sítě směřují k vyšší automatizaci a možnosti programovatelnosti, což zjednodušuje jejich správu a zvyšuje efektivitu provozu
- Přesun správy sítí do cloudového prostředí
	- Správa sítí se stále více přesouvá do cloudu, což umožňuje snadnější údržbu a správu odkudkoli
- Implementace a mikrosegmentace pro zvýšení bezpečnosti
	- Mikrosegmentace v podnikových sítích zajišťuje lepší zabezpečení provozu i v případě napadení
- Rozšíření Wi-Fi sítí do 6 GHz pásma
	- Očekává se schválení použití 6 GHz pásma v Evropě, což přinese vyšší rychlost a kapacitu Wi-Fi sítí
- Integrace nových bezpečnostních řešení
	- Společnost Cisco představila novou řadu firewallů a řešení Cisco XDR pro pokročilou detekci a reakci na hrozby
- Optimalizace stávajících Wi-Fi sítí
	- Důraz je kladen na optimalizaci existujících Wi-Fi sítí, aby poskytovaly kvalitní a spolehlivé připojení

##### Starší trendy
- QoS (Quality of Service)
	- Technologie pro prioritizaci síťového provozu
	- Zajišťuje nižší latenci pro VoIP hovory, streamování a videokonference
	- Nasazována hlavně u IPv4 sítí a Cisco routerů
- VPN (Virtual Private Network)
	- Technologie šifrovaného tunelování přes veřejný Internet
	- Protokoly jako IPSec, PPTP, L2TP
	- FIremní VPN se začaly masově využívat pro vzdálený přístup k firemním sítím
- IPSec (Internet Protocol Security)
	- Standard pro šifrování IP provozu na L3 vrstvě
	- Používá se pro například pro VPN tunely a ochranu mezi routery a firewally
	- Zajišťuje integritu dat, šifrování a autentizaci
- VLAN (Virtual Local Area Network)
	- Logické rozdělení sítě na více virtuálních sítí
	- Zajišťuje oddělení provozu mezi sítěmi (např. administrativa, sales, management)
- Wi-Fi (IEE 802.11)
	- Masivní rozšíření bezdrátových sítí
- PoE (Power over Ethernet, IEEE 802.3.af)
	- Přenos napájení po ethernetovém kabelu
	- Umožňuje napájet IP kamery, VoIP telefony nebo APs bez nutnosti dalšího napájení
- IPv6
	- Reakce na nedostatek IPv4 adres
	- Nasazeno pro datová centra a páteřní sítě
- NAT (Network Address Translation)
	- Řešení pro překlad veřejné IP adresy na privátní adresy
	- Umožňuje více zařízením vystupovat na internetu pod jednou veřejnou IP adresou
- Škálovatelný síťový model
	- S rostoucí firmou je potřeba zajistit škálování počítačové sítě
	- Zajišťuje redundaci, odolnost, hierarchii a snadnou škálovatelnost