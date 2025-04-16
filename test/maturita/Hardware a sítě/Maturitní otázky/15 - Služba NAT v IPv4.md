#### 1) Význam služby NAT v IPv4
##### Charakteristika NAT
- **Šetří** veřejné `IPv4` adresy
- Umožňuje **použít privátní rozsahy** `IP` adres a **připojit se k internetu**
- Překládá `IP` Adresy **odchozích paketů** na veřejnou `IP` adresu **vnějšího rozhraní routeru** a naopak
- Výhody:
	- Mapování adres poskytuje **flexibilitu v možnostech připojení** klientů a serverů
	- **Konzistentní adresace** ve vnitřní síti
	- **Skrývá** `IP` adresy hostitelů z pohledu veřejné sítě
- Nevýhody:
	- **Zpoždění** při předávání paketů
	- **Ztráta oboustranné** `end-to-end` **konektivity** a dohledatelnosti
	- Komplikace při použití **tunelovacích protokolů** (`PPTP`, `L2TP`, `IPSec`)
	- Problémy s některými **aplikačními protokoly** (`FTP`)
##### Terminologie NAT
1) **Inside Local Address**
	- Zdrojová IP adresa z pohledu hostitele vnitřní sítě
	- Pochází z privátního rozsahu
2) **Inside Global Address**
	- Zdrojová IP adresa z pohledu hostitele vnější (veřejné) sítě
	- Většinou se jedná o IP adresu vnějšího (veřejného) hraničního routeru
3) **Outside Local Address**
	- Cílová adresa z pohledu hostitele vnější sítě
4) **Outside Global Address**
	- Cílová IP adresa z pohledu hostitele vnitřní sítě
#### 2) Varianty NAT v IPv4
##### Statický NAT
1) **Jedna lokální** `IP` adresa **odpovídá jedné globální** `IP` adrese:
	- Přiřazení je předem definováno správcem sítě
2) **Užitečné pro zařízení se stabilní adresou** (Webové servery):
	- Kde dynamicky přidělenou lokální IP adresu není možné přiřadit
3) **Umožňuje definovat přístup k zařízení mimo vnitřní síť**:
	- Bezpečnostní riziko při nedostatečném řízení přístupu
4) **Vyžaduje počet veřejných adres odpovídající počtu zařízení**:
	- Pro každé takové zařízení ve vnitřní síti je potřeba dedikovaná adresa
##### Dynamický NAT
1) **Využívá předdefinovaný adresní obor** (`pool`):
	- Adresy jsou přiřazovány na bázi "kdo dřív přijde, ten dřív mele"
	- Adresy jsou dostupné každému hostiteli v síti
	- V případě vyčerpání musí hostitel vyčkat na uvolnění IP adresy
2) **Adresa je přiřazována při zahájení odchozí komunikace**:
	- Kde je přiřazení časově omezené, defaultně 24 hodin
3) **Ostatní nevyužité adresy v oboru jsou k dispozici**:
	- Po uplynutí lhůty se adresa vrací zpět
4) **Vyžaduje počet veřejných adres odpovídající počtu sezení**:
	- Pro každé současně probíhající sezení musí být k dispozici adresa
##### Port Address Translation (PAT)
1) **Více privátních adres je mapováno na jedu či více veřejných**:
	- Což klade nejnižší náklady na počet veřejných adres
2) **Používá zdrojový port pro jedinečnou identifikaci překladu**
	- Což je nutné pro správné přiřazení lokální adresy paketu odpovědi
3) **Snaží se zachovat číslo zdrojového portu i ve vnější síti**
	- Což není možné v případě, že privátní hostitelé zvolí současně stejný port
4) **Volí alternativní zdrojový port po skupinách portů**
	- Například 0 až 511, 512 až 1023, 1024 až 65535
5) **Pokud není další port volný, zvolí další** `IP` **adresu v oboru** (`pool`):
	- Což lze učinit pouze v případě, že je taková adresa k dispozici
- Nejčastěji používaná režim pro zajištění internetového připojení
- Způsoby identifikace paketů odpovědi v PAT:
	1) V případě segmentů/datagramů protokolu TCP/UDP je to číslo zdrojového nebo cílového portu
	2) V případě protokolu ICMP číslo portu neexistuje, proto se používá pro zprávy typu Echo Request/Reply hodnota pole Query ID
##### NAT64
- Překlad `IPv6` adres na `IPv4` adresy
- Speciální `IPv6` adresy mají v sobě zakódované `IPv4` adresy
- Umožňuje `IPv6` sítím konzumovat služby `IPv4` sítí
#### 3) Konfigurace služby NAT a PAT
##### Konfigurace statického NAT
1) **Vytvoření vztahu mezi vnitřní a vnější adresou**:
	- `ip nat inside source static {privátní ip adresa} {veřejná ip adresa}`
2) **Určení rolí rozhraní, které se účastní překladu adres**:
	- `ip nat {inside | outside}` na daném rozhraní 
- Ověřit činnost NAT lze příkazem `show ip nat translations`, kde jsou statické překlady vždy uvedeny
##### Konfigurace dynamického NAT
1) **Vytvoření oboru** (`pool`) a `ACL`:
	- `ip nat pool {nazev oboru} {počáteční ip adresa} {koncová ip adresa} netmask {netmask}` pro vytvoření oboru adres
	- `access-list {čislo ACL} permit {ip adresa} {wildcard maska}` pro vytvoření `ACL`
2) **Sdružení oboru** (`pool`) a `ACL`:
	- `ip nat inside source list {číslo ACL} pool {název oboru (pool)}`
3) **Přiřazení rolí rozhraní**:
	- `ip nat {inside | outside}` na daném rozhraní 
 - Ověřit činnost NAT lze příkazem `show ip nat translations`
 - Dynamické překlady lze smazat příkazem `clear ip nat translation`
##### Konfigurace PAT
1) **Pro jednu globální** `IP` **adresu**:
	1) Vytvoření `ACL`:
		- `access-list {čislo ACL} permit {ip adresa} {wildcard maska}`
	2) Sdružení `ACL` s rozhraním s **klíčovým parametrem** `overload`:
		- `ip nat inside source list {číslo ACL} interface {interface} overload`
	3) Přiřazení rolí rozhraní:
		- `ip nat {inside | outside}` na daném rozhraní 
2) **Pro více globálních IP adres**:
	1) Vytvoření oboru (`pool`) a `ACL`
		- `ip nat pool {nazev oboru} {počáteční ip adresa} {koncová ip adresa} netmask {netmask}` pro vytvoření oboru adres
		- `access-list {čislo ACL} permit {ip adresa} {wildcard maska}` pro vytvoření `ACL`
	2) Sdružení oboru (`pool`) a` ACL` s **klíčovým parametrem** `overload`
		- `ip nat inside source list {číslo ACL} pool {název oboru (pool)} overload`
	3) Přiřazení rolí rozhraní
		- `ip nat {inside | outside}` na daném rozhraní 
 - Ověřit činnost `NAT` lze příkazem `show ip nat translations`, kde lze vidět i porty a přehled o čerpání adres z oboru (pool)
### Kvízy
https://forms.office.com/pages/responsepage.aspx?id=Iw_R_IGNR0iFNaFpxPZo2vxvCnwt1ThBn0P9MkNR0-pUNTFCMU9VSjc1N1ZFUUcxSzRFOTZTSEVVSC4u&route=shorturl
