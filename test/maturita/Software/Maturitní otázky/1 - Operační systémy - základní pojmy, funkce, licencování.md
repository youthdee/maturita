#### 1) Účel operačního systému, víceuživatelský (multiuser) operační systém, multitasking, multiprocessing, multithreading

##### Účel operačního systému
- Vytvořit rozhraní a zajistit komunikaci mezi uživatelem, aplikacemi a hardwarem
- Vytvořit na pevném disku strukturu souborů, která umožňuje ukládání dat
- Umožnit uživateli komunikaci se softwarem a hardwarem
- Vyhledat požadovanou aplikaci a načíst ji do RAM počítače

##### Základní pojmy
-  Multi-user (Víceuživatelský operační systém)
	- V operačním systému je zřízeno více uživatelských účtů (často má každý uživatel vlastní uživatelský účet)
	- Díky tomu může na počítači používat aplikace a periferní (přídavná) zařízení více uživatelů
	- Umožňuje pracovat na počítači více uživatelům současně
- Multitasking
	- Na počítači může běžet více aplikací současně
- Multiprocessing
	- Operační systém podporuje počítače s dvěma a více CPU
- Multithreading
	- Některé aplikace mohou být rozděleny do několika částí, které operační systém načítá pouze v případě potřeby
	- Multithreading umožňuje, aby mohly různé části programu běžet současně

#### 2) Základní funkce operačního systému

##### Základní funkce OS
- Komunikace mezi aplikacemi a hardwarem:
	- pro komunikaci mezi aplikacemi a hardwarem se používají ovladače zařízení
	- Detekce hardwaru a instalace ovladačů probíhá v soudobých operačních systémech automaticky prostřednictvím PnP (Plug and Play)
		- V opačném případě je nutné nainstalovat ovladač ručně
- Správa souborů a složek pro ukládání dat
	- Operační systém vytváří na disku strukturu pro ukládání dat v podobě souborů, které se organizují do složek
	- Na disku se tak vytvoří stromová struktura složek, podsložek a souborů
- Uživatelské rozhraní
	- Slouží pro komunikaci uživatele s operačním systémem, hardwarem a aplikacemi
	- Dělí se na dva typy:
		- Command-line Interface "CLI" (textové rozhraní v podobě příkazového řádku)
		- Graphical User Interface "GUI" (grafické rozhraní v podobě ikon a nabídek)
- Správa aplikací
	- Operační systém načítá požadovanou aplikaci do paměti RAM a přiděluje ji potřebné systémové prostředky
	- Aplikace přistupují k prostředkům spravovaným operačním systémem prostřednictvím API (Application Programming Interface), což je soubor knihoven pro přístup k systémovým prostředkům
	- Aby byla aplikace kompatibilní, musí používat správné API
	- Příklad API:
		- OpenGL (Multiplatformní specifikace pro grafiku)
		- DirectX (Specifikace pro grafiku ve Windows)
		- Windows API (rozhraní pro práci s ovládacími prvky GUI, správu souborů a uživatelské rozhraní)



#### 3) Charakteristika a filozofie licencování operačních systémů a softwaru obecně

##### Komerční Software (proprietární)
- Software s uzavřeným zdrojovým kódem
- Uživatel nemá přístup ke zdrojovému kódu
- Autor programu uživateli (nabyvateli licence) prostřednictvím licence předepisuje podmínky používání programu (např. EULA od firmy Microsoft)
- Patří sem například Windows od firmy Microsoft

##### Filozofie operačního systému Windows
- Operační systém Windows existuje ve 32 bit a 64 bit edicích
- Na trh bylo uvedeno přes 25 různých verzí Windows, z nich se ale nabízí pouze 9
##### Open Source Software
- Alternativa ke komerčnímu softwaru co se týče vývoje a distribuce
- Nabyvatel licence není omezen ve způsobu používání programu a má přístup ke zdrojovému kódu programu
	- může používat program k libovolnému účelu
	- může pořizovat kopie a šířit je
	- může vytvářet odvozená díla a ty pak šířit
	- má přístup ke zdrojovému kódu programu
	- může kombinovat program s jinými programy
- Vývoj svobodného softwaru je spojen se jménem Richard Stallman (Vývojář a propagátor svobodného softwaru)

##### Druhy aplikací dle licence
- Original Equipment Manufacturer (OEM)
	- Běžné verze programů nabízené s novým HW
- Demoverze
	- Zdarma, omezený rozsah funkčnosti
- Zkušební verze (trial)
	- Plnohodnotná, časově omezená verze
- Shareware
	- Typicky plnohodnotná verze
	- po uplynutí lhůty nutno autorovi zaplatit za užití
- Freeware
	- Software dosutpný plně zdarma
	- Lze zdarma užívat i šířit
- Public domain
	- Software bez aotorských dispozic
	- Práva autora expirovala nebo se jich vzdal
- Free & Open Source
	- Volně šiřitelný software včetně zdrojového kódu
	- Organizace, které působí v této oblasti: Free and Open Source Software (FOSS) a Free/Libre/Open source Software (FLOSS)
	- GNU General Public License (GPL)
		- Jedna z nejpopulárnějších licencí
		- k dispozici ve třech verzích
	- GNU Lesser General Public License (LGPL)
		- Umožňuje likování free softwaru s non-free knihovnami
	

##### Filozofie UNIX-Like systémů - UNIX
- Jedním z hlavních pilířů Open Source je Linux, který vychází z UNIXu
- UNIX je operační systém vyvinutý v Bellových laboratořích americké firmy AT&T v roce 1969
- Současně ochranná známka v majetku konsorcia The Open Group
	- Označení UNIX mohou používat pouze systémy certifikované pod Single UNIX Specification
- Existuje řada systémů kompatibilních s UNIXem, ale nechtějí platit licenční poplatky, proto používají varianty názvu UNIX
	- např. otevřené systémy MINIX, Linux, OpenBSD, NetBSD
	- Jedná se o tzv. unixové (unix-like) systémy
- Komerční verze UNIX je například Solaris, HP-UX a AIX
- U komečních verzí UNIX se velmi dbá na zajištění kvality, dokumentace, hlášení chyb a jejich řešení
	- Nelze však měnit a přidávat klíčové součásti systému
	- Změny jsou povoleny pouze jako reakce na chybu v určité části systému
	- Provádí se tzv. regresivní testy s cílem zajistit kvalitu operačního systému
	- Správa kódu je velmi komplikovaná

##### Filozofie UNIX-kie systémů - Linux
- Linus Torvalds
- Linux je vyvíjen jako produkt práce dobrovolníků a za jeho vývoj není zodpovědná žádná organizace
	- Například pokud chce vývojář mít svůj kód v oficiálním kernelu, pošle jej Linusu Torvaldsovi, který jej schválí a otestuje a případně přidá
- Cílem není dokonalý kód, ale neustálý vývoj zdarma dostupné varianty UNIXu
- Nová funkce nebo software se vydává ve verzi alfa a je určena ostatním k otestování, poté následuje verze beta, která je funkční, ale nemusí v ní být všechny potřebné funkce a nakonec fáze finální, kfy je software považován za úplný a použitelný
- Namísto regesních testů kvality se využívá uživatelů, protože uživatel je nejlepší tester
- Linux kernel (jádro linuxu) je napsáno bez použití jakéhokoliv proprietárního kódu
- Software pro Linux se vydává v podobě distribuce
	- Souborů balíčků softwaru tvořících jeden systém (kernel, utility, software)
- Neznámější distribuce Linuxu:
	- RedHat:
		- Firma vyvíjející a prodávající Red Hat Enterprise Linux
		- Nekomerční je distribuce Fedora
	- SuSE:
		- Placené veze pro domácnosti a firmy
		- openSuSE je nekomerční
	- Debian:
		- Nejrozsáhlejší distribuce plně vyvíjena komunitou
		- Vývojový cyklus tří větví (stable, testing, unstable)
		- Používá balíčkový systém apt
	- Ubuntu:
		- Vyvíjena komunitou za podpory firmou Canonical a postavena na distribuci Debian
		- Orientována na osobní PC
	- Další distrubuce:
		- Linux Mint, Arch Linux, Gentoo, Kali Linux, SystemRescueCD
- Linux je součástí síťových prvků, superpočítačů, mobilních telefonů, IoT zařízení...