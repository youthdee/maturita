#### 1) Účel operačního systému, víceuživatelský (multiuser) operační systém, multitasking, multiprocessing, multithreading
##### Účel operačního systému
- **Vytvořit rozhraní** a **zajistit komunikaci** mezi **uživatelem**, **aplikacemi** a **hardwarem**
- **Vytvořit** na pevném **disku** **strukturu souborů**
- Vyhledat požadovanou **aplikaci** a **načíst** ji do **RAM** počítače
##### Základní pojmy
-  **Multi-user** (Víceuživatelský operační systém)
	- V **operačním systému** je zřízeno **více uživatelských účtů** 
	- **aplikace** a **periferní** **zařízení  může používat více uživatelů**
	- Umožňuje **pracovat** na počítači **více uživatelům** **současně**
- **Multitasking**
	- Může **běžet více aplikací současně**
- **Multiprocessing**
	- Operační systém **podporuje počítač s více procesory**
- **Multithreading**
	- **Aplikace rozděleny do dílčích částí**, které jsou **načteny v případě potřeby**
	- Různé části programu mohou **běžet paralelně**
#### 2) Základní funkce operačního systému
##### Základní funkce OS
- **Komunikace mezi aplikacemi a hardwarem** **pomocí ovladačů**:
	- **Detekce hardwaru** a **instalace ovladačů** probíhá **automaticky** **prostřednictvím PnP** (Plug and Play)
- **Správa souborů a složek pro ukládání dat**
	- **Struktura** pro **ukládání dat** **v podobě souborů**, **organizovaných do složek**
- **Uživatelské rozhraní**
	- **Komunikaci uživatele s operačním systémem, hardwarem a aplikacemi**
		- **Command-line Interface**
		- **Graphical User Interface**
- **Správa aplikací**
	- Načtení požadované **aplikace** do paměti **RAM** a **přidělení** systémových prostředků
	- **Aplikace** **přistupují k prostředkům** **prostřednictvím API**
		- **OpenGL** (Multiplatformní specifikace pro grafiku)
		- **DirectX** (Specifikace pro grafiku ve Windows)
		- **Windows API** (rozhraní pro práci s ovládacími prvky GUI, správu souborů a uživatelské rozhraní)
#### 3) Charakteristika a filozofie licencování operačních systémů a softwaru obecně

##### Komerční Software** (**proprietární**)
- **Uzavřený zdrojový kód**, ke kterému **uživatel nemá přístup**
- **Autor** programu **uživateli** předepisuje **podmínky používání** programu **prostřednictvím licence** (např. EULA od firmy Microsoft)
	- **Windows**
##### Filozofie operačního systému Windows
- **32bit** a **64bit** verze
- Uvedeno přes **25** **různých verzí Windows**, **nabízí se pouze 9**
##### Open Source Software
- **Alternativa** ke **komerčnímu softwaru** (**vývoje a distribuce**)
- **Nabyvatel** licence **není omezen** ve **způsobu používání programu** a má **přístup** ke **zdrojovému kódu** programu
	- může **používat** program k **libovolnému účelu**
	- může **pořizovat** **kopie a šířit je**
	- může **vytvářet** **odvozená díla** a ty pak **šířit**
	- má **přístup** ke **zdrojovému kódu** programu
	- může **kombinovat** program s **jinými programy**
- Vývoj spojen se jménem **Richard Stallman** (Vývojář a propagátor svobodného softwaru)
##### Druhy aplikací dle licence
- **Original Equipment Manufacturer** (OEM)
	- **Běžné verze programů** nabízené s **novým HW**
- **Demoverze**
	- **Zdarma**, **omezená funkčnost**
- **Zkušební verze**
	- **Plnohodnotná**, **časově omezená** verze
- **Shareware**
	- **Plnohodnotná verze**, po **uplynutí lhůty** nutno autorovi **zaplatit za užití**
- **Freeware**
	- **Dostupný plně zdarma**, Lze **zdarma** **užívat i šířit**
- **Public domain**
	- Software **bez autorských dispozic**
- **Free & Open Source**
	- **Volně šiřitelný**, **včetně zdrojového kódu**
	- **FOSS**, **FLOSS**
- **GNU General Public License** (**GPL**)
		- Jedna z **nejpopulárnějších** **licencí**
		- k dispozici ve **třech verzích**
- **GNU Lesser General Public License** (**LGPL**)
		- Umožňuje **likování** **free softwaru** s **non-free knihovnami**
##### Filozofie UNIX-Like systémů - UNIX
- Jedním z hlavních **pilířů Open Source** je Linux, který **vychází z UNIXu**
- UNIX je operační systém **vyvinutý** v **Bellových laboratořích** americké firmy **AT&T** v roce **1969**
- Současně **ochranná známka** v majetku **konsorcia The Open Group**
	- **Označení UNIX** mohou používat pouze systémy **certifikované** pod **Single UNIX Specification**
- Existuje **řada** systémů **kompatibilních** s **UNIXem**, ale **nechtějí platit** licenční poplatky, proto používají **varianty názvu UNIX**
	- např. otevřené systémy **MINIX**, **Linux**, **OpenBSD**, **NetBSD**
	- **Jedná se** o tzv. **unixové** (**unix-like**) systémy
- **Komerční verze UNIX** je například **Solaris**, **HP-UX** a **AIX**
- **U komečních verzí UNIX** se velmi dbá na **zajištění kvality**, **dokumentace**, **hlášení chyb** a **jejich řešení**
	- **Nelze** však **měnit** a **přidávat** klíčové **součásti systému**
	- **Změny jsou povoleny** pouze **jako reakce na chybu** v určité části systému
	- **Provádí** se tzv. **regresivní testy** s cílem **zajistit kvalitu operačního systému**
	- **Správa kódu** je velmi **komplikovaná**

##### Filozofie UNIX-kie systémů - Linux
- **Linus Torvalds**
- Linux je **vyvíjen** jako **produkt** **práce dobrovolníků** a za jeho **vývoj** **není zodpovědná žádná organizace**
	- Například **pokud chce vývojář mít svůj kód v oficiálním kernelu**, **pošle jej Linusu Torvaldsovi**, který jej **schválí** a **otestuje** a **případně přidá**
- **Cílem není dokonalý kód**, ale **neustálý vývoj zdarma** dostupné **varianty UNIXu**
- **Nová funkce** nebo **software** se vydává ve **verzi alfa** a je určena **ostatním k otestování**, poté následuje **verze beta**, která je **funkční**, ale **nemusí** v ní **být** všechny **potřebné funkce** a nakonec **fáze finální**, kdy je **software považován za úplný a použitelný**
- **Namísto regesních** testů kvality se **využívá uživatelů**, protože **uživatel je nejlepší tester**
- **Linux kernel** (**jádro linuxu**) je **napsáno bez použití** jakéhokoliv **proprietárního kódu**
- **Software** **pro Linux** se vydává **v podobě distribuce**
	- Souborů **balíčků softwaru** **tvořících jeden systém** (**kernel, utility, software**)
- **Neznámější distribuce** Linuxu:
	- **RedHat**:
		- Firma vyvíjející a prodávající **Red Hat Enterprise Linux**
		- **Nekomerční je distribuce Fedora**
	- **SuSE**:
		- **Placené veze** pro domácnosti a firmy
		- **openSuSE** je **nekomerční**
	- **Debian**:
		- **Nejrozsáhlejší** distribuce **plně** **vyvíjena komunitou**
		- **Vývojový cyklus** tří větví (**stable, testing, unstable**)
		- Používá **balíčkový** **systém apt**
	- **Ubuntu**:
		- **Vyvíjena komunitou** za **podpory firmou Canonical** a **postavena na distribuci Debian**
		- Orientována na **osobní PC**
	- **Další distrubuce**:
		- **Linux Mint**, **Arch Linux**, **Gentoo**, **Kali Linux**, **SystemRescueCD**
- **Linux** je součástí **síťových prvků**, **superpočítačů**, **mobilních telefonů**, **IoT zařízení**...