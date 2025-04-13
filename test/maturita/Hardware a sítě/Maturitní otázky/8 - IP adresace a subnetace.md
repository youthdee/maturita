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

##### Možnosti zápisu IPv6 adresy

##### Struktura IPv6 adres
- IPv6 adresa má 128 bitů, je tvořena 8 slovy:
	- Každé slovo má 16 bitů a zapisuje se jako čtyřznakové hexadecimální číslo
	- Jednotlivá slova jsou oddělena dvojtečkami
- IPv6 adresa má 3 logické části (zleva):
	- Globální routovací prefix (global prefix):
		- Přidělován ISP
		- 48 bitů až 64 bitů
		- Podsíť se vytvoří zvětšením prefixu o velikost podsítě (maximálně 16 bitů)
	- Identifikátor podsítě (subnet ID)
		- 16 bitů
	- Identifikátor rozhraní (Interface ID)
		- 64 bitů
- Hodnota prefixu od ISP udává veřejně routovatelnou síť
- Identifikátor rozhraní ma velikost 64 bitů a zde ho vytvořit několika způsoby:
	- Manuální statické přiřazení
	- Transformování MAC adresy pomocí EUI-64
	- Vygenerování operačním systémem náhodnou hodnotou

##### Důvody vzniku IPv6 Adres
- IPv6 adresy jsou koncipovány tak, aby jich nikdy nebyl nedostatek (IPv4 adresy začaly brzy docházet)
- Z principu musí mít každé síťové rozhraní veřejně routovatelnou IPv6 adresu

##### Druhy cílových IPv6 adres
- Unicast:
	- Obdobné jako v IPv4
	- Reprezentováno global unicast adresou uzlu
- Multicast:
	- Obdoné jako v IPv4
	- Umožňuje odesílání paketu více uzlům najednou (uzly mohou být kdekoliv v Internetu)
	- Definovaných skupinových adres je mnoho, některé z nich jsou uzlům nastavovány povinně
	- Skupiny mohou být veřejné i privátní
	- Broadcast v IPv6 neexistuje, je nahrazen multicast adresou všech uzlů v lokálním linkovém segmentu sítě
- Anycast:
	- Výběrová adresa, která označuje skupinu síťových zařízení
	- Při routingu jsou pakety doručeny nejbližšímu zařízení s anycast adresou (využití u služby DNS)
	- Nemají vlastní síťový rozsah

##### IPv6 adresy na síťových rozhraních
- Každé síťové rozhraní v IPv6 má přiřazeno několik (často povinných) IPv6 adres, některé si generuje automaticky:
	- Global Unicast Adresa:
		- Veřejně routovatelná adresa, zajišťuje jednoznačnou identifikaci v Internetu
		- Jedná se o Globální Prefix s identifikátorem rozhraní
	- Link Local Adresa:
		- Automaticky generovaná povinná adresa
		- Používaná pro komunikaci v lokální síti, nelze ji routovat přes Internet
		- Používá rozsah FE80::/10, ke kterému je přidán identifikátor rozhraní
	- Povinné Multicast Adresy:
		- Používají společný prefix FF00::/8
		- FF02::1 je multicast adresa všech uzlů v lokálním linkovém segmentu sítě (nahrazuje broadcast)
		- FF01::1 je multicast adresa pro vyzývaný uzel (ND)
		- FF02::1:ffxx:xxxx je multicast adresa, kde poslední 3 bajty jsou převzaty z konce MAC adresy síťového rozhraní
	- IPv6 Loopback adresa
		- Adresa ::1/128
	- IPv6 Default gateway využívá adresu ::/0
#### 3) Subnetace, VLSM
##### Subnetace v IPv4
- Subnetace se používá pro potřebu rozdělení větší logické sítě na několik menších logických sítí
- Dva způsoby, jak rozdělit síť na subnety:
	- FLSM (Fixed-Length Subnet Masking):
		- Každý subnet má stejnou masku a tím pádem je v každém subnetu stejný počet hostitelů
	- VLSM (Variable-Length Subnet Masking):
		- Efektivnější způsob využití přiděleného síťového rozsahu
		- Maska podsítě se určí dle požadovaného počtu IP adres v subnetu (omezeno mocninou čísla 2)
- Při subnetaci je nutné dodržet nepřekrývání, což znamená, že IP adresa uzlu v jednom subnetu se nesmí vyskytovat v jiném subnetu

##### VLSM
1) Napsat prefix a dekadickou podobu masky jednotlivých subnetů
2) Napsat skutečný počet adresovatelných zařízení v subnetu
3) Napsat počet subnetů
4) Napsat adresu každého subnetu

##### Postup VLSM
- Subnety seřadit podle velikosti a oddělovat od největšího subnetu
- K subnetu najít nejbližší mocninou čísla 2 k počtu požadovaných zařízení a zjistit tím prefix (32 - mocnina dvou)
- První adresou je adresa sítě a poslední adresou je adresa broadcastu
