#### 1) Typy a charakteristika místních a síťových úložišť, diskové pole RAID a jeho varianty
##### Typy úložišť pro pevné disky ve Windows
1) **Základní disky**
	- Primární oddíly, rozšířené oddíly s logickými jednotkami
	- MBR nebo GPT
	- Běžné úlohy jako instalace OS, ukládání dat
2) **Dynamické disky**:
	- Používají se pro vytvoření **softwarového diskového pole RAID**
	- Je možné **měnit velikost bez nutnosti restartu**
	- Lze vytvářet následujících **pět typů svazků**:
		1) Jednoduchý svazek
		2) Rozložený svazek
		3) Prokládaný svazek
		4) Zrcadlený svazek
		5) Svazek typu RAID 5
##### Charakteristika místních úložišť
1) **HDD** (Hard Disk Drive):
	-  Z **poloviny elektronické** a z **poloviny mechanické** zařízení, které pro princip ukládání dat na otáčející se plotně využívají princip magnetického záznamu
2) **SSD** (Solid State Drive):
	-  Zařízení, které je **čistě elektronické**
##### Charakteristika síťových úložišť
1) **SAN** (Storage Area Network)
	- Architektura používaná u diskových polí, páskových či optických knihoven, které se jeví jako disky připojené přímo k serveru
	- Vždy používají diskové pole `RAID` nebo obdobnou technologii včetně spare drives
	- Kvůli zajištění maximální rychlosti používají protokol `SCSI` (iSCSI) nebo rozhraní Fibre Channel
2) **NAS** (**Network Attached Storage**)
	- Úložiště pracující na úrovni souborů, které se připojuje k počítačové sítí
	- Realizováno obvykle pomocí protokolu `SMB`
	- Obsahuje několik disků zapojených v diskovém poli `RAID`
3) **Komunikační rozhraní** (Slouží ke komunikaci serveru se vzdáleným úložištěm, jako by nebylo vzdálené):
	- **Fibre Channel**:
		- Přenosové rychlost až `128 Gb/s`
		- Transportní protokol `FCP` (Fibre Channel Protocol), který umožňuje používání příkazů `SCSI`
	- **ISCSI** (Internet Small Computing System Interface):
		- Síťový standard založený na protokolu `IP`
		- Používaný pro propojení datových úložišť
	- **SCSI** (Small Computing System Interface):
		- Standardní rozhraní a sad příkazů pro výměnu dat mezi externími zařízeními a počítačovou sběrnicí
##### Disková pole - RAID (Redundant Array of Independent Disks)
- Diskové pole, které používá **současně dva či více disků**, z nichž vytvoří **systém odolný vůči selhání disků** a s **maximálním výkonem** 
- Lze **realizovat jak softwarově**, **tak hardwarově**
##### RAID 0 (Prokládání - Stripping)
- **Ukládá data rovnoměrně na všechny disky**, které vytváří jeden velký virtuální souborový systém, kde jsou všechny jednotlivé bloky rozprostřeny přes všechny disky
- **Neexistuje možnost kontroly** paritou ani odolnost vůči chybám
- Výhodou je **vysoký výkon**
##### RAID 1 (Zrcadlení disku)
- Při zrcadlení disku se **kopíruje obsah disku nebo diskového oddílu na další disk**
- Data se ukládají **oba disky současně**
- Při havárii jednoho disku počítač **přistupuje k datům uloženým na druhém disku**
- Výhodou je **rychlost čtení**
##### RAID 5
- Jeden disk se použije pro **uložení paritních dat**, který **zajišťuje odolnost diskového pole vůči chybám**
- **Paritní data** se ukládají na **všechny disky** kvůli **maximalizaci výkonu**
- Při selhání jednoho disku je možné pokračovat v daném úkonu, díky výpočtům parity z dat na zbývajících discích se zabrání ztrátě dat
##### Hybridní RAID
- **RAID 1 + RAID 0**:
	- Zrcadlená sada (1), na níž se provádí prokládání (0)
- **RAID 0 + RAID 1**:
	- Prokládaná sada (0), na níž se provádí zrcadlení (1)
##### Hot Spare
- **Náhradní disk**, kterým je možné **za běhu nahradit vadný disk**
- Lze kombinovat s diskovým polem RAID
- Po selhání disku si server automaticky vezme náhradní disk, kterým jej nahradí a následně obnoví chybějící data
#### 2) Konfigurace diskového pole RAID ve Windows a v UNIX-like OS
##### Windows OS
1) **Disk Management**
2) **Inicializace disku** (MBR nebo GPT)
3) **Převod na dynamický disk** - New RAID-5 Volume (vybrání disků, celkem tři)
4) **Vytvoření jednoduchého svazku**
5) **Přiřazení identifikátoru** (písmena) jednotky nebo cesty
6) **Formátování disku** (NTFS, exFAT, FAT32, FAT16)
7) **Zvětšení svazku**
##### UNIX-Like OS
1) **Vytvoření diskového pole příkazem**  `mdadm`
	- `mdadm -create -verbose {disk1} -level=stripe -raid-devices=2 {disk2} {disk3}`
2) **Ověření vytvoření pole RAID**:
	-  `mdadm --detail {disk}` nebo `cat /proc/mdstat`
3) **Formátování zařízení požadovaným souborovým systémem**
	- Vytvoření diskových oddílů, formátování souborových systémů, konfigurace oddílů swap
4) **Sledování činnosti pole monitorovací službou**
	- Přidání výstupu z příkazu `mdadm --detail --scan` do souboru `/etc/mdadm/mdadm.conf`
5) **Složení diskového pole z existujících komponent**
	- `mdadm -assemble -scan`
6) **Zajištění spuštění služby při startu počítače**
	- `update-rc.d mdadm defaults` a přidáním řádku `AUTOSTART=true` do souboru `/etc/default/mdadm`
- Rozpojit diskové pole pole lze následujícími způsoby:
	- `mdadm --stop {disk}` pro zastavení
	- `mdadm --remove` pro odebrání
#### 3) Konfigurace prostor úložiště ve Windows a LVM v UNIX-like OS
##### Windows - Vytváření diskových oddílů
- **Při vytváření diskových oddílů dochází k dělení fyzického disku na logické jednotky** (diskové oddíly):
	- Každý diskový oddíl se chová jako samostatný disk ke kterému je možné přidělit jedinečný identifikátor
- Způsob rozdělení disku se nachází v tabulce **partition table**
	- Při formátování disku se vytváří souborový systém svazku vytvořením tabulky metadat a dat pro alokaci souborů (File Allocation Table, která udává umístění souborů a složek ve svazku)
##### Windows - Konfigurace Prostoru úložiště
- **Nástroj správa disků**
- Prostory úložiště jsou technologií diskového pole doporučovanou operačním systémem Windows
	- Vytváří **fondy fyzických pevných disků**, z nichž je následně možné **vytvořit virtuální disky** (prostory úložiště)
##### Windows - Způsoby vytváření diskových oddílů
1) **Master Boot Record** (MBR):
	- Záznam **MBR**, který obsahuje informace o tom, jak jsou na pevném disku rozloženy jednotlivé diskové oddíly
	- Tento záznam má `512B` a obsahuje zavaděč (`boot loader`) v aktivním diskovém oddílu
	- Tento standard se používá zejména v počítačích s firmwarem typu `BIOS`
 2) **GUID Partition Table** (GPT):
	 - **GUID Partition Table** pro pevné disky v podobě **schématu založeném na tabulce oddílů**
	- Využívá celou řadu moderních technik, které rozšiřují možnosti staršího standardu MBR
	- Používá se na počítačích s UEFI
##### Unix-Like OS - Logical volume Management (LVM)
- **Řešení pro správu místa v uložištích**, hlavní výhodou je **možnost měnit velikost vzniklých logických celků**
- Struktura LVM:
	1) **Fyzické svazky** `Physical Volume`
		- (Celé pevné disky nebo diskové oddíly)
			- `pvcreate {disk1} {disk2} ...` pro vytvoření fyzických svazků
			- `pvs` pro výpis vytvořených fyzických svazků
			- `pvdisplay {disk}` pro výpis podrobných informací na daném disku
	2) **Skupina svazků** `Volume Group`:
		- Jednotka úložiště vzniklá z jednoho nebo více fyzických svazků:
			- `vgcreate {name} {disk1} {disk2}` pro vytvoření skupiny fyzických svazků
			- `vgextend {VG} {disk}` pro přidání dalšího fyzického svazku
	3) **Logický svazek** `Logical Volume`:
		-  Vytváří se ve skupině svazků a odpovídá svým způsobem diskovému oddílu
			- `lvcreate -n {nazev} -L {velikost svazku} {skupina svazků}` pro vytvoření logického svazku
			- `lvs` pro zobrazení seznamu logických svazků
			- `lvdisplay {VG/LV}` 
			- `lvreduce -L {velikost} -r {VG/LV}` 
			- `lvextend -L {velikost} -r {VG/LV}`

> Aby bylo možné logické svazky používat, je třeba je nejprve naformátovat, poté  **identifikovat** (`blkid`) a vytvořit pro ně **mountpointy** a upravit soubor `/etc/fstab`. (`UUID={UUID} {Bod připojení} {File system} defaults 0 0`)
	- `mount -a` pro uložení změn a připojení logických svazků