#### 1) Správa diskových oddílů typu MBR a GPT v OS Windows a UNIX-like OS

##### Widnows - Správa disků
- Hlavním nástrojem pro správu disků je **modul snap-in konzoly MMC**, který je součástí **konzoly Správa počítače**
	- Zobrazení stavu disku, přiřazení a změnění písmena disku (mapování), přidání disků a diskových polí, nastavení diskového oddílu jako aktivního a inicializace disku
- Pro **vytvoření oddílu** a jeho **naformátování** lze použít i nástroj `diskpart.exe` a příkaz `Format`
- **Pro naformátování** disku lze použít i program Průzkumník Windows
##### Správa diskových oddílů typu MBR v OS Windows
- **Standard Master Boot Record** používá záznam **MBR**, který obsahuje informace o tom, **jak jsou na pevném disku rozloženy jednotlivé diskové oddíly**
	- Tento záznam má 512 B a obsahuje zavaděč (boot loader) v aktivním diskovém oddílu
	- Tento standard se používá zejména v počítačích s firmwarem typu BIOS
- Pokud je třeba na disku **vytvořit více než 4 oddíly** , pak je možné **jeden diskový oddíl nastavit jako rozšířený**
	- V rozšířeném oddílu se vytváří jednotlivé logické disky, které se používají pro oddělení dat pro účely správy
##### Správa diskových oddílů typu GPT v OS Windows
- Standard **GUID Partition Table** pro pevné disky v podobě **schématu založeném na tabulce oddílů**
	- Využívá celou řadu moderních technik, které rozšiřují možnosti staršího standardu MBR
	- Používá se na počítačích s UEFI
##### Správa diskových oddílů typu MBR v UNIX-like OS
- Nástroj `fdisk {název}` pro **správu disků MBR**
	- Aktuální partition table lze zobrazit klávesou `p`
	- Seznam všech typů diskových oddílů lze zobrazit klávesou `l`
	- Odstranění diskového oddílu klávesou `d`
	- Parametr `ld` lze ručně měnit klávesou `t`
	- Konečné úpravy se zapíší na disk klávesou `w`
##### Správa diskových oddílů typu GPT v UNIX-like OS
- nástroj `gdisk {název}` pro **správu disků GPT**
	- Lze použít pro vytvoření diskových oddílů GPT i MBR
	- Volby jsou velmi podobné volbám nástroji `fdisk`
#### 2) Charakteristika a konfigurace nejběžnějších souborových systémů v OS Windows a UNIX-like OS
##### Windows - Souborový systém
- Představuje **způsob ukládání** a **uspořádání souborů**
- Spravuje **fyzické umístění souborů**
- Windows podporuje:
	1) **FAT16**:
		- File Alocation Table
		- Jednoduchý souborový systém
		- podporuje pouze svazky o maximální velikosti 2 GB
	2) **FAT32**:
		- Maximální velikost souboru 4GB
		- Diskové oddíly do 2 TB
		- Nepodporuje šifrování ani oprávnění
	3) **NTFS**:
		- Upřednostňovaná souborový systém s názvem New Technology File System
		- podporuje disky s velikostí až 16 exabytů a dlouhé názvy souborů
		- Umožňuje ACL a šifrování
	4) **exFAT**:
		- Optimilalizovaný pro disky flash
		- Podpora souborů větších než 4 GB
		- Maximální velikost diskového oddílu je 16 EB
	5) **ReFS**:
		- optimalizován pro big data (ukkládání velkého množství dat ve velkém počtu souborů)
		- Maximální velikost souboru je 16 EB
		- Je určen pro datové disky, nelze z něj zavést operační systém
- Požadovaný souborový systém se zvolí v **Nástroji Správa Disků**
##### Unix-Like OS - Formátování diskových oddílů
- **Po vytvoření** diskových oddílů je třeba tyto diskové oddíly **naformátovat** (vytvořit na nich souborový systém)
	- Zobrazení seznamu podporovaných souborových systémů příkazem `ls /sbin/mk`
- Při výběru souborového systému je třeba zohlednit:
	- Podpora žurnálování:
		- Rychlejší obnova dat při pádu systému
	- Podporu SE Linuxu:
		- Security Enhanced Linux
- Mezi nejvyužívanější souborové systémy patří:
	1) **ext2**
		- Žádný žurnál, není odolný proti výpadkům
		- Rychlý zápis, vhodný pro flash paměti
		- Maximální velikost souboru 2 TB, omezená škálovatelnost
	2) **ext3**
		- Žurnálování, vyšší odolnost proti chybám
		- Kompatibilní s ext2
		- Slabší výkon než ext4, pomalejší při velkých souborech
	3) **ext4**
		- Větší soubory až 16 TB, vhodný pro moderní systémy
		- Rychlejší alokace bloků
		- Zpětně kompatibilní s ext2 a ext3
	4) **ReiserFS**
		- Efektivní pro malé soubory, dynamická alokace místa
		- Žurnálování, rychlá obnova po pádu
		- Zastaralý, vývoj prakticky ukončen
	5) **XFS**
		- Vysoký výkon, optimalizovaný pro velké soubory
		- Žurnálování na metadatech, rychlá obnova
		- Škálovatelný, podporuje velmi velké disky
	6) **FAT**
		- Maximální velikost souboru 4 GB u FAT32, omezená velikost
		- Široká kompatibilita, podporován všemi OS
		- Bez oprávnění a zabezpečení, méně vhodný pro moderní systémy
	7) **HPFS** / **NTFS** / **exFAT**
		- HPFS dříve pro OS/2, dnes zastaralý
		- NTFS podpora oprávnění, šifrování a velkých souborů
		- exFAT kompromis mezi FAT32 a NTFS, ideální pro flash disky
- Příkaz `mkfs -t {souborový systém} -L {popisek} {diskový oddíl}` pro formátování diskového oddílu
- **Alternativně** lze využít **nástroj Disks** (GUI), kterým lze následující:
	- Správa diskových oddílů
	- připojování a odpojování disků
	- formátování diskových oddílů
	- dotazování se na stav disku technologií S.M.A.R.T. (Self Monitoring, Analysis and Reporting Technology)
#### 3) Nástroje pro sledování využití kapacity disků v OS Windows a UNIX-like OS
##### UNIX-Like OS - Nástroje pro sledování využití kapacity disků
1) Příkaz `df` (**disk free**)
	- Celkové využití disku souborovým systémem v bajtech, celkovou velikost souborového systému, volný a obsazený prostor a mount point každého úložiště
	- Příznak `-h` pro human-readable formu
2) Příkaz `du` (**disk usage**)
	- Lze použít pro zjištění, které soubory zabírají nejvíce místa
##### Windows OS - Nástroje pro sledování využití kapacity disků
1) **Správa disků**: (**Modul **snap-in** Konzoly **MMC** - **)
	- Poskytuje podrobnější informace o alokovaném prostoru na discích a diskových oddílech
2) **Průzkumník souborů**:
	- Zobrazuje využité a volné místo na každém disku v systému
3) **Příkazový řádek**:
	- Wmic a fsutil
4) **PowerShell**:
	- Get-Psfrive a Get-Volume