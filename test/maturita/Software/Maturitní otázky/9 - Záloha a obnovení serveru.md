#### 1) Zálohování – definice, typy a správa záloh
##### Zálohování - Definice
- Operace, při níž se **vytváří kopie dat tak**, aby se tyto **kopie daly později použít k obnovení původních dat**, která se poškodila
- Typy poškození může být **havárie**, **nehoda**, **nechtěné smazání**, **útok**
- Záloha se obvykle provádí na **Zálohovací servery**, **externí disky**, **cloud** nebo **magnetické pásky**
- Při plánování zálohování se doporučuje od sebe **oddělit soubory aplikací a datové soubory**
	- Soubory aplikací se obvykle nijak nemění, proto je není nutno zálohovat tak často
	- Datové soubory se oproti tomu mění daleko častěji a proto je nutné je zálohovat častěji
- **Pro každý typ dat je možné naplánovat jinou strategii zálohování**
##### Metody správy zálohování
- **On-line**
- **Near-line** (SSD, cloudové úložiště)
- **Off-line**
- **Backup site** nebo **DR site** (disaster recovery)
	- Zařízení, které se **použije k obnově a obnovení své technologické infrastruktury** v případě havárie
##### OS Windows - Typy záloh celého systému
- **Úplná záloha** (**+ Inkrementální**)
	- Cíl vytvořit **více kopií zálohovaných dat vhodnějším způsobem**
	- Nejdříve je provedena **úplná záloha všech dat**, poté je provedena **inkrementální záloha** (ukládány jsou pouze soubory, které se změnily od předešlé úplné nebo inkrementální zálohy)
	- Hlavní nevýhodou je, že při obnovení zálohy je potřeba pracovat s úplnou zálohou a následně všemi inkrementálními zálohami až k požadovanému okamžiku zálohy
- **Úplná záloha s přírůstkovými zálohami**
- **Úplná záloha s rozdílovou zálohou** 
	- Po úplné záloze každá **částečná záloha zachytí všechny soubory vytvořené nebo změněné od vytvoření úplné zálohy**
	- Výhodou je, že obnova zahrnuje obnovení pouze poslední úplné zálohy a potom její překrytí poslední rozdílovou zálohou, takže je proces obnovení více odolný vůči defektu média se zálohou
##### OS Windows - Typy záloh souborů
- **Normální nebo úplná záloha**
	- zálohuje se vše **bez ohledu na atribut** "**Archivovat**"
	- po **zálohování se** **atribut vymaže**
	- při **změně souboru se atribut znovu** **nastaví**
- **Kopie**
	- zálohuje se **vše bez ohledu na atribut** "**Archivovat**"
	- Po **zálohování** se **atribut** **nevymaže**
- **Rozdílová**
	- Zálohují se soubory **změněné od posledního normálního nebo přírůstkového zálohování**
	- Zálohují se pouze soubory s **aktivním atributem** "**Archivovat**"
	- Atribut se **po zálohování nemění**
- **Přírůstková**
	- Zálohují se pouze soubory s **aktivním atributem** "**Archivovat**"
	- Atribut se **po zálohování vymaže** a při **následné změně nastaví**
- **Denní**
	- Zálohují se soubory na **základě data změny**
	- **Atribut** "**Archivovat**" **se nemění**
#### 2) Možnosti zotavení serveru
##### Příčiny havárie
- Chyby v softwaru
- Chyby v hardwaru
- Omyly uživatelů
- Omyly správců
- Úmyslné poškození
- Vyšší moc
##### Obnova OS Windows Server
- Windows server obsahuje na **instalačním DVD nástroj pro opravu v grafickém rozhraní**
	- Tento nástroj umožňuje **provést obnovu počítače pomocí dříve vytvořené bitové kopie**
	- Nebo **spustit příkazový řádek**
#### 3) Možnosti zálohování ve Windows
##### Programy zálohování Windows Server
- Ve Windows serveru je k dispozici **program Zálohování serveru** (**Windows Server Backup**)
	- Umí provádět **pouze úplné** nebo **přírůstkové zálohy**
	- Zálohuje se **databáze Active Directory**, **spouštěcí soubory**, **databáze prvků COM+** (zajišťuje funkčnost OS a aplikací), **registr systému** a **složka SYSVOL**
	- **U klientských PC** se zálohuje **registr**, **systémové soubory** a **prvky COM+** i s **daty aplikací** je možné provádět připojení a zálohování jiných PC
- Zálohování pomocí **příkazového řádku** příkazem "**wbadmin**"
- Případně programy třetích stran, které nabízejí daleko více možností
- **Prostředí pro zotavení systému Windows**
##### Stínové kopie
- Windows server obsahuje funkci **stínových kopií sdílených složek**, která **automaticky vytváří záložní kopie dat** **ve sdílených složkách** na vybraných svazcích NTFS v naplánovaných časech
- Tato funkce tak **umožňuje uživatelům získávat předchozí verze souborů a složek**
##### Zálohování pevného disku
- Nástroj pro zálohování **umožnuje zálohovat soubory**, případně **vytvořit** a **použít zálohu obrazu** či **vytvořit disk pro opravu systému** (nástroj je součástí OS)
- Funkce historie souborů lze nastavit v **Nastavení -> Aktualizace a zabezpečení -> Zálohování**
	- Tato funkce umožňuje pro **zálohování souborů ve složkách dokumenty**, **hudba**, **obrázky**, **videa a plocha**
	- Postupem času **vytváří historii souborů**, čímž umožňuje se **vrátit k předchozím verzím**, případně je obnovit
#### 4) Možnosti zálohování v UNIX-like OS – archivace, bitová kopie, rsync
##### UNIX-like OS - Možnosti zálohování
- Nástroj **dd**
- Nástroj **tar**
- Nástroj **rsync**
##### UNIX-like OS - Archivace (Nástroj Tar)
- Nástroj pro archivaci dokáže **z více souborů vytvořit jeden samostatný soubor archivu** za účelem zálohování na jiné médium nebo pro přenos po síti
- Nejpoužívanější je nástroj "**Tar - Tape Archiver**", který mimo archivace dokáže **provádět i kompresi**
	- Nástroj "**Tar {volby} {soubory}**" **vytváří archiv tar** (také označovaný jako **tarballl**)
	- Obvykle se používá s **kompresními nástroji**, např. **gzip**, **bzip2**, **xz**
	- **Při použití komprese tedy vznikne komprimovaný tarball**
	- Některé volby tohoto nástroje:
		- --create "**c**" (**vytvoření archivu** tar)
		- --extract "**x**" (**extrahování souborů** z archivu)
		- --update "**u**" (**připojení souborů**, které jsou novější, než ty, co již v archivu jsou)
	- Některé volby pro řízení činnosti tohoto nástroje:
		- --directory dir "**C**" (před zahájení operace dojde **k přepnutí do adresáře dir**)
		- --verbose "**v**" (výpis všech **přečtených nebo extrahovaných souborů**)
		- --verify "**W**" (**ověření archivu** po zapsání)
		- --{metoda archivace} (gzip, bzip2, xz)
- Metody komprese:
	- **gzip**
		- **nejstarší s nejmenším kompresním poměrem**
	- **bzip2**
		- **průměrný kompresní poměr**
	- **xz**
		- **nejnovější s nejlepší kompresí**
##### UNIX-like OS - Nátroj dd (Bitová kopie)
- **Zálohování celých disků** nebo **diskových oddílů**
- Řešení vhodné u nepřipojených zařízení, kde neprobíhají žádné I/O operace
- Nevýhodou je, že **výdledný obraz bude mít stejnou velikost jako disk** (nebo **diskový oddíl**) a to i tehdy, pokud je disk prázdný
- **Vytvoření souboru obrazu**:
	- **dd if={disk} of={obraz}**
- **Obnovení ze souboru obrazu**:
	- **dd if={obraz} of={disk}**
##### UNIX-like OS - Rsync
- Nástroj pro **lokální i vzdálené kopírování souborů**, **ideální pro zálohování** a **synchronizaci souborů na síťové disky**
- Synchronizace dvou místních adresářů nebo místních a vzdálených adresářů připojenách v místním souborovém systému:
	- **rsync -av {source_directory} {destination} {directory}**
	- **volba -a** označuje **rekurzivní synchronizaci** i podadresářů, zachování symbolických odkazů, časových razítek, oprávnění a vlastníků jako uživatelů i skupiny
	- volba **–v** označuje **verbose**
- Synchronizace místního adresáře se vzdáleným adresářem pomocí SSH: (místní adresář backups)
	- **rsync -avzhe ssh backups root@remote_host:/remote_directory/** (volba **-h** pro formát **human-readable**, volba **-e** ukazuje na **připojení pomocí SSH**)
- Synchronizace vzdáleného adresáře s místním adresářem přes SSH (vzdálený adresář backups)
	- **rsync -avzhe ssh root@remote_host:/remote_directory/ backups**
