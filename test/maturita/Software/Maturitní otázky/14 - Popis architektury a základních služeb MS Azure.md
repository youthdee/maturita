#### 1) Hlavní komponenty architektury Azure

##### Microsoft Azure
- Sada cloudových služeb pro vytváření, správu a nasazování aplikací
- Neustále se inovující prostředky, podporu řady jazyků a frameworků, nástroje a služby pro hybridní cloud on-premise i čistě cloudová řešení, zabezpečení a řešení pro zajištění souladu s předpisy.
- Pro využívání MS Azure je třeba předplatné, v rámci jednoho účtu lze mít více předplatných
- V předplatém lze vytvářet skupiny prostředků a v nich pak jednotlivé prostředky
##### Fyzická infrastruktura Azure
- Datacentra (Budovy s hw, napájením, chlazením, síťovou infrastrukturou)
- Oblasti (oblast obsahující jedno nebo více datacenter, které jsou blízko sebe a jsou propojeny do sítě s nízkou latencí)
- Zóny dostupnosti (fyzicky oddělená datacentra v některých oblastech, každá zóna je tvořena jedním nebo více datacentrem, které jsou navzájem propojeny vysokorychlostními a privátnímí sítěmi, s vlastním napájením, síťovou infrastrukturou atd., zajištění redundance dat a služeb pro případ výpadku) 
- Páry oblastí (spárovaní oblastí se vzdáleností minimálně 300 mil, např West US - East US)
- Výsostné oblati "Sovereign Regions" (instance Azure oddělené od hlavní instance Azure z důvodu zákonných nebo dodržení předpisů, např Goverement, Čína)

##### Infrastruktura pro správu
- Prostředky (základní komponenta Azure, např. virtuální počítač)
- Skupiny prostředků (belze je vnořovat do jiných skupin prostředků, některé prostředky lze přesouvat, každý prostředek může být v právě jedné skupině prostředků)
- Předplatná Azure (Každý účet musí mít minimálně jedno předplatné, svázáno s účtem Azure, více předplatných se používá pro zjednodušení účtování za služby a rozdělení na více úrovní)
- Skupiny pro správu (Základní prvek hierarchické struktury pro uspořádání prostředků, např hiearchická struktura pro aplikování různých zásad, zajištění přístupu uživatelům k vícero předplatných)
#### 2) Výpočetní služby Azure

##### Azure Virtual Machines
- vytváření a provozování virtuálních počítaů v cloudu
- řešení IaaS
- úplná kontrola nad operačním systémem
- spouštění vlastního softwaru
- vlatstní konfigurace pro hosting
- lze vytvořit samostaně, nebo pomocí ARM šablony
##### Azure Virtual Machines - Škálovací sada (Virtual Machines Scale Set)
- skupina několika virtuálních počítačů se stejnou konfigurací vytvořena za účelem vyrovnání zátěže (Load Balancing)
- používají se při řešení výpočetních úloh, big data a kontejnerů
##### Azure Virtual Machines - Skupiny Dostupnosti
- zajišťují dostupnost v případě výpadku způsobeného instalací aktualizací či výpadkem sítě nebo napájení
- virtuální počítače se seskupují do:
- Update Domain
	- virtuální počítače, které lze najednou restartovat např. kvůli aktualizaci
- Fault Domain
	- virtuální počítače, které mají stejné napájení a jsou zapojené ke stejnému switchi.

##### Azure Virtual Machines - Možnosti využití
- Testování a vývoj
- Provoz aplikací v cloudu
- Rozšíření datacentra do cloudu
- Obnovení z havárie
- Přesun fyzického serveru do cloudu
- Možnost výběru HW

##### Azure Virtual Machines - Azure Virtual Desktop
- verze OS Windows běžící v cloudu, která je přístupná odkudkoliv z libovolného zařízení
- Windows 10 nebo Windows 11 multi-session (současné přihlášení více uživatelů na jeden virtuální počítač)

##### Azure Containers
- Azure Container Instances v podobě PaaS, které umožňuje načíst kontejnery a pak je spustit.
- Kontejnery se používají v řešeních využívajících architekturu mikroslužeb, kde jsou jednotlivá řešení rozdělena do menších a na sobě nezávislých celků (např. frontend, backend, uložiště)

##### Azure Functions
- Bezserverové řešení řízené událostmi
- Naprogramovaná funkce, která se spustí pouze při výskytu příslušné události
- Automatická škálovatelnost a platí se pouze za čas CPU potřebný pro běh funkce
- Dělií se na:
	- Stateless "Bezestavové" (při každé reakci na událost se spouští znovu nezávisle na předchozím stavu)
	- Stateful "Stavové" (při reakci se funkci předává kontext obsahující aktivitu z předchozího spuštění)
##### Azure App Service
- vytvoření a hostování webových aplikací, úloh běžíích na pozadí či REST API
- Zákazník nespravuje infrastrukturu, ale zaměřuje se na tvorbu a správu aplikací (např. webová aplikace, API aplikace, WebJobs, Mobilní aplikace)
- Automatické škálování a vysoká dostupnost
- Podpora OS Windows, Linux
- Automatizované nasazení z GitHubu, Azure DevOps...
#### 3) Síťové služby Azure

##### Virtuální sítě v Azure
- Zajišťují vzájemnou komunikaci mezi prostředky, uživateli na internetu, klientskými počítači v on-premise
- Víceméně se jedná o rozšíření stávající on-premise sítě o prostředky zajišťující propojení s ostatními prostředky Azure
- Klíčové funkce virtuálních sítí:
	- izolace a segmentace
	- komunikace na internetu
	- komunikace mezi prostředky Azure
	- komunikace s prostředky on-premise, k jejichž propojení lze využít:
		- Připojení point-to-site
		- Připojení site-to-site
		- Připojení ExpressRoute
	- Směrování síťového provozu
	- Filtrování síťového provozu
	- Propojení virtuálních sítí
- Podpora koncových bodů s veřejnou i privátní IP adresou

##### Virtuální sítě v Azure - Azure VPN Gateway
- Brána virtuální sítě, umístěná ve vyhrazené podsíti, zajišťující šifrované tunelované připojení:
	- Datacenter k virtuálním sítím (site-to-site)
	- Jednotlivých zařízení k virtuálním sítím (point-to-site)
	- Virtuálních sítí k jiným virtuálním sítím (network-to-network)
- Dělí se na:
	- Policy-based VPN gateway (pro každý tunel se zadáva IP adresa)
	- Route-based 
		- Tunely IPSec mají buď podobu síťového rozhraní, nebo virtuálního tunelového rozhraní
		- příslušné rozhraní pro odesílání paketů se definuje statickým nebo dynamickým routingem
		- Přednostně používaný u on-premise řešenich
		- Např propojení virtuálních sítí, point-to-site připojení, multisite připojení, koexistence s Azure ExpressRoute
- Možnosti zvýšení odolnosti:
	- active/standby instance (dvě instance VPN Gateway)
	- active/active instance (dvě instance VPN Gateway)
	- ExpressRoute failover (VPN Gateway slouží jako záloha)
	- Zone-redundant gateways (nasazení bran VPN a ExpressRoute v oblastech s podporou zón dostupnostiee)

##### Virtuální sítě v Azure - Azure ExpressRoute
- Umožňuje rozšíření on-premise sítí (poboček, datacenter...) do cloudu pomocí privátního připojení v podobě okruhu ExpressRoute
- Nevyužívá veřejný internet
- Spolehlivější, rychlejší, stabilní latence a vyšší bezpečnost

##### Virtuální sítě v Azure - Azure DNS
- Nabízí překlad názvů prostřednictvím infrastruktury Azure
- Výhody:
	- Spolehlivost a výkon
	- Bezpečnost
	- Spravování záznamů jak pro služby Azure, tak pro externí prostředky
	- Součástí portálu Azure, Azure CLI, Azure Powershell, RestApi a SDK
	- Podpora privátních domén
	- Podpora záznamů typu Alias
#### 4) Služby úložiště Azure Storage
##### Účet uložiště
- Jedinečný jmenný prostor pro data Azure Storage
- Data jsou přístupná odkudkoliv pomocí HTTP nebo HTTPS
- Data jsou zabezpečena a mají vysokou dostupnost, odolnost a škálovatelnost
- Různé typy účtu uložiště
- Koncový bod pro účet uložiště je dán kombinací názvu účtu a koncového bodu služby Azure Storage

##### Možnosti redundance u úložiště Azure
- Vždy je ukládáno několik kopií dat za účelem ochrany před ztrátou
- k dispozici je několik řešení redundance (vždy je potřeba rozhodnout mezi výši nákladů a úrovni dostupnosti)

##### Redundance v primární oblasti
- Data existují ve třech kopiích
- Locally redundant storage (LRS)
	- tři kopie v jednom datacentru nacházejícím se v primární oblasti
	- Nejlevnější řešení s ochranou pouze proti selhání serverového racku a disků
- Zone redundant sotrage (ZRS)
	- Provádí se synchroní replikace dat přes tři zóny dostupnosti primární oblasti
	- Data jsou dostupná i po výpadku zóny

##### Redundance v sekundární oblasti
- Pro zajištění vysoké odolnosti dat (kopírování do sekundární oblasti, která je vzdálena několik set kilometrů od primární oblasti)
- Ochrana před ztrátou dat kvůli havárii v primární oblasti
- Azure Storage nabízí v sekundární oblasti tyto dva způsoby replikace:
	- Geo redundant storage (GRS)
		- Tři kopie dat v jednom místě v primární oblasti (LRS) a poté se asynchronně vytvoří kopie do jednoho umístění v sekundární oblasti (LRS)
	- Geo zone redundant storage (GZRS)
		- Data se kopírují do tří zón dostupnosti v primární oblasti (ZRS) a následně se kopírují do druhé oblasti (LRS)
		- Nejvyšší odolnost, dostupnost a výkon
- Ve výchozím nastavení lze k datům v sekundární oblasti přistupovat až po selhání první oblasti
- Je možné povolení přístupu pro čtění pomocí RA-GRS (read access geo-redundant storage) nebo RA-GZRS (read access geo zone redundant storage)

##### Služby úložiště Azure
- Azure Blobs (škálovatelné úložiště pro binární data a text s podporou pro big data)
- Azure Files (sdílení souborů pro on-premise i cloudová řešení)
- Azure Queues (úložiště pro zprávy zasílané při komunikaci mezi komponentami aplikací)
- Azure Disks (svzaky úložišť využívající blok určené pro virtuální počítače Azure)
- Výhody: 
	- odolnost vůči chybám
	- vysoká dostupnost
	- bezpečnost
	- škálovatelnost
	- zajištěná správa hardwaru pro ukládání dat
	- přístup odkudkoliv přes HTTP, HTTPS, podpora jazyků a skriptů pro Azure Powershell nebo Azure CLI
	- podpora přístupu přes portál Azure nebo průzkumník uložišť Azure

##### Úložiště typu blob (Azure Blob Storage)
- vhodné pro ukládnání velkého množství binárních nebo textových dat
- nestrukturované úložiště
- Přístup k datům lze realizovat přes HTTP, HTTPS nebo REST API, Azure Powershell, Azure CLI
- Úrovně přístupu se dělí na základě frekvence přístupu a intervalu jejich změny na: 
	- Hot access (data, k nimž se přistupuje velmi často)
	- Cool access (data, k nimž se přistupuje velmi málo)
	- Archieve access (data, k nimž se přistupuje velmi málo, nejnižší cena za uložení, ale nevyšší cena za přístup)

##### Azure Files
- Sdílení souborů v cloudu s možností přístupu přes protokoly SMB nebo NFS
- Sdílené prostředky lze připojit k zařízením v cloudu i on-premise a to v OS Windows, Linux i macOS
- Pomocí Azure File Sync lze sdílené prostředky uložit do cahce serverů Windows Server
- Plně spravované řešení s podporou skriptování v PowerSehllu nebo Azure CLI
- vysoce odolné proti výpadkům

##### Azure Queue Storage
- Úložiště pro ukládání nezpracovaných zpráv pro asycnrhonní zpracování
- Pro ukládní velkého množství zpráv o max velikosti 64 KB
- Často se využívá v kombinaci s jinyými výpočetními službami, které se aktivují při přijetí zprávy (např. Azure Functions)
##### Disk Storage (Azure managed disks)
- Bloková úložiště určená pro práci s virtuálními počítači Azure
- běžné disky s posílenou odolností a dostupností

##### Možnosti migrace dat
- možnost migrace infrastruktury, aplikací i dat v reálném čase (Azue Migrate) i asynchroní migrace (Azure Data Box)
- Azure Migrate
	- migrace on-premise do cloudu
	- jednotná platforma a nástroje pro spuštění, běh a seldování migrace
- Azure Data Box
	- Fyzický přesun velkých objemů dat
	- Asynchornní

##### Možnosti přesunu souborů
- Nástroje pro přesun jednotlivých souborů nebo malého množství souborů
- AzCopy:
	- příkazový řádek pro kopírování blobů nebo souborů
- Azure Storage Exporer
	- grafické rozhraní pro správu soubroů a blobů
- Azure File Sync
	- centralizace sdílených souborů v Azure Files určený pro zachování kompability s OS Windows Server
	- vyvtáří miniaturní síť CDN (Content Delivery Network) 
	- Automaticky synchronizuje soubory Windows Serveru se soubory Azure
