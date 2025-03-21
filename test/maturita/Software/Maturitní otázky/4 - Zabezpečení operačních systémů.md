##### 1) Bezpečnostní hrozby, malware a ochrana proti malwaru, síťové útoky, sociální inženýrství
##### Bezpečnostní hrozby
- **Neaktuální antivirus**
- **Neaktuální** **operační systém**
- **Neaktuální programy**
- **Infikované stránky**
- **Nevyžádané e-maily**
- **Data přes výměnné sítě**
- **Stažení** "**free**" **programů**
- **Nalezené flashdisky**
- **Další hosté na počítači**
- **Otevírání příloh ze sociálních sítí**
##### Malware
- Nejčastěji se **šíří přes internet**, skrze **webové stránky**, **zkušební** verze, **cracky**...
- **Obsahuje škodlivý kód** bez ohledu na způsob **napadení**, **chování** nebo **výsledek**
- Typicky instalován na počítači **bez vědomí** uživatele
- Jakmile je počítač infikovaný, **malware může**:
	- **Měnit konfiguraci** počítače
	- **Odstraňovat soubory** nebo **poškodit disk**
	- **Sbírat informace** uložené na počítači **bez oprávnění uživatele**
	- **Otevírat extérní okna** nebo **přesměrovat prohlížeč**
- Hlavní **typy malwaru**:
	- **Virus** (malware šířící se rychle po počítačové síti)
	- **Spyware** (Malware špehující uživatele)
	- **Adware** (Malware propagující nechtěné reklamy)
	- **RansomWare** (malware vyžadující výkupné za dešifrování disku)
	- **Trosjký kůň** (malware skrývající se za něčem užitečným)
	- **Červ** (Malware který se sám replikuje)
##### Ochrana proti Malwaru
- **Antimalwarové** (antivirové) programy které **dokážou blokovat** různé typy malwaru
- Spouštějí se **při spuštění počítače** a **kontrolují systémové prostředky**, **disky** a **paměť** na přitomnost malwaru
- Navíc **běží nepřetržitě na pozadí** a **skenují podpisy malwaru**
	- Když je **detokován malware**, **anitmalwarový program vydá upozornění** a ideálně ho **zablokuje** nebo **přesune do karantény**
- **Možnosti detekce virů**:
	- **Scanner**:
		- Vyhledávání **vybraných oblastí** na **výskyt vzorků viru** podle **virové databáze** antivirového programu (**file signature**)
	- **Heuristická analýza**:
		- Rozbor kódu **hledající postupy**, které jsou pro **činnost virů typické** nebo nějak **podezřelé**
	- **Kontrola integrity**:
		- Porovnání **aktuálního stavu** důležitých programů a **oblasti na disku** s informacemi, které si o nich **kontrolní program uložil při jejich příchodu do systému** nebo při své **instalaci**
	- **Monitorování systému**:
		- **Neustálé hlídání změn** v nastavení systému
##### Síťové útoky
- **DDoS** (**Distributed Denial of Service**):
	- Cílem je **službu znefunkčnit** a **znepřístupnit ostatním uživatelům** obrovským množstvím požadavků **pocházejících z infikovaných počítačů** (**zombies**)
	- **SYN Flood** (**SYN pakety bez odpovědi**)
	- **ICMP Flood** (**ICMP pakety** s **falešnou zdrojovou IP adresou**)
- **Man In The Middle** (**MITM**):
	- Snaha útočníka **odposlouchávat komunikaci** mezi **dvěma prostředky** tak, že se **postaví mezi ně** a stane se tak **prostředníkem**
- **Únos spojení TCP**:
	- Hacker zjistí **pořadové číslo klienta a serveru** a tím pádem **všechny data procházejí přes hackera**
- **DNS Poisoning**:
	- **Infikování klientského počítače** pro příjem **falešných záznamů** dns

##### Sociální inženýrství
- **Techniky pro manipulaci lidí** za účelem **provedení určité akce** nebo **získání určité informace** (osobních údajů)
- Druh **podvodu** nebo **podvodného jednání** za **účelem získání utajených informací** organizace nebo **přístupu do informačního systému** firmy
- Ve většině případů útočník **nepřichází do osobního kontaktu** s obětí
- **Nejslabším článkem každého bezpečnostního řešení je člověk**
- Techniky se snaží **upoutat vaši pozornost** a **donutit vás uskutečnit** předem promyšlenou akci, s **cílem získat určité informace** nebo **získat práva do počítačového systému**
- **Princip fungování**:
	- **Vyvolání strachu**
	- Brnkání na strunu **chamtivosti**
	- Vzbuzení **zvědavosti**
	- **Žádost o pomoc**
	- Zneužití **empatie** či **soucitu**
- **Nejznámější techniky a nástroje sociálního inženýrství**:
	- **Pharming** (**přesměrování adresy** pomocí **změny DNS** na **zfalšovanou webovou adresu**)
	- **Phishing** (**Vydávání se za důvěryhodnou autoritu**)
	- **Vishing** (Technika **telefonicky** prováděného phishingu)
	- **Pretexting** (získávání **cizích osobních údajů pod falešnou záminkou**)
	- **Evil twin** (cracker **falešně napodobuje** vlastnosti **otevřené Wi-Fi** sítě, kam se má uživatel připojit. Jedná se o **specifický phishing**)
##### 2) Základní postupy při zabezpečení operačních systémů – zásady zabezpečení, fyzické zabezpečení, metody ochrany a bezpečného odstraňování dat
##### Zásady zabezpečení
- **Sada pravidel** umožňujících **bezpečnost sítě**, **dat** a **počítačů v organizaci**
- Konstantě **aktualizovaný dokument** na **bázi změn v technologií**, **biznisu** a **požadavků zaměstnanců**
- **Pravidla typu**:
	- **Identifikace** a **ověřování** (**Kdo** a **jak** se může **přihlásit do sítě**).
	- **Hesla** (Požadavky na **složitost** a **pravidelnou změnu**)
	- **Přijatelné použití** (Co je **povoleno** a co hrozí za **porušení** pravidel)
	- **Vzdálený přístup** (**Jak** a **k čemu** se lze **připojit na dálku**)
	- **Údržba sítě** (**Aktualizace** **systémů** a **aplikací**)
	- **Řešení incidentů** (Postup při **bezpečnostních problémech**)
##### Fyzické zabezpečení
- Stejně **důležité jako zabezpečení dat** (když je počítač s daty ukraden, data jsou ukradena a zároveň ztracena)
- **Fyzická bezpečnost zahrnuje**:
	- **Ochranu vstupu** do budovy
	- **Ochranu** omezených **prostor**
	- **Zabezpečení IT** a **sítě**
##### Metody ochrany a bezpečného odstraňování dat
- **Ochránit data lze**:
	- **Zálohováním**:
		- Jedno z nejvíce **efektivních způsobů** **zabezpečení dat** proti ztrátě
		- Zálohy by měly být prováděny **pravidelně**
		- Většinou jsou shromažďovány **mimo hlavní působení** (např. v jiném serveru) kvůli zajištění redundance
	- **Šifrováním**
		- Technologie kdy jsou data **transformována do podoby kde jsou nečitelná pro počítač**
		- Speciálním **klíčem** je lze **zpět dešifrovat**
		- Na **Windows** technologie **EFS**, **BitLocker**
	- **Nastavení oprávnění**
		- Lze tak **efektivně povolit** či **zabránit přístup** k **souborům** nebo **složkám** uživatelům nebo skupinám
		- **Uživatelé by měli být oprávněni pouze k věcem, které nutně potřebují k vykonání práce**
- **Bezpečně odstranit data lze**:
	- **Na magnetických discích**:
		- **Software pro mazání dat**:
		    - **Přepisuje existující data** opakovaně, čímž je **činí nečitelnými**.
		    - Známé také jako "**secure erase**".
		- **Degaussingová hůlka**:
		    - Obsahuje **silné magnety**, které **narušují** nebo **odstraňují** **magnetické pole** na plotnách pevného disku.
		    - Disky musí být vystaveny účinku hůlky **přibližně 2 minuty**.
		- **Elektromagnetické degaussingové zařízení**:
		    - **Rychlé** a **účinné** pro **mazání více disků** najednou.
		    - Používá **magnet s elektrickým proudem** k vytvoření **silného magnetického pole**, které **narušuje data**.
		    - Velmi **drahé**, ale **extrémně rychlé** (vymaže disk během **několika sekund**).
	- **Na ostatních mediích**: 
		- Pro bezpečné **smazání SSD** se používá **secure erase**.
		- **Optická média**, **eMMC**, **USB disky** je nutné **fyzicky zničit** (skartace/spálení).
		- Data mohou být i v **tiskárnách** a **multifunkčních zařízeních** – je třeba je **pravidelně mazat**.
##### 3) Konfigurace zabezpečení a zásad zabezpečení serverů a klientských stanic.
##### Klientské stanice
- Počítače by měly být **zabezpečeny proti krádeži**
- Uživatelé by měly **uzamknout počítač** v případě **nepřitomnosti**
- Přístup do počítače by měl být **zabezpečen hesly** (existují **3 vrstvy zabezpečení pomocí hesel**):
	- **BIOS** nebo **UEFI** (**všichni uživatelé sdílejí stejné heslo**)
	- **Windows Login** (**Windows Hello**, **PIN**, **Picture Password**, **Dynamic Lock**)
	- **Přihlášení do aplikací**
- Pokud jde o **lokální zásadu zabezpečení**, ta se dá **nakonfigurovat v konzoli** "**secpol.msc**" -> **secpol**
- Také lze **nastavit zásady v Zásady účtu** -> **Hesla nebo Zásady účtu** -> **Account Lockout Policy**
	- Kde **Account Lockout Policy zabraňuje útokům typu dictionary**, kde se **zkouší prolomit heslo** pomocí **každého slova v tomto slovníku**
##### Servery
- Lze konfigurovat **Doménovou zásadu zabezpečení** na **Windows Serveru**, podle které se pak **řídí počítače v doméně**
##### Active Directory a Místní bezpečnostní zásady ve Windows
Ve většině sítí s Windows je **Active Directory** nakonfigurováno na Windows Serveru s doménami. Počítače v doméně se řídí **Doménovou bezpečnostní politikou**, kterou nastavuje administrátor.

Pro **samostatné počítače mimo doménu** slouží **Místní bezpečnostní zásady** (**Local Security Policy**), které lze otevřít pomocí:

- **Windows 7 a Vista**: Start > Ovládací panely > Nástroje pro správu > Místní bezpečnostní zásady
- **Windows 8, 8.1, 10**: Hledání > `secpol.msc`
- **Všechny verze**: `secpol.msc` v příkazovém řádku **Spustit**

##### **Nastavení bezpečnostní politiky**

- **Hesla**: Požadavky na složitost nastavíte v **Account Policies > Password Policy**
- **Blokace účtů**: Ochrana proti útokům hrubou silou a slovníkovým útokům (**Account Policies > Account Lockout Policy**)
- **Auditování**: Zaznamenávání přihlášení (**Local Policies > Audit Policy**)
- **Práva uživatelů**: Konfigurace přístupových práv a bezpečnostních možností

##### **Replikace Místní bezpečnostní politiky**

Administrátor může politiku exportovat a nasadit na jiné počítače:

1. **Exportovat** pomocí **Action > Export List…**
2. **Uložit** jako např. `workstation.inf` na externí médium
3. **Importovat** do dalších samostatných počítačů

Tím lze snadno zavést jednotnou bezpečnostní konfiguraci na více zařízeních.