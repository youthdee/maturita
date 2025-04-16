#### 1) Sítě WAN – definice, účel, topologie a vlastnosti
##### WAN - Definice a účel, typy, vlastnosti
- **Rozlehlá komunikační síť** pokrývající zpravidla **širokou geografickou oblast**, která je potřebná pro připojení ke službám dostupným za hranicemi běžné `LAN`
	1) **Propojují** vzdálené uživatele, sítě a lokality
	2) **Ve vlastnictví různých poskytovatelů**
	3) Za použití se **účtují poplatky** poskytovatelům
	4) Nabízí rychlosti v širokém rozsahu s ohledem na výši platby
1) **Privátní** `WAN`
	- Spojení, které je vyhrazeno pro jediného zákazníka
	- Nabízí garantovanou službu, konzistentní propustnost a bezpečnost
2) **Veřejná** `WAN`
	- Poskytována `ISP` nebo jiným poskytovatelem
	- Realizována prostřednictvím sítě Internet
	- Úroveň poskytované služby je proměnlivá a nelze ji zpravidla zaručit
	- Zabezpečení komunikace (šifrování, autenticita) je na zákazníkovi
##### Topologie sítí WAN
- Fyzická topologie **popisuje přenosovou infrastrukturu** sítě
	- Zpravidla **komplexní a skrytá pro uživatele** (zákazníka)
- Sítě `WAN` se popisují zpravidla pomocí logické topologie:
	1) `Point-to-Point`:
		- Vzájemné propojení dvou lokalit
		- Služba na vrstvě `L2` skrze síť poskytovatele
		- Z pohledu zákazníka transparentní
		- Představuje nákladné řešení, pokud je potřeba velký počet takových spojů
	2) `Hub-and-Spoke`:
		- Jediné rozhraní na centrálním routeru (`hub`), které je sdíleno všemi spoji (`spokes`)
		- Routery spojů (`spokes`) jsou propojeny skrze centrální router (`hub`) pomocí virtuálních okruhů
		- Routery spojů (`spokes`) mohou navzájem komunikovat výhradně skrze centrální router (`hub`)
		- Centrální router (`hub`) představuje `single point of failure`
	3) `Dual-homed`:
		- Síťová redundance a `load balancing`
		- Nákladnější oproti `single-homed` topologiím (vyžaduje více hardware a služeb `WAN` poskytovatele)
		- Obtížnější na implementaci, protože vyžadují náročnější konfiguraci síťových prvků
	4) `Fully Meshed`:
		- Používá více virtuálních okruhů (spojů) k propojení všech lokalit
		- Nejvyšší míra odolnosti proti selhání
	5) `Partially Meshed`:
		- Používá více virtuálních okruhů (spojů) k přímému propojení vybraných lokalit
		- Méně nákladné na implementaci
- Rozsáhlé sítě `WAN` tyto topologie obvykle kombinují
##### Způsoby připojení k síti WAN
1) `Single-Carrier` připojení:
	- Připojení k jedinému poskytovateli
	- Vlastní připojení i služby poskytovatele představují single point of failure
	- Levnější řešení
	- Nezajišťuje vždy dostupnost připojení
2) `Dual-Carrier` připojení:
	- Připojení ke dvěma nezávislým poskytovatelům
	- Vlastní připojení i služby poskytovatele jsou redundantní
	- Nákladnější řešení
	- Zlepšení propustnosti připojení a load-balancing
#### 2) Základní pojmy a zařízení používaná v sítích WAN
##### DTE (Data Terminal Equipment)
- Připojuje síť `LAN` zákazníka k zařízení `DCE`
##### DCE (Data Communication Equipment)
- Zajišťuje komunikaci s `WAN` infrastrukturou poskytovatele
##### CPE (Customer Premises Equipment)
- Zařízení `DTE` a `DCE` umístěná na hranici sítě `LAN`
##### POP (Point-Of-Presence)
- Bod, kde se zákazník připojuje k síti poskytovatele
##### Demarkační bod
- Fyzické umístění v budově nebo komplexu, které odděluje `CPE` od vybavení poskytovatele
##### Pronajaté linky (leased lines)
- Poskytovány telekomunikačními operátory jako **pevné připojení**
- Dostupné v různých **pevně daných přenosových rychlostech**
- **Garantována kvalita** služby díky vyhrazené přenosové kapacitě
##### Možnosti připojení k internetu
1) Pevné (wired) připojení
	- Metalické či optické kabeláže
	- Stabilní rychlost přenosu
	- Nízká latence a vyšší náklady
	- `XDSL`, `Cable`, `Optical Fiber`
2) Bezdrátové (wireless) připojení
	- Komunikace rádiovými vlnami
	- Omezení dosahu, vliv rušení
	- Méně nákladné, možnosti závislé na lokalitě
	- `Municipal Wi-Fi`, `Celluar`, `Satellite Internet`, `WiMAX`
3) Možnosti připojení k Internetu:
	1) `Sinlge-homed`:
		- Jeden `ISP` a spoj, nejnižší náklady, bez redundance
	2) `Dual-homed`:
		- jeden `ISP`, dva spoje, redundance a `load-balancing`, závislost na jednom `ISP`
	3) `Multihomed`:
		- Dva různí `ISP`s, vyšší spolehlivost a možnost `load-balancing`u, vyšší náklady
	4) `Dual-multihomed`:
		- Více `ISP`s a více spojů, nejvyšší spolehlivost a redundance, nejdražší řešení
#### 3) Přehled a základní charakteristika technologií sítí WAN
##### Připojení využívající přepínání okruhů
1) **Public Service Telephone Network** (`PSTN`)
	- Veřejná telefonní síť
	- Možnost připojení pomocí klasického modemu až do `56 kb/s`
	- Zastaralá technologie, která je již nahrazena modernějšími technologiemi
2) **Integrated Services Digital Network** (`ISDN`)
	- Digitální připojení místní smyčky
	- Rychlost přenosu od `45kb/s` do `2048 Mb/s`
	- S ohledem na rozmach `DSL` a omezenou rychlost je tato technologie na ústupu
##### Připojení využívající přepínání paketů
1) **Frame Relay**
	- Jednoduchá technologie pracující na `L2`
	- Umožňuje propojit podnikové sítě `LAN` ve vzdálených lokalitách
	- Podporuje více samostatných `PVC` okruhů, rychlosti až `4 Mb/s`
	- Nahrazována moderními technologiemi - `Metro Ethernet`
2) **Asynchronous Transfer Mode** (ATM):
	- Přenos hlasových, video a datových služeb se zajištěním `QoS`
	- Navržena s použitím buňkové architektury (buňka = `54 bajtů`)
	- Na rozdíl od `Frame Relay` je méně efektivní při přenosu velkých objemů dat
	- Nahrazována moderními technologiemi - `Metro Ethernet`
##### Ethernet ve WAN sítích
- Novější `Ethernet` standardy nabízejí **podporu optických vláken**
- Poskytovatelé nabízejí `WAN` připojení **s použitím optiky** jako:
	1) **Metropolitan Ethernet** (`Metro Ethernet`)
	2) **Ethernet over MPLS**
	3) **Virtual Private LAN Service**
##### Multiprotocol Label Switching (MPLS)
- **Výkonná směrovací technologie** nezávislá na druhu přístupu
- Podporuje různé metody přístupu:
	- `Ethernet`, `DSL`, kabel, Frame Relay
- Podporuje zapouzdření `IPv4` a `IPv6`
- K dispozici služby `QoS`, redundance spojů a `VPN`
- Příklad nasazení `MPLS` s použitím `Label-switched Routers`:
	1) **Customer Edge** (CE) **Router**:
		- Hraniční router zákazníka)
	2) **Provider Edge** (PE) **Router**:
		- Označí paket labelem
	3) **Internal Provider** (P) **Router**:
		- Směruje paket dle labelu
##### Digital Subscriber Line (DSL)
- **Vysokorychlostní**, trvalé připojení
- Užívá přenosu v rozprostřeném **frekvenčním spektru**
- **Symetrické** (`SDSL`) a **Asymetrické** (`ADSL`,` ADSL2+`, `VDSL`, `VDSL2`)
- **Populární možnost připojení**, lze využít existujícího vedení
- Využívá **telefonního účastnického vedení** (**místní smyčky**)
	- `DSL` modem moduluje či demoduluje signál na přípojce a převádí na nebo z data
	- `DSLAM `(DSL Access Multiplexer) jako protějšek umístěn v ústředně
##### Kabelové připojení
- Užívá **koaxiálního kabelu** jako média účastnické přípojky
- Standard `DOCSIS` (**Data over Cable Service Interface Specification**)
- Hybridní sítě (`HFC`) užívají optické spoje pro připojení k `CMTS` (**Cable odem Termination System**)
##### Optické připojení
- **Fiber to the Home** (`FTTH`):
	- Optika zavedena až do bytu
- **Fiber to the Building** (`FTTB`)
	- Optika zavedena jen do budovy
- **Fiber to the Node/Neighborhood** (`FTTN`)
	- Optika zavedena do uzlu poblíž účastnických obydlí
- Řešení `FTTx` nabízí **nejvyšší dosažitelné rychlosti připojení**
##### Vyhrazené širokopásmové připojení (broadband)
- Díky `DWDM` technologií **významná úspora počtu optických vláken**
- Volná vlákna lze pronajímat dalším subjektům (`dark fiber`)
##### Bezdrátové připojení
1) `Municipal Wi-Fi`:
	- Městské bezdrátové připojení, nízká cena
2) `Celluar`:
	- Datové připojení mobilních zařízení skrze buňkovou síť mobilního operátora
	- Technologie `3G`/`4G`/`5G` a `LTE`
3) `Satellite Internet`:
	- Užíván na venkově či v odlehlých oblastech, kde není k dispozici jiný druh připojení
	- Účastník se připojuje prostřednictvím mikrovlnné směrové antény k družicím
4) `WiMAX`:
	- Vysokorychlostní bezdrátové připojení se širokým pokrytím geografických oblastí