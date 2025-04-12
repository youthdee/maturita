#### 1) Bezpečnostní hrozby, malware a ochrana proti malwaru, síťové útoky, sociální inženýrství
##### Bezpečnostní hrozby
- Neaktuální antivirus, operační systém či programy
- Infikované stránky
- Data přes výměnné sítě
- Stažení "free" programů
- Nalezené flashdisky
- Další hosté na počítači
- Otevírání příloh ze sociálních sítí či nevyžádaných e-mailů
##### Malware
- Nejčastěji se **šíří přes internet**, skrze **webové stránky**, **zkušební** verze
- **Obsahuje škodlivý kód** bez ohledu na způsob **napadení**, **chování** nebo **výsledek**
- Typicky instalován na počítači **bez vědomí** uživatele
- **Jakmile je počítač infikovaný, malware může**:
	- Měnit konfiguraci počítače
	- Odstraňovat soubory nebo poškodit disk
	- Sbírat uložené informace bez oprávnění uživatele
	- Otevírat extérní okna nebo přesměrovat prohlížeč
- **Hlavní typy malwaru**
	1) **Virus**: 
		- Malware šířící se rychle po počítačové síti
	2) **Spyware**: 
		- Malware špehující uživatele
	3) **Adware**: 
		- Malware propagující nechtěné reklamy
	4) **RansomWare**: 
		- Malware vyžadující výkupné za dešifrování disku
	5) **Trosjký kůň**: 
		- Malware skrývající se za něčem užitečným
	6) **Červ**:
		- Malware který se sám replikuje
##### Ochrana proti Malwaru
- Programy, které **dokážou blokovat** různé typy malwaru
- Spouštějí se při spuštění počítače a kontrolují systémové prostředky, disky a paměť na přítomnost malwaru
- **Běží nepřetržitě na pozadí** a **skenují podpisy malwaru**
	- Když je detekován malware, program vydá upozornění a zablokuje ho nebo přesune do karantény
- **Možnosti detekce virů**:
	 1) **Scanner**:
		- Vyhledávání vybraných oblastí na výskyt vzorků viru podle virové databáze antivirového programu (file signature)
	2) **Heuristická analýza**:
		- Rozbor kódu hledající postupy, které jsou pro činnost virů typické nebo nějak podezřelé
	3) **Kontrola integrity**:
		- Porovnání aktuálního stavu důležitých programů a oblasti na disku s informacemi, které si o nich kontrolní program uložil při jejich příchodu do systému nebo při své instalaci
	4) **Monitorování systému**:
		- Neustálé hlídání změn v nastavení systému
##### Síťové útoky
1) **DDoS** (**Distributed Denial of Service**):
	- Cílem je službu znefunkčnit a znepřístupnit ostatním uživatelům obrovským množstvím požadavků pocházejících z infikovaných počítačů (zombies)
	- **SYN Flood** (SYN pakety bez odpovědi)
	- **ICMP Flood** (ICMP pakety s falešnou zdrojovou IP adresou)
2) **Man In The Middle** (**MITM**):
	- Odposlech komunikace mezi dvěma prostředky, postavením se mezi ně a být tak prostředníkem
3) **Únos spojení TCP**:
	- Hacker zjistí pořadové číslo klienta a serveru a tím pádem všechny data procházejí přes hackera
4) **DNS Poisoning**:
	- Infikování klientského počítače pro příjem falešných záznamů DNS
##### Sociální inženýrství
- **Techniky pro manipulaci lidí** za účelem **provedení určité akce** nebo **získání určité informace**
- Druh **podvodu** nebo **podvodného jednání** za **účelem získání utajených informací** organizace nebo **přístupu do informačního systému** firmy
- Ve většině případů útočník **nepřichází do osobního kontaktu** s obětí
- **Nejslabším článkem každého bezpečnostního řešení je člověk**
- **Princip fungování**:
	- Vyvolání strachu
	- Brnkání na strunu chamtivosti
	- Vzbuzení zvědavosti
	- Žádost o pomoc
	- Zneužití empatie či soucitu
- **Nejznámější techniky a nástroje sociálního inženýrství**:
	1) **Pharming**:
		- Přesměrování adresy pomocí změny DNS na zfalšovanou webovou adresu
	2) **Phishing**:
		- Vydávání se za důvěryhodnou autoritu
	3) **Vishing**:
		- Technika telefonicky prováděného phishingu
	4) **Pretexting**: 
		- Získávání cizích osobních údajů pod falešnou záminkou
	5) **Evil twin**:
		- Cracker falešně napodobuje vlastnosti otevřené Wi-Fi sítě, kam se má uživatel připojit. Jedná se o specifický phishing
#### 2) Základní postupy při zabezpečení operačních systémů – zásady zabezpečení, fyzické zabezpečení, metody ochrany a bezpečného odstraňování dat
##### Zásady zabezpečení
- **Sada pravidel** umožňujících **bezpečnost sítě**, **dat** a **počítačů v organizaci**
- Konstantě **aktualizovaný dokument** na **bázi změn v technologií**, **biznisu** a **požadavků zaměstnanců**
- **Pravidla typu**:
	1) **Identifikace a ověřování**:
		- Kdo a jak se může přihlásit do sítě
	2) **Hesla**:
		- Požadavky na složitost a pravidelnou změnu
	3) **Přijatelné použití**:
		- Co je povoleno a co hrozí za porušení pravidel
	4) **Vzdálený přístup**:
		- Jak a k čemu se lze připojit na dálku
	5) **Údržba sítě**: 
		- Aktualizace systémů a aplikací
	6) **Řešení incidentů**:
		- Postup při bezpečnostních problémech
##### Fyzické zabezpečení 
- **Fyzická bezpečnost zahrnuje**:
	- Ochranu vstupu do budovy
	- Ochranu omezených prostor
	- Zabezpečení IT a sítě
##### Metody ochrany a bezpečného odstraňování dat
- **Ochránit data lze**:
	1) **Zálohováním**:
		- Jedno z nejvíce efektivních způsobů zabezpečení dat
		- Zálohy by měly být prováděny pravidelně
		- Shromažďovány mimo hlavní působení (např. v jiném serveru) kvůli zajištění redundance
	2) **Šifrováním**
		- Data jsou transformována do podoby kde jsou nečitelná pro počítač
		- Speciálním klíčem je lze zpět dešifrovat
		- Na Windows technologie EFS, BitLocker
	3) **Nastavení oprávnění**
		- Efektivní povolení či odepření přístupu k souborům nebo složkám
		- Uživatelé by měli být oprávněni pouze k věcem, které nutně potřebují k vykonání práce
- **Bezpečně odstranit data lze**:
	1) **Na magnetických discích**:
		1) **Software pro mazání dat**:
		    - Přepisuje existující data opakovaně, čímž je činí nečitelnými.
		    - Známé také jako "secure erase".
		2) **Degaussingová hůlka**:
		    - Obsahuje silné magnety, které narušují nebo odstraňují magnetické pole na plotnách pevného disku.
		3) **Elektromagnetické degaussingové zařízení**:
		    - Rychlé a účinné pro mazání více disků najednou.
		    - Používá magnet s elektrickým proudem k vytvoření silného magnetického pole, které narušuje data.
		    - Velmi drahé, ale extrémně rychlé.
	2) **Na ostatních mediích**: 
		- Pro bezpečné smazání SSD se používá secure erase.
		- Optická média, eMMC, USB disky je nutné fyzicky zničit
		- Data mohou být i v tiskárnách a multifunkčních zařízeních
#### 3) Konfigurace zabezpečení a zásad zabezpečení serverů a klientských stanic.
##### Klientské stanice
- Počítače by měly být **zabezpečeny proti krádeži**
- Uživatelé by měly **uzamknout počítač** v případě **nepřítomnosti**
- **3 vrstvy zabezpečení pomocí hesel**:
	1) **BIOS nebo UEFI**:
		- Všichni uživatelé sdílejí stejné heslo
	2) **Windows Login**:
		- Windows Hello, PIN, Picture Password, Dynamic Lock
	3) **Přihlášení do aplikací**:
- Lokální zásada zabezpečení se konfiguruje v konzoli `secpol.msc` -> secpol
- Také lze **nastavit zásady v Zásady účtu** -> **Hesla nebo Zásady účtu** -> **Account Lockout Policy**
	- Kde Account Lockout Policy zabraňuje útokům typu dictionary, kde se zkouší prolomit heslo pomocí každého slova v tomto slovníku
##### Servery
- Lze konfigurovat **Doménovou zásadu zabezpečení** na **Windows Serveru**, podle které se pak **řídí počítače v doméně**
##### Active Directory a Místní bezpečnostní zásady ve Windows
- Počítače v doméně se řídí **Doménovou bezpečnostní politikou**
- Pro **samostatné počítače mimo doménu** slouží **Místní bezpečnostní zásady** (**Local Security Policy**), které lze otevřít pomocí:
	- `secpol.msc`
##### Nastavení bezpečnostní politiky
1) **Hesla**: 
	-  Account Policies > Password Policy
2) **Blokace účtů**: 
	- Ochrana proti útokům hrubou silou a slovníkovým útokům (Account Policies > Account Lockout Policy)
3) **Auditování**: 
	- Zaznamenávání přihlášení (Local Policies > Audit Policy)
4) **Práva uživatelů**:
	- Konfigurace přístupových práv a bezpečnostních možností

