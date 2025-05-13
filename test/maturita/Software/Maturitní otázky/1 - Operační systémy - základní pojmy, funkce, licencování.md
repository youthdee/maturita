#### 1) Účel operačního systému, víceuživatelský (multiuser) operační systém, multitasking, multiprocessing, multithreading
##### Účel operačního systému
- **Vytvořit rozhraní** a **zajistit komunikaci** mezi **uživatelem**, **aplikacemi** a **hardwarem**
- **Vytvořit** na pevném **disku** **strukturu souborů**
- Vyhledat požadovanou **aplikaci** a **načíst** ji do **RAM** počítače
##### Základní pojmy
1) **Multi-user** (Víceuživatelský operační systém):
	- V operačním systému je zřízeno více uživatelských účtů 
	- Aplikace a periferní zařízení  může používat více uživatelů
	- Umožňuje pracovat na počítači více uživatelům současně
2) **Multi-tasking**:
	- Může běžet více aplikací současně
3) **Multi-processing**:
	- Operační systém podporuje počítač s více procesory
4) **Multi-threading**:
	- Aplikace rozděleny do dílčích částí, které jsou načteny v případě potřeby (do vláken)
	- Různé části programu mohou běžet paralelně
#### 2) Základní funkce operačního systému
##### Základní funkce operačního systému
1) **Komunikace mezi aplikacemi a hardwarem** **pomocí ovladačů**:
	- Detekce hardwaru a instalace ovladačů probíhá automaticky prostřednictvím PnP (Plug and Play)
2) **Správa souborů a složek pro ukládání dat**:
	- Struktura pro ukládání dat v podobě souborů, organizovaných do složek
3) **Uživatelské rozhraní**:
	- **Komunikaci uživatele s operačním systémem, hardwarem a aplikacemi**
		- Command-line Interface
		- Graphical User Interface
4) **Správa aplikací**:
	- Načtení požadované **aplikace** do paměti **RAM** a **přidělení** systémových prostředků
	- **Aplikace** **přistupují k prostředkům** **prostřednictvím API**:
		- **OpenGL** (Multiplatformní specifikace pro grafiku)
		- **DirectX** (Specifikace pro grafiku ve Windows)
		- **Windows API** (rozhraní pro práci s ovládacími prvky GUI, správu souborů a uživatelské rozhraní)
#### 3) Charakteristika a filozofie licencování operačních systémů a softwaru obecně
##### Komerční Software (**proprietární**)
- **Uzavřený zdrojový kód**, ke kterému **uživatel nemá přístup**
- **Autor** programu **uživateli** předepisuje **podmínky používání** programu **prostřednictvím licence** (např. EULA od firmy Microsoft):
	- Windows
##### Filozofie operačního systému Windows
- **32bit** a **64bit** verze
- Uvedeno přes **25** **různých verzí Windows**, **nabízí se pouze 9**
##### Open Source Software
- **Alternativa** ke **komerčnímu softwaru** (**vývoje a distribuce**)
- **Nabyvatel** licence **není omezen** ve **způsobu používání programu** a má **přístup** ke **zdrojovému kódu** programu:
	- Používání k libovolnému účelu
	- Pořizování kopií a šíření
	- Vytváření odvozených děl
	- Přístup ke zdrojovému kódu
	- Kombinace s jinými programy
- Vývoj spojen se jménem **Richard Stallman** (Vývojář a propagátor svobodného softwaru)
##### Druhy aplikací dle licence
1) **Original Equipment Manufacturer** (**OEM**):
	- Běžné verze programů nabízené s novým HW
2) **Demoverze**:
	- Zdarma, omezená funkčnost
3) **Zkušební verze**:
	- Plnohodnotná, časově omezená verze
4) **Shareware**:
	- Plnohodnotná verze, po uplynutí lhůty nutno autorovi zaplatit za užití
5) **Freeware**:
	- Dostupný plně zdarma, Lze zdarma užívat i šířit
6) **Public domain**:
	- bez autorských dispozic
7) **Free & Open Source**:
	- Volně šiřitelný, včetně zdrojového kódu
	- FOSS, FLOSS
8) **GNU General Public License** (**GPL**):
	- Nejpopulárnější, tři verze
9) **GNU Lesser General Public License** (**LGPL**):
	- Linkování free softwaru s non-free knihovnami
##### Filozofie UNIX-Like systémů - UNIX
- **Vyvinutý** v **Bellových laboratořích** americké firmy **AT&T** v roce **1969**
- **Ochranná známka** v majetku **konsorcia The Open Group**
	- Označení UNIX mohou používat pouze systémy certifikované pod Single UNIX Specification
- **Řada** systémů je **kompatibilních** s **UNIXem**, ale **neplatí** licenční poplatky, proto používají **varianty názvu UNIX** (**unixové** - **unix-like** systémy)
	-  MINIX, Linux, OpenBSD, NetBSD 
- **U komerčních verzí UNIX** se dbá na **zajištění kvality**, **dokumentace**, **hlášení chyb** a **jejich řešení**
	- Solaris, HP-UX a AIX
	- Nelze měnit a přidávat klíčové součásti systému, Změny jsou povoleny pouze jako reakce na chybu
	- Provádí se regresivní testy s cílem zajistit kvalitu operačního systému
##### Filozofie UNIX-kie systémů - Linux
- **Linus Torvalds**
- **Vyvíjen** jako **produkt** **dobrovolníků**, za jeho **vývoj** **není zodpovědná žádná organizace**
	- Pokud chce vývojář mít svůj kód v oficiálním kernelu, pošle jej Linusu Torvaldsovi, který jej schválí a otestuje a případně přidá
- **Cílem není dokonalý kód**, ale **neustálý vývoj zdarma** dostupné **varianty UNIXu**
	- Alfa verze je určena ostatním k testování
	- Beta verze je fukční, ale nemusí obsahovat potřebné funkce
	- Finální verze je úplná a použitelná
- **Místo regresivních testů se využívá uživatelů**
- **Linux kernel** je **napsán bez použití** jakéhokoliv **proprietárního kódu**
- **Software** **pro Linux** se vydává **v podobě distribuce**
- Soubor **balíčků softwaru** tvořících **jeden systém** (**kernel, utility, software**)
- **Neznámější distribuce** Linuxu:
	1) **RedHat**:
		- Firma vyvíjející a prodávající Red Hat Enterprise Linux
		- Nekomerční je distribuce Fedora
	2) **SuSE**:
		- Placené veze pro domácnosti a firmy
		- Nekomerční je OpenSuse
	3) **Debian**:
		- Nejrozsáhlejší distribuce plně vyvíjena komunitou, vývojový cyklus tří větví (stable, testing, unstable)
		- Balíčkový systém apt
	4) **Ubuntu**:
		- Vyvíjena komunitou za podpory firmou Canonical a postavena na distribuci Debian
		- Orientována na osobní PC**
	- **Další distrubuce**:
		- Linux Mint, Arch Linux, Gentoo, Kali Linux, SystemRescueCD