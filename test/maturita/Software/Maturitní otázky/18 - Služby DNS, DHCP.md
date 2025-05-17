#### 1) Obecná charakteristika služeb DNS a DHCP

##### DNS
- Překlad názvů na IP adresy a obráceně
- Dva typy zón - Dopředná a zpětná
- Server naslouchá na portu `TCP/UDP:53`
##### DHCP
 - Služba, která automaticky **přiděluje klientským zařízením v síti IP adresu** a další adresní parametry (Masku podsítě, IP adresu routeru, IP adresu DNS serveru)
 - IP adresy jsou přidělovány na **určitou dobu**
 - Server DHCP spravuje soubor IP adres (**pool**)
 - Klient **posílá zprávy UDP na portu 67** a server **odpovídá na portu UDP 68**
#### 2) konfigurace a správa služby DNS v OS Windows a v UNIX-like OS
##### OS Windows
- Hiearchický, distrubuovaný, databázový systém
1) **Vrchol stromu** (**kořenová doména**, **root domain**)
	- Doména nejvyšší úrovně (top-level domains)
	- Generické TLD (.com, .edu, .net...)
	- Národní TLD (.cz, .uk, .us...)
2) **Zóna dopředného vyhledávání**
	- Obsahuje naprostou většinu zdrojových záznamů
	- Záznamy typu A, CNAME
3) **Zóna zpětného vyhledávání**
	- Definuje se pomocí formátu pro zpětné vyhledávání
	- Záznam typu PTR
- Dotazy a přenosy probíhají mezi **primárními** a **sekundárními** zónami prostřednictvím protokolů **TCP/UDP na portu 53** 
- Poskytuje i informace o správci domény a o dalších rolích
##### OS Windows - Konfigurace
- `Server Manager/Manage/Add roles and features`
- Role se konfiguruje ve `Windows Administrative Tools`
- V **DNS Manageru** se konfigurují zóny
- Okno **Dynamic update** určuje, zda-li bude moct kdokoliv upravovat záznamy dns (i nedůvěryhodná zařízení)
- Volba `Allow only secure dynamic updates` umožňuje spravovat záznamy pouze **zařízením v Active Directory**.
##### OS Windows - Windows Internet Service (WINS)
- **Zastaralá názvová služba překládající názvy NetBIOS** za účelem přesného určení sítového prvku)
- Server WINS obsahuje **databázi IP adres** a **názvů NetBIOS**, které se automaticky aktualizují 
- **Není hierarchický** jako DNS, takže je použitelný pouze v rámci firmy a pouze v operačních systémech windows
##### OS Windows - Soubor Hosts
- **Textový soubor**, který obsahuje **název uzlu v síti** a jeho **přiřazenou IP adresu**
- **Zastaralý** a neefektivní způsob (dnes používaný pouze pro řešení problému s překladem nebo testování)
- Podobnou funkci má i soubor **LMHOSTS**, který používá názvy spojené se službou WINS
##### Unix-like OS
- U malých sítí lze využít soubor `/etc/hosts` (**IP adresa, název, aliasy**)
- U velkých sítí se používá **server DNS**, který provádí dotazování v databázi názvů.
	- Nejpoužívanějším je démon `bind`
	- `bind9 bind9utils`
	- Konfigurační soubor: `named.conf` (`/etc/bind/named.conf`)
##### Unix-like OS - Vytváření zón
- Zóna **mapuje název domény s IP adresou**
- Provádí se mimo blok options:
	- V ubuntu samostatný soubor `/etc/bind/named.conf.local`
- Současně se mapuje i **reverzní zóna**, která mapuje **IP adresu s názvem domény**
- Vlastní konfigurace každé zóny se provádí do **samostatného souboru**
##### Unix-like OS - Konfigurace zón
- Konfigurace **dopředného vyhledávání** (forward zone)
	1) TTL je doba existence odpovědi, v paměti cache, po jejímž uplynutí bude nahrazena výsledkem z jiného dotazu
	2) Odkaz na doménu a emailová adresa na správce
	3) Záznam SOA (Stat of Authority), který definuje hlavní názvový server a hlavní informace týkající se zóny (čas pro obnovení, email...)
	4) Záznam NS, který udává název autoritativního serveru domény
	5) Záznam typu A (ipv4) nebo Záznam typu AAAA (ipv6)
		- Pro vlastní překlad názvu na IP adresy
	6) Záznam MX pro poštovní servery
	7) Záznam CNAME pro aliasy
##### Unix-like OS - Konfigurace zón zpětného vyhledávání (reverse zone)
- Např. `/named/0.168.192.in-addr.arpa.zone`
- Záznam **PTR** obsahuje **poslední oktet** IP adresy
- Kontrola zónových souborů příkazem `named-checkzone`
- Příkaz `host` pro zjištění ip adresy
#### 3) konfigurace a správa služby DHCP v OS Windows a v UNIX-like OS
##### OS Windows
1) **Server Manager /Manage/Add roles and feautres**
2) Konzole DHCP v "Administrative Tools/DHCP"
	- Konfigurace poolu adres v `IPV4/New Scope`
	- V okně "Add Exclustions" lze definovat rozsahy, které se nebudou přidělovat v definovaném poolu.
	- V okně **Lease Duration** se definuje doba pronájmu IP adresy.
	- Okna typu Router, Domain Name and DNS Servers, WINS Servers
3) Server DHCP se aktivuje v nabídce **Action/Authorize** a pozná se podle zelené značky u položek IPv4 a IPv6.
4) Na klientech je poté adekvátní přepnout IPv4 adresaci ze statické na DHCP.
5) Ověření funkčnosti lze ověřit v konzoli DHCP (**Scope/Address Leases**)
6) U služby DHCP je možné vytvořit **rezervaci**
	- V konzoli DHCP (IPv4/Scope/Reservations)
	- Nutná MAC adresa
##### Unix-like OS
- Nejpoužívanější je  `isc-dhcp-server`
- V souboru `/etc/default/isc-dhcp-server` nastavení rozhraní, na kterém **deamon** DHCP odpovídá na žádosti o přidělení:
	- `DHCPARGS="{rozhraní}"`
- Konfigurace v souboru `/etc/dhcp/dhcp.conf`, která obsahuje **dvě části**:
	1) **Globální parametry**
		- Konfigurační síťové parametry přiřazované klientům, definice způsobu provádění úloh
	2) **Deklarace**
		- Síťová topologie, stav klientů, nabízení adres, nasazení skupiny parametrů skupině deklarací
- Povolení provozu: `sudo ufw allow 67/udp` 
##### Unix-like OS - Konfigurace klientů DHCP
- Spočívá v **úpravě** příslušných konfiguračních souborů
- `sudo vi /etc/network/interfaces` -> `sudo systemctl restart networking`
- V ubuntu 18.04 se pro konfiguraci sítě používá program **Netplan** (`/etc/netplan`)
	- Po konfiguraci se potvrdí příkazem `sudo netplan apply`
- Alternativně nástroj `Nmtui`