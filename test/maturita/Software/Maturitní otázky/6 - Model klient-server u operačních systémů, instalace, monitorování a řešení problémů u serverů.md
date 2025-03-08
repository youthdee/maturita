#### 1) Model klient/server u operačních systémů, role serveru, kritéria pro správný výběr serverových komponent, základní subsystémy serveru

##### Model Klient/Server
- Síť obsahující servery a klienty
- Síť obsahující server je ideální pro sdílení prostředků a dat, přičemž je dokáže centrálně zabezpečit

##### Server
- Počítač poskytující služby
- Při výběru serveru je vhodné vybrat hardware a software na základě role serveru. kterou bude plnit a na základě výkonu počítačů, které budou serverové služby využívat
- Role serveru je hlavní úkol, který server plní
	- Přičemž server může plnit současně více rolí (souborové, tiskové, webové, poštovní, databázové...)

##### Server - Výběr hardwaru
- Je třeba si uvědomit tyto požadavky:
	- Server je určen k tomu, aby poskytoval síťové služby více uživatelům současně
	- Pokud server havaruje nebo se stane nedostupným, ovlivní tato skutečnost klientské počítače, které využívají tento server
	- Je třeba tyto problémy předvídat, aby se s nimi dalo vypořádat co nejrychleji

##### Server - výběr softwaru
- Nejprve je třeba si vybrat operační systém, poté role, které bude operační systém a server plnit a naposled ostatní požadovaný software
##### Server - Základní subsystémy serveru
- Subsystémy:
	- Procesor
		- Integrovaný obvod, který vykonává matematické či logické instrukce
		- Rychlost procesoru se udává v GHz (taktovací frekvence)
		- Většina procesorů jsou multicore
		- 64bit a 32bit
	- Paměť (RAM)
		- Random Access Memory je paměť pro dočasné uložení dat
		- Volatilní (při výpadku napájení se obsah paměti smaže)
		- Obsahuje procesy (instrukce a data), ke kterým procesor přímo přistupuje
		- Velikost RAM významně ovlivňuje celkový výkon počítače
	- Úložiště
		- HDD (Hard Disk Drive) je z poloviny elektronické a z poloviny mechanické zařízením která pro princip ukládání dat na otáčející se plotně využívají princip magnetického záznamu
		- SSD (Solid State Drive) je zařízení, které je čistě elektronické
		- Běžné počítače využívají lokální disky
		- Servery mohou využívat externí úložiště typu NAS (Network Attached Storage) nebo SAN (Storage Area Network)
	- Počítačová síť
		- Bez připojení nemůže server komunikovat
		- Většina serverů má více síťových karet
		- Minimální přenosová rychlost u síťových karet je v současnosti 100 Mbit/s nebo 1 Gbit/s
			- U serverů je to minimálně 10 Gbit/s
	- Základní deska
		- Propojuje subsystémy do jednoho subsytému
		- Obsahuje procesor, který komunikuje s ostatními komponentami výpočetního systému
		- Sběrnice (Bus) slouží pro přenos dat mezi procesorem a pamětí a I/O zařízeními
- Po selhání libovolného subsystému havaruje celý server
- Každý z těchto subsystémů se může stát úzkým hrdlem, které ovlivní výkon celého serveru

##### Server - Funkce
- Programy, které nejsou přímou součástí role
- Požívají se pro rozšíření funkčnosti rolí a tedy i celého serveru

##### Klient
- Počítač využívající služby


#### 2) Monitorování a řešení problémů u serverů s OS Windows a UNIX-like OS včetně vhodných nástrojů

##### Metodika řešení problémů
1) Vyhledat problém
2) Vyhodnotit konfiguraci systému
3) Vypsat nebo vytypovat možná řešení problémů a zkusit problém izolovat odstraněním daného hardwaru nebo softwaru
4) Vykonat naplánované operace
5) Prověřit výsledek

##### Windows Server - vhodné nástroje pro řešení problémů a monitorování
- Systémové informace (MSINFO32.EXE)
	- Zobrazuje podrobné údaje o konfiguraci PC, komponentách operačního systému, ovladačích atd.
- Prohlížeč událostí (EVENTVWR.MSC)
	- Zásuvný modul pro konzolu MMC
	- Nástroj pro procházení a správu záznamů o událostech
	- Součást nástrojů Správa počítače, Správce serveru a Nástroje pro správu
- Sledování prostředků
	- Nástroj, který zobrazuje jak procesy a služby využívají systémové prostředky
	- Lze provádět analýzu neodpovídajících procesů, souborů využívaných aplikacemi a řídit činnost procesů a služeb
- Konfigurace systému (MSCONFIG.EXE)
	- Nástroj pro zjišťování problémů při spouštění Windows
	- Dokáže zakázat spouštění programů a služeb při startu operačního systému
- Správce úloh
	- Nástroj pro sledování výkonu, stavu spuštěných programů a programů, které neodpovídají a je třeba je ukončit
- Sledování výkonu
	- Poskytuje nástroje pro analýzu výkonu počítače
	- Je možné sledovat výkon aplikací a hardwaru v reálném čase, konfigurovat, která data se mají shromažďovat, definovat úrovně pro varování a automatické provádění určitých operací
- Další nástroje: 
	- Nástroj pro konfiguraci systému (msconfig)
	- Nástroj pro diagnostiku paměti (nástroje pro správu)
	- Průvodce řešením problémů
	- Spouštěcí nabídka včetně nouzového režimu
	- Obnova Windows
	- - Správce zařízení
##### Unix-Like OS - Vhodné nástroje pro řešení problémů a monitorování
- Sledování využití prostoru na discích
	- Příkaz "df" (disk free)
		- Zobrazí celkové využití disku souborovým systémem v bajtech, celkovou velikost souborového systému, volný a obsazený prostor a mount point každého úložiště
		- Příznak "-h" pro human-readable formu
		- - častým problémem může být nedostatek inodes (všechny soubory jsou mapovány na inodes, která obsahují metadata souboru)
	- Příkaz "du" (disk usage)
		- Lze použít pro zjištění, které soubory zabírají nejvíce místa
- Sledování využití RAM a CPU ( Nástroj "top")
	- zobrazuje stav systému v reálném čase
	- Pro sledování využití RAM a odkládacího prostore je možné použíz i příkaz "free" s příznakem "-g" pro human-readable formu
	- Alternativně nástroj "Htop"
- Sledování procesů (Nástroj "ps" a "pstree")
	- Zobrazuje vlastníka procesu, PID, parent PID, využití CPU, čas spuštění, tty, kumulovaný čas CPU, příkaz asociovaný s procesem
	- Procesy lze spravovat pomocí následujících signálů:
		- SIGTERM (15)
		- SIGINT (2)
		- SIGKILL (9)
		- SIGHUP (1
		- SIGTSTP (20)
		- SIGSTOP (19)
		- SIGCONT (18)
	- Příklad: "kill -9 {PID}"
	- Příčinu výpdaku či selhání lze odhalit pomcí logů v adresáři "/var/log"
- Nástroj pro správu služeb (systemctl)
	- Enable (Povolení)
	- Restart (Restartování)
	- Status (Status)
	- Start (Spouštění)
- Nástroj pro zobrazení chyb v konfiguračních souborech (journalctl)

#### 3) Technologie a komponenty používané pro zajištění nepřetržitého provozu serveru

##### Odolnost serveru vůči chybám
- Pro zajištění maximální odolnosti je třeba zjistit:
	- Které komponenty pravděpodobně havarují
	- Použít techniky minimalizující pravděpodobnost výpadku
- Jako redundantní se používají tyto komponenty:
	- Disky (RAID a náhradní disky - Hot Spares)
	- Napájecí zdroje
		- Řešeny pomocí nepřerušitelných napájecích zdrojů (UPS) a generátorů
	- Síťové karty - NIC Teaming
		- Je seskupení dvou nebo více síťových karet do jedné logické síťové karty
		- Zajišťuje odolnost vůči chybám, větší přenosovou rychlost a možnost provést rozložení zátěže (load balancing)
- Zálohování
	- Operace, při níž se vytváři kopie dat tak, aby se tyto kopie daly později použít k obnovení původních dat, která se poškodila
	- Provádí se na zálohovací servery, externí disky, cloud, magnetickou pásku
	- Při plánování zálohování se doporučuje oddělit soubory aplikací a datové soubory

##### Cluster
- Seskupení počítačů, které společně pracují jako jeden počítač
- V závislosti na použité technologii mohou clustery zajistit dostupnost a vyrovnání zátěže
- Cluster, který slouží pro zajištění činnosti po výpadku zařízení funguje i tehdy, když některý z jeho prvků havaruje
- Nejvyužívanější podoby clusterů:
	- Clustery s ochranou proti výpadku (failover clusters)
	- Clustery pro vyrovnání zátěže (load-balancing clusters)
##### 4) Možnosti vzdáleného přístupu a správy serveru

##### Unix-Based OS - SSH
- Příkaz "ssh {user}@{domain_name} -p {port}"
- Lze nakonfigurovat připojení v souboru ".ssh/config"

##### Windows Server - Remote Access Server (RAS)
- Umožňuje uživatelům se připojit k počítačové síti vzdáleně prostřednictvím různých protokolů a připojení
- Po připojení k serveru pro vzdálený přístup přes Internet se uživatelé zároveň dostanou do sítě firmy
##### Windows Server - Služby vzdálené plochy
- Remote Desktop Services, dříve Terminal Services
- Standardně se používá licenční režim vzdálené plochy pro správu, který umožňuje připojení až dvou vzdálených relací (nebo tří, pokud vznikla i konzolová relace při místním přihlášení)