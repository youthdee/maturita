#### 1) Hlavní komponenty architektury Azure
##### Microsoft Azure
- Sada cloudových služeb pro **vytváření**, **správu** a **nasazování aplikací**
- Neustále se **inovující** **prostředky**, podporu řady jazyků a frameworků, nástroje a služby pro hybridní cloud a  on-premise i čistě cloudová řešení, zabezpečení a řešení pro zajištění souladu s předpisy.
- Pro **využívání** MS Azure je třeba **předplatné**, v rámci jednoho účtu **lze mít více předplatných**
	- V předplatném lze vytvářet skupiny prostředků a v nich pak jednotlivé prostředky
##### Fyzická infrastruktura Azure
1) **Datacentra**:
	- Budovy s hw, napájením, chlazením, síťovou infrastrukturou
2) **Oblasti**: 
	- Oblast obsahující jedno nebo více datacenter, které jsou blízko sebe a jsou propojeny do sítě s nízkou latencí
3) **Zóny dostupnosti**: 
	- Fyzicky oddělená datacentra v některých oblastech
	- Každá zóna je tvořena jedním nebo více datacentrem, které jsou navzájem propojeny vysokorychlostními a privátními sítěmi, s vlastním napájením, síťovou infrastrukturou
	- Zajištění redundance dat a služeb pro případ výpadku) 
4) **Páry oblastí**:
	- Spárovaní oblastí se vzdáleností minimálně 300 mil 
	- West US - East US
5) **Výsostné oblastí**:
	- Instance Azure oddělené od hlavní instance Azure z důvodu zákonných nebo dodržení předpisů
	- Goverement, Čína
##### Infrastruktura pro správu
1) **Prostředky**
	- Základní komponenta Azure
	- Virtuální počítač
2) **Skupiny prostředků**
	- Nelze je vnořovat do jiných skupin prostředků, některé prostředky lze přesouvat
	- Každý prostředek může být v právě jedné skupině prostředků
3) **Předplatná Azure** 
	- Každý účet musí mít minimálně jedno předplatné, svázáno s účtem Azure, více předplatných se používá pro zjednodušení účtování za služby a rozdělení na více úrovní
4) **Skupiny pro správu**:
	- Základní prvek hierarchické struktury pro uspořádání prostředků 
	- Hierarchická struktura pro aplikování různých zásad, zajištění přístupu uživatelům k vícero předplatných)
#### 2) Výpočetní služby Azure
##### Azure Virtual Machines
- **Vytváření** a **provozování** virtuálních počítačů v cloudu
- Řešení IaaS
- **Úplná kontrola** nad operačním systémem
- **Vlastní konfigurace** pro hosting
- Lze vytvořit samostatně, nebo pomocí ARM šablony
##### Azure Virtual Machines - Škálovací sada (Virtual Machines Scale Set)
- **Skupina několika virtuálních počítačů** se **stejnou konfigurací** vytvořena za účelem **vyrovnání zátěže** (**Load Balancing**)
- Používají se při řešení výpočetních úloh, big data a kontejnerů
##### Azure Virtual Machines - Skupiny Dostupnosti
- Zajišťují **dostupnost** v případě **výpadku** způsobeného **instalací aktualizací** či **výpadkem sítě** nebo **napájení**
- **Virtuální počítače se seskupují do**:
	1) Update Domain
		- Virtuální počítače, které lze najednou restartovat např. kvůli aktualizaci
	2) Fault Domain
		- Virtuální počítače, které mají stejné napájení a jsou zapojené ke stejnému switchi.
##### Azure Virtual Machines - Možnosti využití
- Testování a vývoj
- Provoz aplikací v cloudu
- Rozšíření datacentra do cloudu
- Obnovení z havárie
- Přesun fyzického serveru do cloudu
- Možnost výběru HW
##### Azure Virtual Machines - Azure Virtual Desktop
- Verze **OS Windows běžící v cloudu**, která je přístupná **odkudkoliv** z **libovolného zařízení**
- **Windows 10** nebo **Windows 11 multi-session** (současné přihlášení více uživatelů na jeden virtuální počítač)
##### Azure Containers
- **Azure Container Instances** v podobě **PaaS,** které umožňuje **načíst kontejnery** a pak je **spustit**.
- Kontejnery se **používají v řešeních využívajících architekturu mikroslužeb**, kde jsou **jednotlivá řešení rozdělena do menších a na sobě nezávislých celků** (např. frontend, backend, uložiště)
##### Azure Functions
- **Bezserverové** řešení řízené událostmi**
- Naprogramovaná funkce, která se spustí pouze při **výskytu příslušné události**
- **Automatická škálovatelnost** a platí se pouze za čas CPU potřebný pro běh funkce
- Dělií se na:
	- **Stateless**:
		- Při každé reakci na událost se spouští znovu nezávisle na předchozím stavu
	- **Stateful**: 
		- Při reakci se funkci předává kontext obsahující aktivitu z předchozího spuštění)
##### Azure App Service
- **Vytvoření** a **hostování webových aplikací**, úloh běžíích na pozadí či REST API
- **Zákazník nespravuje infrastrukturu**, ale zaměřuje se na **tvorbu** a **správu aplikací** (např. webová aplikace, API aplikace, WebJobs, Mobilní aplikace)
- **Automatické škálování** a **vysoká dostupnost**
- Podpora OS Windows, Linux
- Automatizované nasazení z GitHubu, Azure DevOps...
#### 3) Síťové služby Azure
##### Virtuální sítě v Azure
- Zajišťují **vzájemnou komunikaci** mezi prostředky, uživateli na internetu, klientskými počítači v on-premise
- Víceméně se jedná o rozšíření stávající on-premise sítě o prostředky zajišťující propojení s ostatními prostředky Azure
- **Klíčové funkce** virtuálních sítí:
	1) izolace a segmentace
	2) komunikace na internetu
	3) komunikace mezi prostředky Azure
	4) komunikace s prostředky on-premise, k jejichž propojení lze využít:
		- Připojení point-to-site
		- Připojení site-to-site
		- Připojení ExpressRoute
	5) Směrování síťového provozu
	6) Filtrování síťového provozu
	7) Propojení virtuálních sítí
- Podpora koncových bodů s **veřejnou** i **privátní IP adresou**
##### Virtuální sítě v Azure - Azure VPN Gateway
- **Brána virtuální sítě**, umístěná ve vyhrazené podsíti, zajišťující šifrované tunelované připojení:
	1) Datacenter k virtuálním sítím (site-to-site)
	2) Jednotlivých zařízení k virtuálním sítím (point-to-site)
	3) Virtuálních sítí k jiným virtuálním sítím (network-to-network)
- Dělí se na:
	1) Policy-based VPN gateway:
		- Pro každý tunel se zadáva IP adresa
	2) Route-based: 
		- Tunely IPSec mají buď podobu síťového rozhraní, nebo virtuálního tunelového rozhraní
		- Příslušné rozhraní pro odesílání paketů se definuje statickým nebo dynamickým routingem
		- Přednostně používaný u on-premise řešenich
		- Např propojení virtuálních sítí, point-to-site připojení, multisite připojení, koexistence s Azure ExpressRoute
- Možnosti **zvýšení odolnosti**:
	1) Active/standby instance
		- Dvě instance VPN Gateway
	2) Active/active instance
		- Dvě instance VPN Gateway
	3) ExpressRoute failover
		- VPN Gateway slouží jako záloha
	4) Zone-redundant gateways
		- Nasazení bran VPN a ExpressRoute v oblastech s podporou zón dostupností)**
##### Virtuální sítě v Azure - Azure ExpressRoute
- Umožňuje **rozšíření on-premise sítí** (poboček, datacenter...) **do cloudu** pomocí **privátního připojení** v podobě okruhu ExpressRoute
- **Nevyužívá veřejný internet**
- **Spolehlivější**, **rychlejší**, **stabilní latence** a **vyšší bezpečnost**
##### Virtuální sítě v Azure - Azure DNS
- Nabízí **překlad názvů** prostřednictvím infrastruktury Azure
- Výhody:
	- Spolehlivost a výkon
	- Bezpečnost
	- Spravování záznamů jak pro služby Azure, tak pro externí prostředky
	- Součástí portálu Azure, Azure CLI, Azure Powershell, RestApi a SDK
	- Podpora privátních domén
	- Podpora záznamů typu Alias
#### 4) Služby úložiště Azure Storage
##### Účet uložiště
- **Jedinečný jmenný prostor** pro data Azure Storage
- Data jsou **přístupná odkudkoliv** pomocí HTTP nebo HTTPS
- Data jsou **zabezpečena** a mají **vysokou dostupnost**, **odolnost** a **škálovatelnost**
- Různé typy účtu uložiště
- Koncový bod pro účet uložiště je dán kombinací názvu účtu a koncového bodu služby Azure Storage
##### Možnosti redundance u úložiště Azure
- Vždy je **ukládáno několik kopií dat** za účelem **ochrany před ztrátou**
- k dispozici je **několik řešení redundance** (vždy je potřeba rozhodnout mezi výši nákladů a úrovni dostupnosti)
##### Redundance v primární oblasti
1) **Locally redundant storage** (**LRS**)
	- Tři kopie v jednom datacentru nacházejícím se v primární oblasti
	- Nejlevnější řešení s ochranou pouze proti selhání serverového racku a disků
2) **Zone redundant sotrage** (**ZRS**)
	- Provádí se synchronní replikace dat přes tři zóny dostupnosti primární oblasti
	- Data jsou dostupná i po výpadku zóny
##### Redundance v sekundární oblasti
1) **Geo redundant storage** (**GRS**)
	- Tři kopie dat v jednom místě v primární oblasti (LRS) a poté se asynchronně vytvoří kopie do jednoho umístění v sekundární oblasti (LRS)
2) **Geo zone redundant storage** (**GZRS**)
	- Data se kopírují do tří zón dostupnosti v primární oblasti (ZRS) a následně se kopírují do druhé oblasti (LRS)
		- Nejvyšší odolnost, dostupnost a výkon
##### Služby úložiště Azure
1) **Azure Blobs**
	- Škálovatelné úložiště pro binární data a text s podporou pro big data
2) **Azure Files**
	- Sdílení souborů pro on-premise i cloudová řešení
3) **Azure Queues**
	- Úložiště pro zprávy zasílané při komunikaci mezi komponentami aplikací
4) **Azure Disks**
	- Svazky úložišť využívající blok určené pro virtuální počítače Azure
- **Výhody**: 
	1) Odolnost vůči chybám, vysoká dostupnost, bezpečnost, škálovatelnost
	2) Zajištěná správa hardwaru pro ukládání dat
	3) Přístup odkudkoliv přes HTTP, HTTPS, podpora jazyků a skriptů pro Azure Powershell nebo Azure CLI
	4) Podpora přístupu přes portál Azure nebo průzkumník uložišť Azure
##### Úložiště typu blob (Azure Blob Storage)
- Vhodné pro ukládání velkého množství **binárních** nebo **textových dat**
- Nestrukturované úložiště
- **Úrovně přístupu se dělí na základě frekvence přístupu** a **intervalu jejich změny** na: 
	1) Hot access:
		- Data, k nimž se přistupuje velmi často
	2) Cool access:
		- Data, k nimž se přistupuje velmi málo
	3) Archieve access:
		- Data, k nimž se přistupuje velmi málo, nejnižší cena za uložení, ale nevyšší cena za přístup
##### Azure Files
- Sdílení souborů v cloudu s možností **přístupu** přes **protokoly SMB** nebo **NFS**
- **Sdílené prostředky lze připojit** k zařízením v **cloudu** i **on-premise** a to v **OS Windows**, **Linux** i **macOS**
- Pomocí **Azure File Sync** lze **sdílené prostředky** **uložit do cahce serverů Windows Server**
- **Plně spravované řešení** s podporou **skriptování** v **PowerSehllu** nebo **Azure CLI**
- **Vysoce odolné proti výpadkům**
##### Azure Queue Storage
- Úložiště pro **ukládání nezpracovaných zpráv pro asycnrhonní zpracování**
- Pro **ukládní velkého množství zpráv** o **max velikosti 64 KB**
- Často se využívá **v kombinaci s jinyými výpočetními službami**, které se aktivují při přijetí zprávy (např. **Azure Functions**)
##### Disk Storage (Azure managed disks)
- **Bloková úložiště** určená pro práci s **virtuálními počítači** Azure
- **běžné disky** s posílenou **odolností** a **dostupností**

