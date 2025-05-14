#### 1) Charakteristika OS Windows – historie, přehled verzí, architektura, popis základních prvků grafického rozhraní OS Windows, příkazový řádek
##### OS Windows - Historie
- Od roku **1985** uvedeno na trh **25 různých verzí Windows**
- **1985** – Windows **1.0**
- **1995** – Windows **95** – **Nabídka Start**, **32bitová** architektura.
- **2001** – Windows **XP** – **Stabilní** a **populární**.
- **2007** – Windows **Vista** – **Nový vzhled**, ale **horší výkon**.
##### OS Windows - Přehled verzí
1) **Windows 7**:
	- 2009
	- Jedna z nejúspěšnějších verzí Windows
	- Objevení Knihoven a sdílení souborů v podobě domácí skupiny
2) **Windows 8**:
	- 2012
	- Proměna uživatelského rozhraní
	- Kompatibilitu s dotykovými obrazovkami, tablety a mobilními zařízeními
	- Méně populární a neúspěšná verze
3) **Windows 8.1**:
	- 2013
	- Obrazovka, na kterou byli uživatelé zvyklí a plnohodnotná nabídka start
	- Celá řada nových funkcí a snazší možnosti konfigurace pro desktopové grafické rozhraní
4) **Windows 10**:
	- 2015
	- Možnost návratu k desktopově orientovanému rozhraní
	- Univerzální aplikace, pro počítače i  mobilních zařízení
	- Prohlížeč Microsoft Edge
	- Panel Charm byl nahrazen Centrem akcí
	- Nový model aktualizací s aktualizacemi funkcí vydávanými dvakrát ročně a aktualizacemi vydávanými měsíčně
5) **Windows 11**:
	- 2021
	- Modernizované uživatelské rozhraní s přepracovanou nabídkou Start
	- Vylepšený multitasking díky funkcím Snap Layouts, Snap Groups a virtuálním plochám
	- Integrace Microsoft Teams přímo do systému
	- Lepší podpora pro dotyková zařízení a gesta
##### OS Windows - Architektura
- **32bit**
- **64bit**
##### OS Windows - Popis základních prvků grafického rozhraní
1) **Pracovní plocha**:
	- Hlavní panel, Tlačítko Start, Ikony připnutých programů
	- Lze ji přizpůsobit (přetažením zástupců, změněním motivu..)
2) **Nabídka Start**:
	- Zástupci k nejběžnějším knihovnám, nastavením a tlačítkům,
	- Aplikace v abecedním pořadí včetně naposledy instalovaných aplikací a nejčastěji používaných aplikací
	- Dlaždice aplikací seřazené do jednotlivých kategorií
3) **Hlavní panel (Taskbar)**:
	- Snadný přístup k nejčastěji používaným funkcím, aplikacím, souborům, nástrojům a nastavením Windows
	- Jump Lists (seznamy příkazů specifické pro každou aplikaci)
##### OS Windows - Příkazový řádek
- **CMD** a **PowerShelll**
- **Powershell** je nástroj představující **prostředí s příkazovým řádkem**, který má **více funkcí**, včetně**skriptování** a **automatizace**:
	- Prostředí pro skriptování se nazývá PowerShell ISE
	- Pracuje s cmdlety, pro které je možné nadefinovat aliasy
	- Poprvé uveden ve Windows 10
- **Lze spustit** klávesovou zkratkou **okno + r -> cmd**
- Klávesovou zkratkou **Ctrl + Shift + Enter** se spustí **v režimu správce**
- **Základní příkazy**:
	- `help`
	- `exit`
	- `dir`
	- `cd` 
	- `md` (make directory)
	- `rd` (remove directory)
	- `move `
	- `ren` (rename)
	- `type` (zobrazení typu souboru)
	- `more` (zobrazení obsahu souboru)
	- `copy`
	- `xcopy` (kopírování souborů nebo celých adresářových stromů)
	- `robocopy` (robust copy, hromadné kopírování)
	- `tasklist`
	- `taskkill`
	- `del`
	- `shutdown`
- Oba dva nástroje **podporují zástupné znaky**
#### 2) Charakteristika UNIX-like OS – popis a ovládání pomocí grafického rozhraní i terminálu, práce s nápovědou, základní pojmy z oblasti UNIX-like operačních systémů (pojmy distribuce, rodina distribucí, balíček, závislost, repozitář, nástroje pro správu balíčků a další)

##### UNIX-like OS - Popis a ovládání pomocí grafického rozhraní
- Obsahuje **subsystémy**, které **uživatel** může **přidávat** nebo **odebírat**
- **Výchozím GUI** v **Ubuntu** je **Unity**
- **Schopnost pracovat** s **více pracovními plochami**
##### UNIX-like OS - Popis a ovládání pomocí terminálu
- **Komunikace** s **operačním systémem** pomocí  **CLI**:
	- Parametry, volby a přepínače pro zajištění flexibility příkazů a nástrojů (znak pomlčky)
- V **GUI** se příkazový řádek spustí **prostřednictvím aplikace pro emulaci terminálu**:
	- Zadané příkazy jsou interpretovány shellem, který tyto příkazy předá jádru operačnímu systému:
		- Program login spouští shell po úspěšném přihlášení uživatele 
##### UNIX-like OS - Práce s nápovědou
1) **Man Pages** (**Manual Pages**):
	- Manuál pro daný příkaz
	- Obsahuje seznam voleb podporovaný příkazem včetně vysvětlení jejich významu a příklady použití (u některých)
	- `man {příkaz}`
2) **Volba** `--help`:
	- Lze ji použít u řady příkazů (ne u všech)
	- Zkrácená verze manuálu
3) **Dokumentace v** `/usr/share/doc`:
	- Pro každý nástroj je adresář, v němž se nachází užitečné informace, které nejsou v man pages,  šablony a konfigurační soubory
	- `/usr/share/doc/squid-3.3.8` obsahuje podrobnou dokumentaci k nástroji Squid včetně podrobně konfiguračního souboru
4) **GNU Info**:
	- Velmi podobné man pages
	- Hypertextové odkazy pro navigaci mezi jednotlivými sekcemi dokumentace
	- `info coreutils` obsahuje podrobný popis každého nástroje, který je součástí coreutils
##### UNIX-like OS - Základní pojmy z oblasti UNIX-like operačních systémů
- **Distribuce**:
	- Soubor balíčků softwaru tvořících jeden systém (kernel, utility, software)
- **Rodina Distribucí**:
	- Skupina operačních systémů založených na společném základu, které sdílejí podobné balíčkové systémy a filozofii
	- Debian, Red Hat nebo Arch Linux
- **Balíček**:
	- Předem sestavený program nebo sada
	- K dispozici v centrálních repozitářích, kde jsou již sestavené, otestované a udržované a pro každou distribuci
- **Závislost**:
	- Vlastnost balíčků mezi sebou
- **Repozitář**:
	- Online úložiště softwarových balíčků, odkud lze instalovat, aktualizovat a spravovat software v systému pomocí balíčkovacího nástroje
- **Nástroje pro správu balíčků**:
	- Každá rodina distribucí má jiný balíčkovací systém, které jsou nekompatibilní:
		- Debian má .deb
		- CentOS má .rpm
	- Slouží ke správě a instalaci softwaru
	- Dokážou řešit závislosti mezi balíčky
	- Dva typy nástrojů:
		- **Low-level tools**:
			- Provádí na pozadí vlastí instalaci, upgrade a odstranění souborů balíčků
			- pro Debian dpkg
			- pro CentOS rpm
		- **High-level tools**:
			- Zajišťují řešení závislostí a vyhledávání metadat
			- Pro Debian apt-get nebo aptitude
			- pro CentOS yum
- **Kernel**:
	- Jádro operačního systému, které spravuje hardware, procesy, pameť a I/O operace
	- Linux Kernel
#### 3) Možnosti instalace a upgradu operačních systémů Windows a UNIX-like OS
##### Možnosti upgradu OS Windows
- Závisí na **konkrétní verzi operačního systému**
- Platí, že **nelze provést upgrade** **32 bitové** verze **na 64 bitovou verzi** a na **W10 lze upgradovat** z **W7** a **W8**
- **Nástroj Pomocník** pro aktualizaci systému, který **lze získat** na webu:
	1) **In-place upgrade**:
		- Aktualizace a současný přenos aplikací a nastavení do nového operačního systému
		- automatizace nástrojem SCCM (System Center Configuration Manager)
		- provádí se z W7, W8 na W10**
	2) **Čistá instalace**:
		- Úplné vymazání dat
		- Instalační disk lze vytvořit pomocí nástroje Media Creation Tool
##### Možnosti instalace OS Windows
1) **Síťová instalace**:
	- **PXE instalace** (**Preboot Execution Enviroment**):
		- Instalační soubory jsou na serveru, klient k nim přistupuje vzdáleně pomocí Softwarového balíčku, který zajišťuje uložení instalačních souborů a poskytuje vše potřebné pro přístup k instalačním souborům
		- Vytvoření speciálního prostředí, které zajistí spuštění počítače, připojení do sítě a komunikaci se serverem (PXE)
	- **Bezobslužná instalace**:
		- Instalační program `setup.exe` je nutné spustit s volbami uživatele přednastavenými v souboru odpovědí:
			- Odpovědi na kladené dotazy jsou automaticky vyplněné z tohoto souboru
			- Pro vytvoření souboru odpovědí lze použít System Image Manager (SIM)
			- Tento soubor se kopíruje na server, na klientovi se spustí `unattended.bat`, kde se nastaví disk a instaluje přes síť, nebo se vytvoří spouštěcí disk pro instalaci
	- **Vzdálená instalace**:
		- Autopilot
2) **Instalace z obrazu**:
	- Obraz uložený na diskovém oddílu (skrytém oddílu):
		- Který je nepřístupný (recovery partition)
	- Operační systém se obnoví do továrního nastavení
3) **Pokročilé možnosti spuštění** (**Windows Advanced Startup Options**):
	- Obnovit počítač do továrního nastavení
	- Obnovení Systému
	- Upgrade
	- Opravná instalace
- Po **dokončení** instalace provést **aktualizaci** službou **Microsoft Windows Update**
##### UNIX-like OS - Možnosti upgradu a instalace
- **Možnosti instalace**:
	1) Čistá instalace z bootovacího média (USB/DVD)
	2) Dual-Boot (Instalace vedle Windows s možností volby OS při startu)
	3) Virtuální stroj (VirtualBox, VMWare)
- **Možnosti Upgradu**:
	- Přímý upgrade (do-release-upgrade)
	- LTS na LTS (Operační systémy s dlouhodobou podporou lze upgradovat mezi sebou)
	- Reinstalace při zachování dat
 