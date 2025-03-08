#### 1) Typy a charakteristika místních a síťových úložišť, diskové pole RAID a jeho varianty

##### Stavba Disku
- Inicializace disku (MBR nebo GPT) pro způsob vytváření diskových oddílů
- Vytvoření oddílů
- Naformátování oddílů

##### Typy úložišť pro pevné disky ve Windows
- Základní disky
- Dynamické disky
	- Používají se pro vytvoření softwarového diskového pole RAID
	- je možné měnit velikost bez nutnosti restartu operačního systému
	- Lze vytvářet následujících pět typů svazků:
		- Jednoduchý svazek
		- Rozložený svazek
		- Prokládaný svazek
		- Zrcadlený svazek
		- Svazek typu RAID 5

##### Charakteristika místních úložišť
- HDD (Hard Disk Drive) je z poloviny elektronické a z poloviny mechanické zařízením která pro princip ukládání dat na otáčející se plotně využívají princip magnetického záznamu
- SSD (Solid State Drive) je zařízení, které je čistě elektronické
##### Charakteristika síťových úložišť
- SAN (Storage Area Network)
	- Architektura používaná u diskových polí, páskových či optických knihoven, které se pak jeví jako disky připojené přímo k serveru
	- Vždy používají nějakou podobu diskového pole RAID, případně nějakou jinou technologii, která zajistí redundanci
	- Obvykle obsahuje náhradní disky (spare drives)
	- Kvůli zajištění maximální rychlosti používají protokol SCSI (iSCSI) nebo rozhraní Fibre Channel
	
- NAS (Network Attached Storage)
	- Úložiště pracující na úrovni souborů, které se připojuje k počítačové sítí
	- Umožňuje přistupovat k uloženým sdíleným diskům či složkám
	- Realizováno obvykle pomocí protokolu SMB
	- Obvykle obsahuje několik disků zapojených v diskovém poli RAID
	- Obvykle se tato úložiště spravují přes webové rozhraní
- Fibre Channel
	- Komunikační rozhraní o přenosové rychlosti až 128 Gb/s
	- Používá transportní protokol FCP (Fibre Channel Protocol), který umožňuje používání příkazů SCSI
- ISCSI (Internet Small Computing System Interface)
	- Síťový standard založený na protokolu IP
	- Používaný pro propojení datových úložišť
- SCSI (Small Computing System Interface)
	- Standardní rozhraní a sad příkazů pro výměnu dat mezi externími zařízeními a počítačovou sběrnicí

##### Disková pole - RAID (Redundant Array of Independent Disks)
- Diskové pole, které používá současně dva či více disků, z nichž vytvoří systém odolný vůči selhání disků a s maximálním výkonem 
- Diskové pole lze realizovat jak softwarově, tak hardwarově

##### RAID 0 (Prokládání - Stripping)
- Ukládá data rovnoměrně na všechny disky, které vytváří jeden velký virtuální souborový systém, kde jsou všechny jednotlivé bloky rozprostřeny přes všechny disky
- Neexistuje možnost kontroly paritou ani odolnost vůči chybám
- Nejedná se tedy o skutečnou podobu diskového pole RAID
- Výhodou je vysoký výkon

##### RAID 1 (Zrcadlení disku)
- Při zrcadlení disku se kopíruje obsah disku nebo diskového oddílu na další disk
- Při ukládání se tedy tato data ukládají na oba disky současně
- Při havárii jednoho disku počítač přistupuje k datům uloženým na druhém disku
- Výhodou je rychlost čtení

##### RAID 5
- Podobný RAIDU 0
- Jeden disk se použije pro uložení paritních dat (oprava chyb), který zajišťuje odolnost diskového pole vůči chybám
- Paritní data se ukládají na všechny disky kvůli maximalizaci výkonu (Aby výpočet paritiy nezůstával pouze na jednom disku)
- Při selhání jednoho disku je možné pokračovat v daném úkonu, díky výpočtům parity z dat na zbývajících discích se zabrání ztrátě dat

##### Hybridní RAID
- RAID 1 + RAID 0
	- Zrcadlená sada (1), na níž se provádí prokládání (0)
- RAD 0 + RAID 1
	- Prokládaná sada (0), na níž se provádí zrcadlení (1)

##### Hot Spare
- Náhradní disk, kterým je možné za běhu nahradit vadný disk
- Tento disk lze kombinovat s diskovým polem RAID
- Po selhání disku si server automaticky vezme náhradní disk, kterým jej nahradí a následně obnoví chybějící data

#### 2) Konfigurace diskového pole RAID ve Windows a v UNIX-like OS

##### Windows OS
- Disk Management
- Inicializace disku (MBR nebo GPT)
- Převod na dynamický disk - New RAID-5 Volume (vybrání disků, celkem tři)
- Vytvoření jednoduchého svazku
- Přiřazení identifikátoru (písmena) jednotky nebo cesty
- Formátování disku (NTFS, exFAT, FAT32, FAT16)
- Zvětšní svazku
##### UNIX-Like OS
1) Vytvoření diskového pole příkazem "mdadm" 
	- mdadm -create -verbose {disk1} -leveléstripe -radi.-devices=2 {disk2} {disk3}
2) Ověření vytvoření pole RAID příkazy "mdadm -detail {disk}" nebo "cat /proc/mdstat"
3) Formátování zařízení požadovaným souborvým systémem (vytvoření diskových oddílů, formátování souborových systémů, konfigurace oddílů swap)
4) Sledování činnosti pole monitorovací službou
	- A přidání výstupu z příkazu "mdadm --detail --scan" do souboru "/etc/mdadm/mdadm.conf"
5) Složení diskového pole z existujících komponent ("mdadm -assemble -scan")
6) Zajištění spuštění služby při startu počítače
	- příkazem "update-rc.d mdadm defaults" a přidáním řádku "ATUOSTART=true" do souboru "/etc/default/mdadm" 
- U variant RAID s podporou redundance lze při poškození některého z disků provést automatickou náhradu, ale pouze jen tehdy, pokud byl náhradní disk přidán už při prvním vytvoření diskového pole
	- V opačném případě je třeba přidat nový disk do počítače ručně a poté spustit příkaz "mdadm {disk-chyba} -add {nahradni-disk}"
- Rozpojit diskové pole pole lze následujícími způsoby:
	- příkaz "mdadm --stop {disk}" pro zastavení
	- příkaz "mdadm --remove" pro odebrání

##### UNIX-Like OS - Varianty diskového pole RAID
- RAID 0 (využití u real-time aplikací, kde je výkon důležitější)
	- mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=2 /dev/sdb1 /dev/sdc1
-  RAID 1 (využití disků s operačním systémem a důležitých podadresářů)
	- mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
- RAID 5 (webové a souborové servery)
	- mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1 --spare-devices=1 /dev/sde1
- RAID 6 (využití u souborových serverů a zálohovacích serverů s požadavky na vysokou dostupnost)
	- mdadm --create --verbose /dev/md0 --level=6 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 --spare-devices=1 /dev/sdf1
- RADI 1 + RAID 0 (Využití u databázových a aplikačnich serverů vyžadujícíh rychlé I/O operace)
	- mdadm --create --verbose /dev/md0 --level=10 --raid-devices=4 /dev/sd[be]1 --spare-devices=1 /dev/sdf1
#### 3) Konfigurace prostor úložiště ve Windows a LVM v UNIX-like OS

##### Windows - Stavba disku
- Na každém disku je třeba před prvním použitím vytvořit diskové oddíly nebo svazky a naformátovat je
- Aby byl disk použitelný, je třeba nejdříve:
	- Inicializovat disk (MBR nebo GPT)
	- Vytvořit oddíly (svazky)
	- Naformátovat oddíly (vytvořit souborový systém)

##### Windows - Vytváření diskových oddílů
- Při vytváření diskových oddílů dochází k dělení fyzického při virtuálního disku na logické jednotky (diskové oddíly)
- Každý diskový oddíl se chová jako samostatný disk ke kterému je možné přidělit jedinečný identifikátor (písmeno)
- Způsob rozdělení disku se nachází v tabulce "partition table"
- Při formátování disku se vytváří souborový systém svazku vytvořením tabulky metadat a dat pro alokaci souborů (File Allocation Table, která udává umístění souborů a složek ve svazku)

##### Windows - Konfigurace Prostoru úložiště
- Nástroj správa disků
- Prostory úložiště jsou technologií diskového pole doporučovanou operačním systémem Windows
	- Vytváří fondy fyzických pevných disků, z nichž je následně možné vytvořit virtuální disky (prostory úložiště)
##### Windows - Způsoby vytváření diskových oddílů
- Master Boot Record (MBR)
- GUID Partition Table (GPT)

##### Unix-Like OS - Logical volume Management (LVM)
- Řešení pro správu místa v uložištích, hlavní výhodou je možnost měnit velikost vzniklých logických celků
- Struktura LVM:
	- Fyzické svazky "PV" (Celé pevné disky nebo diskové oddíly)
		- Příkaz "pvcreate {disk1} {disk2} ..." pro vytvoření fyzických svazků
		- Příkaz "pvs" pro výpis vytvořených fyzických svazků
		- Příkaz "pvdisplay {disk}" pro výpis podrobných informací na daném disku
	- Skupina svazků "VG" (Jednotka úložiště vzniklá z jednoho nebo více fyzických svazků)
		- Příkaz "vgcreate {name} {disk1} {disk2}" pro vytvoření skupiny fyzických svazků
		- Příkaz "vgextend {VG} {disk}" pro přidání dalšího fyzického svazku
	- Logický svazek "LV" (Vytváří se ve skupině svazků a odpovídá svým způsobem diskovému oddílu)
		- Příkaz "lvcreate -n {nazev} -L {velikost svazku} {skupina svazků}" pro vytvoření logického svazku
		- Příkaz "lvs" pro zobrazení seznamu logických svazků
		- Příkaz "lvdisplay {VG/LV}" pro zobrazení podrobných informací
		- Příkaz "lvreduce -L {velikost} -r {VG/LV}" pro zmenšení logického svazku
		- Příkaz "lvextend -L {velikost} -r {VG/LV}" pro zvětšení logického svazku
- Aby bylo možné logické svazky používat, je třeba je nejprve identifikovat (pomocí UUID) a vytvořit pro ně body připojení a upravit soubor "/etc/fstab"
- Nakonec je třeba logické svazky připojit a přiřadit vhodná oprávnění
	- Příkaz "blkid {VG/LV}" pro zjištění UUID
	- Příkaz "mkdir {cesta}" pro vytvoření bodů připojení
	- Příklad konfigurace v "/etc/fstab"
		- "UUID={UUID} {Bod připojení} {File system} defaults 0 0"
	- Příkaz "mount -a" pro uložení změn a připojení logických svazků