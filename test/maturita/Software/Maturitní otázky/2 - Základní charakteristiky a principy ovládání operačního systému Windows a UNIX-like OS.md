#### 1) Charakteristika OS Windows – historie, přehled verzí, architektura, popis základních prvků grafického rozhraní OS Windows, příkazový řádek
##### OS Windows - Historie
- Od roku **1985** bylo uvedeno na trh přes **25 různých verzí Windows**
- **1985** – Windows **1.0**
- **1995** – Windows **95** – **Nabídka Start**, **32bitová** architektura.
- **2001** – Windows **XP** – **Stabilní** a **populární**.
- **2007** – Windows **Vista** – **Nový vzhled**, ale **horší výkon**.
##### OS Windows - Přehled verzí
- **Windows 7**
	- Uvedeno na trh **v roce 2009**
	- Jedna z **nejúspěšnějších verzí** Windows
	- Objevení **Knihoven** a **sdílení souborů** v podobě **domácí skupiny**
- **Windows 8**
	- Uvedeno na trh **v roce 2012**
	- Zásadní **proměna uživatelského rozhraní**
	- Navrženo pro **kompatibilitu** s **dotykovými obrazovkami**, **tablety** a **mobilními zařízeními**
	- **Méně populární** a spíše **neúspěšná verze** windows
- **Windows 8.1**
	- Uvedeno na trh **v roce 2013**
	- Obsahoval **obrazovku**, na kterou **byli uživatelé zvyklí** a **plnohodnotnou nabídku start** v hlavním panelu
	- Obsahoval **celou řadu nových funkcí** a **snazší možnosti konfigurace** pro **desktopové grafické rozhraní**
- **Windows 10**
	- Uvedeno na trh **v roce 2015**
	- Nabízí **možnost návratu** k **desktopově orientovanému rozhraní**
	- Obsahuje **univerzální aplikace**, které běží jak na **stolních počítačích**, tak na **mobilních zařízeních**
	- Poprvé se objevil prohlížeč **Microsoft Edge**
	- **Panel Charm** byl **nahrazen** **Centrem akcí Windows**
	- Využívá **nový model aktualizací** s aktualizacemi **funkcí vydvanými dvakrát ročně** a **aktualizacemi vydávanými měsíčně**
- **Windows 11**
	- Uvedeno na trh **v roce 2021**
	- **Modernizované uživatelské rozhraní** s přepracovanou **nabídkou Start** a zaoblenými rohy
	- **Vylepšený multitasking** díky funkcím **Snap Layouts**, **Snap Groups** a **virtuálním plochám**
	- **Integrace Microsoft Teams** přímo do **systému**
	- **Lepší podpora** pro **dotyková zařízení a gesta**
##### OS Windows - Architektura
//TODO
##### OS Windows - Popis základních prvků grafického rozhraní
- **Pracovní plocha**
	- Obsahuje **Hlavní panel**, **Tlačítko Start**, **Ikony připnutých programů**
	- Lze ji **přizpůsobit**, např přetažením zástupců, změněním motivu..
- **Nabídka Start**
	- Obsahuje **Zástupce** k **nejběžnějším knihovnám**, **nastavením** a **tlačítkům pro vypnutí počítače**, **Aplikace** v abecedním pořadí včetně **naposledy instalovaných aplikací** a **nejčastěji používaných aplikací** a **Dlaždice aplikací** seřazené do **jednotlivých kategorií**
- **Hlavní panel (Taskbar)**
	- Poskytuje **snadný přístup** k **nejčastěji používaným funkcím**, **aplikacím**, **souborům**, **nástrojům** a **nastavením Windows**
	- Nabízí funkce **Jump Lists** (**seznamy příkazů specifické pro každou aplikaci**), možnost zobrazení obrázku s náhledem spuštěného programu
##### OS Windows - Příkazový řádek
- V OS Windows se nachází **dva nástroje** obsahující  **příkazový řádek** - **PowerShell** a klasický **příkazový řádek** (**cmd**)
- **Powershell** je nástroj představující **prostředí s příkazovým řádkem**, který má **daleko více funkcí**, nabízí možnost **skriptování** a **automatizace**
	- **Vlastní prostředí** pro **skriptování** se nazývá **PowerShell ISE**
	- **Powershell** pracuje s **cmdlety**, pro které je možné **nadefinovat aliasy**
- **cmd** byl **standardním nástrojem** pro **práci** **v prostředí tohoto příkazového řádku** až do **uvedení PowerShellu ve Windows 10**
- **Rozhraní příkazového řádku** lze **spustit** např. **okno + r -> cmd**
- Klávesovou zkratkou **Ctrl + Shift + Enter** se spustí **cmd v režimu správce**
- **Základní příkazy**:
	- **help**
	- **command** /? (zobrazení nápovědy ke kontkétnímu příkazu)
	- **cls**
	- **exit**
	- **ctrl c**
	- **dir**
	- **cd** 
	- **md** (make directory)
	- **rd** (remove directory)
	- **move** 
	- **ren** (rename)
	- **type** (zobrazení typu souboru)
	- **more** (zobrazení obsahu souboru)
	- **copy**
	- **xcopy** (kopírování souborů nebo celých adresářových stromů)
	- **robocopy** (robust copy, hromadné kopírování)
	- **chkdisk**
	- **format**
	- **diskpart** (spuštění samostatného programu pro práci s diskovými oddíly)
	- **tasklist**
	- **taskkill**
	- **del**
	- **dism** (pro práci s obrazy systému používaná před jejich nasazením)
	- **sfc** (ověření a oprava systémových souborů Windows)
	- **shutdown**
- U **Cmd** a **Powershellu** je podpora **zástupných znaků** (* ?)

#### 2) Charakteristika UNIX-like OS – popis a ovládání pomocí grafického rozhraní i terminálu, práce s nápovědou, základní pojmy z oblasti UNIX-like operačních systémů (pojmy distribuce, rodina distribucí, balíček, závislost, repozitář, nástroje pro správu balíčků a další)

##### UNIX-like OS - Popis a ovládání pomocí grafického rozhraní
- **Grafické rozhraní** v **UNIX-Like** systémech většinou obsahuje **celou řadu subsystémů**, které **uživatel** rovněž může **přidávat** nebo **odebírat**
- **Výchozím GUI** u distribuce **Ubuntu** je **Unity**
- **GUI** v **Linuxu** má **schopnost pracovat** s **více pracovními plochami**
##### UNIX-like OS - Popis a ovládání pomocí terminálu
- V **UNIX-Like Systémech** může uživatel **komunikovat** s **operačním systémem** pomocí rozhraní **příkazového řádku** (**CLI**)
- Kvůli **flexibilitě** se u **příkazů** nebo **nástrojů** **podporujících parametry**, **volby** a **přepínače** obvykle píše **před** těmito **řetězci** znak **pomlčky** 
- I přes **existenci** rozhraní **příkazového řádku** se **často operační systém** standardně **zavádí** do **grafického rozhraní**, čímž se **rozhraní příkazového řádku** před **uživatelem skrývá**
- Jednou z možností, jak v **grafickém uživatelském rozhraní** **spustit** rozhraní **příkazového řádku** je **prostřednictvím** **aplikace** pro **emulaci terminálu**
- **Příkazy** zadané z klávesnice jsou **interpretovány** **programem** s názvem **shell**, který tyto **příkazy předává operačnímu systému**
	- **Program login** spouští **shell** po **úspěšném přihlášení** uživatele do operačního systému
	- Hned poté **může ověřený uživatel** začít **komunikovat** s **jádrem operačního systému** pomocí **textových příkazů**

##### UNIX-like OS - Práce s nápovědou
- **Man Pages** (**Manual Pages**)
	- Představuje **manuál** pro **daný příkaz**
	- Obsahuje **seznam voleb** **podporovaný příkazem** včetně **vysvětlení jejich významu**
	- U některých **příkazů** jsou **uvedeny** i **příklady použití**
	- Příkaz "**man {příkaz}**"
- **Volba --help**
	- Lze ji **použít** u řady **příkazů** (**ne u všech**)
	- **Zkracéná verze** **manuálu** pro daný příkaz
	- Příkaz "**{příkaz} --help**"
- **Dokumentace v /usr/share/doc**
	- Zde je pro každý **nástroj nainstalovaný** v **Linuxu** **jeden adresář**, v němž se **nachází užitečné informace**, které **nejsou v man pages**, dále **šablony** a **konfigurační** soubory usnadňující konfiguraci
	- Příklad "/usr/share/doc/squid-3.3.8" obsahuje **podrobnou** **dokumentaci** k nástroji Squid včetně podrobně **komentovaného konfiguračního souboru**
- **GNU Info**
	- Dokumentace **info** jsou **velmi podobné man pages**
	- kromě **nápovědy** pro daný **příkaz** obsahují **hypertextové odkazy** pro **navigaci** mezi **jednotlivými sekcemi** dokumentace
	- Příklad "**info coreutils**" obsahuje **podrobný popis každého nástroje**, který **je součástí coreutils**
##### UNIX-like OS - Základní pojmy z oblasti UNIX-like operačních systémů
- **Distribuce**
	- **soubor balíčků** softwaru **tvořících** jeden systém (**kernel**, **utility**, **software**)
- **Rodina Distribucí**
	- **Skupina operačních systémů** založených na **společném základu**, které **sdílejí** podobné **balíčkové systémy** a **filozodii**
	- Například **Debian**, **Red Hat** nebo **Arch Linux**
- **Balíček**
	- **Předem sestavený program** nebo **sada programů**
	- Lze ho získat přes **Internet** z **centrálních repozitářů**, kde jsou **již sestavené**, **otestované** a **udržované** a pro **každou distribuci** (popřípadě **v podobě zdrojového kódu** pro ruční instalaci)
- **Závislost**
	- **Vlastnost balíčků** mezi sebou (jeden balíček **může mít závislost na jiném**, nebo na **nějaké knihovně**)
- **Repozitář**
	- **Online Úložiště** **softwarových balíčků**, odkud lze **instalovat**, **aktualizovat** a **spravovat** software v systému pomocí **balíčkovacího nástroje**
- **Nástroje pro správu balíčků**
	- Každá rodina **distribucí** má **jiný balíčkovací systém**, které jsou **nekompatibilní**
		- **Debian** má **.deb**
		- **CentOS** má **.rpm**
	- Slouží ke **správě** a **instalaci** (včetně **aktualizace** a **odebrání**) softwaru (balíčků) **v operačním systému**
	- Dokážou zároveň **řešit závislosti** mezi balíčky pro **zajištění funkčnosti**
	- Pro správu balíčků se používají **dva typy nástrojů**:
		- **Low-level tools**
			- Provádí **na pozadí vlastí instalaci**, **upgrade** a **odstranění** souborů balíčků
			- pro **Debian dpkg**, pro **CentOS rpm**
		- **High-level tools**
			- Zajišťují **řešení závislostí** a **vyhledávání metadat**
			- Pro **Debian apt-get** nebo **aptitude**, pro **CentOS yum**
- **Kernel**
	- **Jádro operačního systému**, které **spravuje hardware**, **procesy**, **pameť** a **I/O operace**
	- Například **Linux Kernel**
	

#### 3) Možnosti instalace a upgradu operačních systémů Windows a UNIX-like OS
##### Možnosti instalace a upgradu OS Windows
- **Upgrade OS Windows**
	- Dostupné **možnosti upgradu** závisí na **konkrétní verzi operačního systému**
	- Platí, že **nelze provést upgrade** **32 bitové** verze **na 64 bitovou verzi** a na **W10 lze upgradovat** z **W7** a **W8** (Nikoliv W XP či W Vista)
	- **Upgrade** lze provést **pomocí nástroje Pomocník** **pro aktualizaci systému**, který **lze získat** na webu
		- Například **upgrade z W7** nebo **W8 na Windows 10** lze provést **stažením Průvodce Pomocník** pro aktualizaci systému Windows 10, který lze získat na webu Microsoft
	- Počítače s OS W XP nebo W Vista není možné upgradovat na W 10
		- v tomto případě je třeba provést čistou instalaci (instalační disk lze vytvořit pomocí nástroje Media Creation Tool)
	- Způsoby upgradu:
		- In-place upgrade
			- Aktualizace operačního systému a současně přenos aplikací i nastavení a ovladačů do nového operačního systému
			- Lze automatizovat nástrojem SCCM (System Center Configuration Manager)
			- Tento způsob upgradu se provádí z W7, W8 na W10
		- Čistá instalace
			- Dojde k úplnému vymazání dat z disku
- Instalace OS Windows
	- Možnosti instalace OS Windows:
		- Síťová instalace
			- PXE instalace (Preboot Execution Enviroment)
				- instalační soubory se nacházejí na serveru, klient k nim přistupuje vzdáleně pomocí softwarového balíčku (Remote Installation Services), který zajišťuje uložení instalačních souborů a poskytuje vše potřebné pro přístup k instalačním souborům
				- Vzhledem k tomu, že na klientském PC není žádný operační systém, je třeba pro spuštění počítače vytvořit speciální prostředí, které zajistí spuštění počítače, připojení do sítě a komunikaci se serverem (PXE)
			- Bezobslužná instalace
				- Instalační program setup.exe je nutné spustit s volbami uživatele přednastavenými v souboru odpovědí
				- Instalační program pak hledá tyto odpovědi na dotazy kladené během instalace v tomto souboru a nechce je tím pádem od uživatele
				- Pro vytvoření souboru odpovědí pro instalaci lze použít System Image Manager (SIM)
				- soubor odpovědí se pak kopíruje na server do sdílené složky určené pro distribuci, kde se buď spustí soubor unattended.bat přímo na klientském PC (nastaví se tak pevný disk a instalace probíhá přes síť) nebo vytvořit spouštěcí disk, který spustí počítač a připojí ho ke sdílené složce určené pro distribuci
			- Vzdálená instalace
		- Instalace z obrazu uloženého na diskovém oddílu v počítači
			- Zde se používá obraz OS Windows uložený na diskovém oddílu (často skrytém oddílu)
			- Při použití tohoto obrazu se operační systém obnoví do stavu, v jakém byl při výrobě počítače (tovární nastavení)
			- jedná se o diskový oddíl, který je nepřístupný uživateli (recovery partition)
		- Pokročilé možnosti spuštění (Windows Advanced Startup Options)
		- Obnovit počítač do továrního nastavení
		- Obnovení Systému
		- Upgrade
		- Opravná instalace
		- Obnovení počítače do továrního nastavení
	- Po dokončení instalace je nutno provést aktualizaci operačního systému službou Microsoft Windows Update
	- Také je nutno ověřit, zda je správně nainstalovaný veškerý hardware nástrojem Správce Zařízení

##### UNIX-like OS - Možnosti upgradu a instalace
- Možnosti instalace:
	- Čistá instalace z bootovacího média (USB/DVD)
	- Dual-Boot (Instalace vedle Windows s možností volby OS při startu)
	- Virtuální stroj (VirtualBox, VMWare)
- Možnosti Upgradu:
	- Přímý upgrade (do-release-upgrade)
	- LTS na LTS (Operační systémy s dlouhodobou podporou lze upgradovat mezi sebou)
	- Reinstalace při zachování dat
