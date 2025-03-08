#### 1) Význam služby NAT v IPv4

##### Charakteristika NAT
- NAT šetří veřejné IPv4 adresy
- Umožňuje použít privátní rozsahy IP adres a připojit se k internetu
- Překládá IP Adresy odchozích paketů na veřejnou IP adresu vnějšího rozhraní routeru a naopak
- Veřejných IP adres pro překlad může být více

##### Výhody NAT a PAT
- Šetří veřejné IP adresy
- Mapování adres poskytuje flexibilitu v možnostech připojení klientů a serverů
- Konzistentní adresace ve vnitřní síti
- Skrývá IP adresy hostitelů z pohledu veřejné sítě
##### Nevýhody NAT a PAT
- Zpoždění při předávání paketů
- Ztráta oboustranné end-to-end konektivity a dohledatelnosti
- Komplikace při použití tunelovacích protokolů (PPTP, L2TP, IPSec)
- Problémy s některými aplikačními protokoly (FTP)
##### Terminologie NAT
- Inside Local Address
	- Zdrojová IP adresa z pohledu hostitele vnitřní sítě
	- Pochází z privátního rozsahu
- Inside Global Address
	- Zdrojová IP adresa z pohledu hostitele vnější (veřejné) sítě
	- Většinou se jedná o IP adresu vnějšího (veřejného) hraničního routeru
- Outside Local Address
	- Cílová adresa z pohledu hostitele vnější sítě
- Outside Global Address
	- Cílová IP adresa z pohledu hostitele vnitřní sítě
#### 2) Varianty NAT v IPv4

##### Statický NAT
- Jedna lokální IP adresa odpovídá jedné globální IP adrese
	- Přiřazení je předem definováno správcem sítě
- Užitečné pro zařízení se stabilní adresou (Webové servery)
	- Kde dynamicky přidělenou lokální IP adresu není možné přiřadit
- Umožňuje definovat přístup k zařízení mimo vnitřní síť
	- Bezpečnostní riziko při nedostatečném řízení přístupu
- Vyžaduje počet veřejných adres odpovídající počtu zařízení
	- Pro každé takové zařízení ve vnitřní síti je potřeba dedikovaná adresa

##### Dynamický NAT
- Využívá předdefinovaný adresní obor (pool)
	- Adresy jsou přiřazovány na bázi FIFO (kdo dřív přijde, ten dřív mele)
	- Adresy jsou dostupné každému hostiteli v síti
	- V případě vyčerpání musí hostitel vyčkat na uvolnění IP adresy
- Adresa je přiřazována při zahájení odchozí komunikace
	- Kde je přiřazení časově omezené, defaultně 24 hodin
- Ostatní nevyužité adresy v oboru jsou k dispozici
	- Po uplynutí lhůty se adresa vrací zpět
- Vyžaduje počet veřejných adres odpovídající počtu sezení
	- Pro každé současně probíhající sezení musí být k dispozici adresa

##### Port Address Translation (PAT)
- Více privátních adres je mapováno na jedu či více veřejných
	- Což klade nejnižší náklady na počet veřejných adres
- Používá zdrojový port pro jedinečnou identifikaci překladu
	- Což je nutné pro správné přiřazení lokální adresy paketu odpovědi
- Zajišťuje použití odlišných čísel portů pro různá sezení
	- Více privátních hostitelů může používat jedinou veřejnou adresu
- PAT se snaží zachovat číslo zdrojového portu i ve vnější síti
	- Což není možné v případě, že privátní hostitelé zvolí současně stejný port
- PAT volí alternativní zdrojový port po skupinách portů
	- Například 0 až 511, 512 až 1023, 1024 až 65535
- Pokud není další port volný, PAT zvolí další IP adresu v oboru (pool)
	- Což lze učinit pouze v případě, že je taková adresa k dispozici
- Nejčastěji používaná režim pro zajištění internetového připojení
- Způsoby identifikace paketů odpovědi v PAT:
	- V případě segmentů/datagramů protokolu TCP/UDP je to číslo zdrojového nebo cílového portu
	- V případě protokolu ICMP číslo portu neexistuje, proto se používá pro zprávy typu Echo Request/Reply hodnota pole Query ID

##### NAT64
- Překlad IPv6 adres na IPv4 adresy
- Speciální IPv6 adresy mají v sobě zakódované IPv4 adresy
- Umožňuje IPv6 sítím konzumovat služby IPv4 sítí
#### 3) Konfigurace služby NAT a PAT

##### Konfigurace statického NAT
1) Vytvoření vztahu mezi vnitřní a vnější adresou
	- Příkazem "ip nat inside source static {privátní ip adresa} {veřejná ip adresa}"
2) Určení rolí rozhraní, které se účastní překladu adres
	- Příkazem "ip nat {inside | outside}" na daném rozhraní 
- Ověřit činnost NAT lze příkazem "show ip nat translations", kde jsou statické překlady vždy uvedeny

##### Konfigurace dynamického NAT
1) Vytvoření oboru (pool) a ACL
	- Příkaz "ip nat pool {nazev oboru} {počáteční ip adresa} {koncová ip adresa} netmask {netmask}"
	- Příkaz "access-list {čislo ACL} permit {ip adresa} {wildcard maska}"
2) Sdružení oboru (pool) a ACL
	- Příkaz "ip nat inside source list {číslo ACL} pool {název oboru (pool)}"
3) Přiřazení rolí rozhraní
	- Příkaz "ip nat {inside | outside}" na daném rozhraní 
 - Ověřit činnost NAT lze příkazem "show ip nat translations", kde lze dynamické překlady smazat příkazem "clear ip nat translation"

##### Konfigurace PAT
- Pro jednu globální IP adresu:
	1) Vytvoření ACL:
		- Příkaz "access-list {čislo ACL} permit {ip adresa} {wildcard maska}"
	2) Sdružení ACL s rozhraním s klíčovým parametrem overload
		- Příkaz "ip nat inside source list {číslo ACL} interface {interface} overload"
	3) Přiřazení rolí rozhraní
		- Příkaz "ip nat {inside | outside}" na daném rozhraní 
- Pro více globálních IP adres:
	1) Vytvoření oboru (pool) a ACL
		- Příkaz "ip nat pool {nazev oboru} {počáteční ip adresa} {koncová ip adresa} netmask {netmask}"
		- Příkaz "access-list {čislo ACL} permit {ip adresa} {wildcard maska}"
	2) Sdružení oboru (pool) a ACL s klíčovým parametrem overload
		- Příkaz "ip nat inside source list {číslo ACL} pool {název oboru (pool)} overload"
	3) Přiřazení rolí rozhraní
		- Příkaz "ip nat {inside | outside}" na daném rozhraní 
 - Ověřit činnost NAT lze příkazem "show ip nat translations", kde lze vidět i porty a přehled o čerpání adres z oboru (pool)

### Kvízy
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUNTFCMU9VSjc1N1ZFUUcxSzRFOTZTSEVVSC4u&route=shorturl
