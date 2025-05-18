#### 1) Zálohování – definice, typy a správa záloh
##### Zálohování - Definice
- Operace, při níž se **vytváří kopie dat tak**, aby se tyto **kopie daly později použít k obnovení původních dat**, která se poškodila
- Záloha se obvykle provádí na **zálohovací servery**, **externí disky**, **cloud** nebo **magnetické pásky**
- Při plánování zálohování se doporučuje od sebe **oddělit soubory aplikací a datové soubory**
	- Soubory aplikací se obvykle nijak nemění, proto je není nutno zálohovat tak často
	- Datové soubory se oproti tomu mění daleko častěji a proto je nutné je zálohovat častěji
- **Pro každý typ dat je možné naplánovat jinou strategii zálohování**
##### Nástroje pro správu záloh
- **Windows Server Backup**
	- Pouze úplné nebo přírůstkové zálohy
	- Zálohuje se Active Directory, spouštěcí soubory, databáze prvků COM+ (zajišťuje funkčnost OS a aplikací), registr systému a složka SYSVOL
	- U klientských PC se zálohuje registr, systémové soubory a prvky COM+ i s daty aplikací je možné provádět připojení a zálohování jiných PC
- Příkaz `wbadmin`
	- Zálohování jednotlivých svazků, disků a oddílů
	- Vytvoření bitové kopie systému
##### Metody správy zálohování
- **On-line**
- **Near-line** (SSD, cloudové úložiště)
- **Off-line**
- **Backup site** nebo **DR site** (disaster recovery)
	- Zařízení, které se použije k obnově a obnovení své technologické infrastruktury v případě havárie
##### OS Windows - Typy záloh celého systému
1) **Úplná záloha + Přírůstková záloha**
    - Nejprve se vytvoří kompletní kopie všech dat
    - Následné přírůstkové zálohy ukládají pouze změněné soubory od poslední zálohy
    - Nevýhoda: při obnově je třeba úplná záloha a všechny přírůstkové zálohy až k požadovanému bodu
2) **Úplná záloha + Rozdílová záloha**
    - Po úplné záloze každá rozdílová záloha obsahuje všechny změny od vytvoření úplné zálohy
    - Výhoda: obnova vyžaduje pouze úplnou zálohu a poslední rozdílovou zálohu
    - Proces je odolnější vůči poškození záložních médií
#### 2) Možnosti zotavení serveru
##### Příčiny havárie
- Chyby v softwaru, hardwaru
- Omyly uživatelů, správců
- Úmyslné poškození
- Vyšší moc
##### Obnova OS Windows Server
- Windows server obsahuje na instalačním DVD nástroj pro opravu v grafickém rozhraní
	- Tento nástroj umožňuje provést obnovu počítače pomocí dříve vytvořené bitové kopie a spustit příkazový řádek
#### 3) Možnosti zálohování ve Windows
##### Programy zálohování Windows
- Obraz systému (Ovládací Panely -> Zálohování a obnovení)
- Příkaz `robocopy`
- Případně programy třetích stran, které nabízejí daleko více možností
- Prostředí pro zotavení systému Windows
##### Stínové kopie
-  **Automaticky vytváří záložní kopie dat** **ve sdílených složkách** na vybraných svazcích NTFS v naplánovaných časech
- **Umožňuje uživatelům získávat předchozí verze souborů a složek**
##### Zálohování pevného disku
- Nástroj pro zálohování **umožnuje zálohovat soubory**, případně **vytvořit** a **použít zálohu obrazu** či **vytvořit disk pro opravu systému**
- Funkce historie souborů lze nastavit v `Nastavení -> Aktualizace a zabezpečení -> Zálohování
	- Zálohování souborů ve složkách dokumenty, hudba, obrázky, videa a plocha
	- Postupem času vytváří historii souborů
#### 4) Možnosti zálohování v UNIX-like OS – archivace, bitová kopie, rsync
##### UNIX-like OS - Archivace (Nástroj Tar)
- Dokáže **z více souborů vytvořit jeden samostatný soubor archivu**
- Nejpoužívanější je nástroj `Tar - Tape Archiver`, který mimo archivace dokáže **provádět i kompresi**
	- `Tar {volby} {soubory}` vytváří archiv tar (také označovaný jako tarballl)
	- Některé volby tohoto nástroje:
		1) Vytvoření archivu tar:
			- `--create` / `c` 
		2) Extrahování souborů z archivu:
			- `--extract` / `x`
		3) Připojení souborů, které jsou novější, než ty, co již v archivu jsou:
			- --`update` / `u`
	- Některé volby pro řízení činnosti tohoto nástroje:
		4) Před zahájení operace dojde k přepnutí do adresáře dir:
			- `--directory dir` / `C` 
		5)  Výpis všech přečtených nebo extrahovaných souborů):
			- `--verbose` / `v`
		6) Ověření archivu po zapsání:
			- `--verify` / `W` 
		7) Archivace:
			- `--{metoda archivace} (gzip, bzip2, xz)`
- Metody komprese:
	1) Gzip
		- Nejstarší s nejmenším kompresním poměrem
	2) Bzip2
		- Průměrný kompresní poměr
	3) Xz
		- Nejnovější s nejlepší kompresí
##### UNIX-like OS - Nátroj dd (Bitová kopie)
- **Zálohování celých disků** nebo **diskových oddílů**:
	- Řešení vhodné u nepřipojených zařízení, kde neprobíhají žádné I/O operace
- **Výsledný obraz bude mít stejnou velikost jako disk** a to i tehdy, pokud je disk prázdný
- Vytvoření souboru obrazu:
	- `dd if={disk} of={obraz}`
- Obnovení ze souboru obrazu:
	- `dd if={obraz} of={disk}`
##### UNIX-like OS - Rsync
- Nástroj pro **lokální i vzdálené kopírování souborů**, **ideální pro zálohování** a **synchronizaci souborů na síťové disky**:
	1) Synchronizace dvou místních adresářů nebo místních a vzdálených adresářů připojených v místním souborovém systému:
		- `rsync -av {source_directory} {destination} {directory}`
		- volba `-a` označuje rekurzivní synchronizaci, zachování symbolických odkazů, časových razítek, oprávnění a vlastníků jako uživatelů i skupiny
	2) Synchronizace místního adresáře se vzdáleným adresářem pomocí SSH: (místní adresář backups)
		- `rsync -avzhe ssh backups root@remote_host:/remote_directory/`
		- Volba `-e` pro vzdálený přístup pomocí SSH
	3) Synchronizace vzdáleného adresáře s místním adresářem přes SSH (vzdálený adresář backups)
		- `rsync -avzhe ssh root@remote_host:/remote_directory/ backups`
