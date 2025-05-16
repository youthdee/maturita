#### 1) Účel IP adresace, zápis, struktura a druhy IPv4 adres
##### Účel IP adresace
- Slouží k **jednoznačné identifikaci** síťového rozhraní v síti a umožňuje **směrování paketů** mezi různými sítěmi
- **IP adresy jsou logické** a jsou přidělovány síťovému rozhraní operačním systémem **dle konfigurace** nebo **automaticky**
- Každý uzel v lokální síti musí **mít unikátní IP adresu**, která patří do stejné IP sítě
- Každý přímo dostupný uzel v Internetu musí mít **unikátní IP veřejnou adresu**
##### IPv4 adresy
- **IPv4 adresa je 32 bitové číslo, tvořené 4 osmibitovými částmi (oktety), oddělenými tečkou**:
	- Jednotlivé oktety se zapisují dekadicky (0 až 255)
- **IPv4 adresa má dvě logické části**:
	1) Adresu sítě (vyšší bity vlevo), tuto část adresy mají všechny uzly v jedné logické síti stejnou, označována jako prefix (síťový prefix)
	2) Adresu uzlu v síti (nižší bity vpravo), touto částí adresy se jednotlivé uzly v logické síti liší
- **Hranice mezi oběma částmi IPv4 adresy je určena maskou podsítě, která je dána délkou prefixu**:
	1) Zapisuje se na konec adresy za lomítko a nabývá hodnot 0 až 32
	2) Délka prefixu určuje kolik jedničkových bitů zleva je v masce podsítě
	3) Zapisuje se ve stejném formátu jako IPv4 adresa v dekadické podobě
- Síťový rozsah (velikost sítě) je dán celkovým **počtem IP adres**, které je možné v síti vytvořit
- **První adresa** v síťovém rozsahu je vždy **adresou sítě** (**vždy končí sudým číslem**)
- **Poslední adresa** v rozsahu je vždy adresou **broadcastu** (**vždy končí lichým číslem**)
##### Druhy IPv4 Adres
1) **Unicast**:
	- Individuální adresa síťového rozhraní, pakety odeslané na unicast adresu obdrží právě jeden uzel v síti
2) **Multicast**:
	- Slouží k adresování definovaných skupin síťových rozhraní, pakety odeslané na multicast adresu jsou doručeny všem členům skupiny
	- Např. 224.0.0.1 je adresa pro všechny prvky v linkovém segmentu sítě
	- Multicast adresa není nikdy používána jako zdrojová adresa
3) **Broadcast**:
	- Pakety odeslané na broadcast adresu jsou doručeny všem uzlům v logické síti
	- V případě limitovaného broadcastu (255.255.255.255) jsou pakety doručeny všem uzlům v broadcastové doméně (všem uzlům v síťovém segmentu)
	- V případě řízeného broadcastu (poslední adresa v síťovém rozsahu) jsou pakety doručeny všem uzlům v konkrétní IP síti

##### Dělení IPv4 adres do tříd
- Některé síťové rozsahy či jednotlivé adresy jsou **rezervovány** pro použití v **privátních sítích** a některé mají **speciální význam**
- Privátní rozsahy nejsou **globálně routovatelné** v Internetu
- Přidělováním IP adres typu A a B se velmi plýtvalo s veřejnými IPv4 adresami a začaly brzy docházet
- Řešením je **NAT** (Network Address Translation) což je přechod na **classless** (systémy v Internetu ignorují pravidla pro třídy adres) pro fungování routingu v Internetu a vývoj IPv6
- Jednotlivé třídy:
	1) Třída A:
		- `0.0.0.0/8` do `127.0.0.0/8`
	2) Třída B:
		- `128.0.0.0/16` do `191.255.0.0/16`
	3) Třída C:
		- `192.0.0.0/24` do `223.255.255.0/24`
	4) Třída D:
		- `224.0.0.0` do `239.0.0.0`
	5) Třída E:
		- `240.0.0.0` do `255.0.0.0`
##### Privátní síťové rozsahy IPv4 adres
- **Rozsahy pro použití na adresaci v lokální sítích**:
	- `10.0.0.0/8`
	- `172.16.0.0/12`
	- `192.168.0.0/16`
- **Speciálním druhem IPv4 adresy je loopback**:
	- Pro tento typ adres je rezervován rozsah `127.0.0.0/8`
	- Jedná se o lokální logickou smyčku z původního zařízení zpět ke zdroji
- Pro automaticky přiřazované IPv4 adresy slouží rozsah `169.254.0.0/16` (link-state local address), známé jako APIPA (Automatic Private IP Addressing)
- Pro default route se používá adresa `0.0.0.0/0` (této adrese vyhoví všechny pakety)
#### 2) IPv6 – důvody vzniku, zápis, struktura a druhy IPv6 adres
##### Důvody vzniku IPv6 Adres
- IPv6 adresy jsou koncipovány tak, aby jich nikdy **nebyl nedostatek** (IPv4 adresy začaly brzy docházet)
- Z principu musí mít každé síťové rozhraní **veřejně směrovatelnou IPv6 adresu

##### Struktura IPv6 adres
- **IPv6 adresa má 128 bitů, je tvořena 8 slovy**:
    - Každé slovo má `16 bitů` a zapisuje se jako čtyřznakové hexadecimální číslo
    - Celkem 2^128 možných adres
- **IPv6 adresa má 3 logické části** (**zleva**):
    1. **Globální směrovací prefix**:
	    - `48 bitů` až `64 bitů`
        - Přidělován ISP
        - Podsíť se vytvoří zvětšením prefixu o velikost podsítě (maximálně `16 bitů`)
        - Udává veřejně směrovatelnou síť
        - První 3 bity určují typ adresy (např. 001 = globální unicast)
    2. **Identifikátor podsítě** (`subnet ID`):
        - `16 bitů`
        - Umožňuje vytvořit až 65 536 podsítí
        - Může být hierarchicky strukturován
        - Součást globálního směrovacího prefixu (společně tvoří prefix sítě)
    3. **Identifikátor rozhraní** (`Interface ID`):
        - `64 bitů`
        - Identifikuje konkrétní rozhraní v dané podsíti
        - Nahrazuje MAC adresu z IPv4 prostředí
        - Musí být unikátní v rámci dané podsítě
        - Umožňuje připojit 2^64 zařízení do jedné podsítě
- **Identifikátor rozhraní lze vytvořit několika způsoby:**
    1. **Manuální statické přiřazení**:
        - Administrátorem nakonfigurovaná hodnota
        - Používá se pro servery a klíčová zařízení
        - Usnadňuje správu a dokumentaci sítě
        - Obvykle se používají jednoduše zapamatovatelné hodnoty (např. ::1, ::2)
    2. **Transformování `MAC` adresy pomocí `EUI-64`**:
        - Převádí 48-bitovou MAC adresu na 64-bitový identifikátor
        - Proces:
            - Vloží `FFFE` doprostřed MAC adresy (po prvních 24 bitech)
            - Invertuje 7. bit (U/L bit) první skupiny
        - Příklad: MAC `00:1A:2B:3C:4D:5E` → IPv6 ID `021A:2BFF:FE3C:4D5E`
        - Umožňuje sledování zařízení napříč sítěmi (problém soukromí)
    3. **Vygenerování náhodnou hodnotou operačním systémem**:
        - Operační systém vytvoří náhodný identifikátor
        - Zvyšuje soukromí
        - Může se periodicky měnit (dočasné adresy)
        - Využívá kryptografické funkce pro zajištění unikátnosti
        - Standardní metoda v moderních OS (Windows, Linux, macOS)
    4. **DHCPv6**:
        - Server přiděluje celou IPv6 adresu
        - Umožňuje centrální správu a evidenci adres
        - Podobná funkce jako DHCP v IPv4 prostředí
##### Možnosti zápisu IPv6 adresy
1) **Standardní zápis** (plný):
    - Všech osm skupin po čtyřech hexadecimálních číslicích
    - Příklad: `2001:0db8:0000:0000:0000:ff00:0042:8329`
2) **Vynechání úvodních nul** (v každé skupině):
    - Úvodní nuly v každé skupině lze vynechat
    - Příklad: `2001:db8:0:0:0:ff00:42:8329`
3) **Komprese nulových bloků** (použití ::):
    - Souvislý blok nulových skupin lze nahradit pomocí dvojité dvojtečky `::`
    - Lze použít pouze jednou v adrese
    - Příklad: `2001:db8::ff00:42:8329`
4) **Kombinovaný zápis**:
    - Kombinace vynechání úvodních nul a komprese nulových bloků
    - Nejkratší možný zápis
    - Příklad: `2001:db8::ff00:42:8329`
5) **Zahrnutí prefixu sítě**:
    - Adresa s uvedením délky prefixu za lomítkem
    - Příklad: `2001:db8::/32` (prefixem je 32 bitů)
6) **Smíšená notace** (IPv4 v IPv6):
    - Poslední 32 bitů (dvě skupiny) lze zapsat v IPv4 formátu
    - Používá se pro přechodové mechanismy
    - Příklad: `2001:db8::192.168.1.1`
- **Speciální IPv6 adresy**:
	1) **Loopback adresa**:
	    - `::1` (ekvivalent 127.0.0.1 v IPv4)
	2) **Nespecifikovaná adresa**:
	    - `::` (ekvivalent 0.0.0.0 v IPv4)
	3) **Unikátní lokální adresy**:
	    - Začínají prefixem `fc00::/7` nebo `fd00::/8`
	    - Obdoba privátních adres v IPv4
	    - Příklad: `fd12:3456:789a:1::1`
	4) **Lokální linkové adresy**:
	    - Začínají prefixem `fe80::/10`
	    - Automaticky konfigurovány na rozhraních
	    - Platné pouze v rámci jednoho síťového segmentu
	    - Příklad: `fe80::1234:5678:9abc`
	5) **Multicastové adresy**:
	    - Začínají prefixem `ff00::/8`
	    - Příklad: `ff02::1` (všechny uzly na lince)
##### Druhy cílových IPv6 adres
1) **Unicast**:
	- Obdobné jako v `IPv4`
	- Reprezentováno global unicast adresou uzlu
2) **Multicast**:
	- Obdoné jako v `IPv4`
	- Umožňuje odesílání paketu více uzlům najednou (uzly mohou být kdekoliv v Internetu)
	- Definovaných skupinových adres je mnoho, některé z nich jsou uzlům nastavovány povinně
	- Skupiny mohou být veřejné i privátní
	- Broadcast v `IPv6` neexistuje, je nahrazen multicast adresou všech uzlů v lokálním linkovém segmentu sítě
3) **Anycast**:
	- Výběrová adresa, která označuje skupinu síťových zařízení
	- Při routingu jsou pakety doručeny nejbližšímu zařízení s anycast adresou (využití u služby `DNS`)
	- Nemají vlastní síťový rozsah
##### IPv6 adresy na síťových rozhraních
- Každé síťové rozhraní v IPv6 má přiřazeno **několik** (často povinných) `IPv6` adres, některé si generuje automaticky:
	1) **Global Unicast Adresa**:
		- Veřejně routovatelná adresa, zajišťuje jednoznačnou identifikaci v Internetu
		- Jedná se o Globální Prefix s identifikátorem rozhraní
	2) **Link Local Adresa**:
		- Automaticky generovaná povinná adresa
		- Používaná pro komunikaci v lokální síti, nelze ji routovat přes Internet
		- Používá rozsah `FE80::/10`, ke kterému je přidán identifikátor rozhraní
	3) **Povinné Multicast Adresy**:
		- Používají společný prefix `FF00::/8`
		- `FF02::1` je multicast adresa všech uzlů v lokálním linkovém segmentu sítě (nahrazuje broadcast)
		- `FF01::1` je multicast adresa pro vyzývaný uzel (ND)
	4) `IPv6` **Loopback adresa**:
		- Adresa ::1/128
	5) `IPv6` Default gateway využívá adresu ::/0
#### 3) Subnetace, VLSM
##### Subnetace v IPv4
- Subnetace se používá pro potřebu **rozdělení** větší logické sítě na několik **menších logických sítí**
- Dva způsoby, jak rozdělit síť na subnety:
	1) **FLSM** (Fixed-Length Subnet Masking):
		- Každý subnet má stejnou masku a tím pádem je v každém subnetu stejný počet hostitelů
	2) **VLSM** (Variable-Length Subnet Masking):
		- Efektivnější způsob využití přiděleného síťového rozsahu
		- Maska podsítě se určí dle požadovaného počtu IP adres v subnetu (omezeno mocninou čísla 2)
- Při subnetaci je nutné dodržet **nepřekrývání**:
	- Což znamená, že IP adresa uzlu v jednom subnetu se nesmí vyskytovat v jiném subnetu
##### VLSM
1) Napsat prefix a dekadickou podobu masky jednotlivých subnetů
2) Napsat skutečný počet adresovatelných zařízení v subnetu
3) Napsat počet subnetů
4) Napsat adresu každého subnetu
##### Postup VLSM
1) Subnety seřadit podle velikosti a oddělovat od největšího subnetu
2) K subnetu najít nejbližší mocninou čísla 2 k počtu požadovaných zařízení a zjistit tím prefix (32 - mocnina dvou)
3) První adresou je adresa sítě a poslední adresou je adresa broadcastu
