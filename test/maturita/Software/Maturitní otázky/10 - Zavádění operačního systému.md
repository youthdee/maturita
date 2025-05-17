#### 1) Popis spouštěcí sekvence v OS Windows
##### Spouštěcí sekvence v OS Windows
- Po absolvování **POST** (**Power On Self Test**) **vyhledá BIOS** a **načte nastavení konfigurace**  **z paměti CMOS**
	- Jedním z nich je pořadí vyhledávání disků pro zavedení operačního systému (boot device priority):
		- Během něhož se vyhledává diskový oddíl, z něhož lze zavést operační systém
		- Systém BIOS spouští počítač z prvního disku, který obsahuje platný zaváděcí sektor
		- Jedná se o sektor obsahující záznam MBR (Master Boot Record) nebo GPT
			- Který obsahuje informace o VBR (Volume Boot Record), který načítá příslušného správce spouštění (`bootmgr.exe`)
- Operační systém lze zavést z **pevných disků**, **síťových disků**, **USB disků** včetně **vyměnitelných médií** (To vše závisí na **funkcích základní desky**)
#### 2) Popis spouštěcí sekvence v UNIX-like OS
##### UNIX-Like OS -  Zavádění operačního systému (bootování)
- Po zapnutí se spustí **firmware uložený v paměti EEPROM**, který spustí test **POST** (Power On Self Test), který **zkontroluje funkčnost hardwaru**
- Následně **vyhledá zavaděč**, který se nachází v **MBR** nebo **diskovém oddílu EFI** na **prvním disku** a předá mu řízení:
	- Master Boot Record (MBR) je záznam o velikosti 512 B, který se nachází na prvním sektoru disku
		- Obsahuje spustitelný kód a tabulku oddílů (partition table), kde se nachází záznamy pro každý diskový oddíl (jeho velikost, počáteční a konečný sektor)
	- V případě EFI/UEFI, tak načte UEFI své nastavení, z něhož zjistí umístění oddílu EFI (disk a diskový oddíl) a jakou aplikaci má spustit
- V dalším kroku se **načte a spustí správce spouštění** (boot manager) **GRUB**:
	- Konfiguračního souboru GRUB2 s názvem `/etc/default/grub`
	- Změny lze možné aktivovat příkazem `update-grub`
	- GRUB načítá Kernel a obraz initrd nebo initramfs, které pomáhají při detekci hardwaru, načítání modulů Kernelu a detekci zařízení nutných pro připojení kořenového souborového systému
- Po **aktivaci souborového systému** **Kernel spustí správce systému a služeb** (**init** nebo **systemd** s PID 1), které **zajistí zobrazení uživatelského rozhraní**
	- Jedná se o deamony spravující ostatní deamony jak při spuštění, tak vypínání systému
#### 3) Správci spouštění v OS Windows a UNIX-like OS, možnosti úprav zavádění operačního systému
##### Možnosti zavedení operačního systému - OS Windows
- Režimy spouštění ve Windows 7 (Vybrat režim lze klávesou F8 při spouštění počítače):
	1) **Nouzový režim**
		- Diagnostický režim pro řešení problémů s operačním systémem a jeho spouštěním
		- Funkčnost je omezená
	2) **Nouzový režim se sítí**
		- Nouzový režim s podporou konektivity do počítačové sítě
	3) **Nouzový režim s příkazovým řádkem**
		- Operační systém Windows v CLI
	4) **Poslední známá funkční konfigurace**
		- Načte konfiguraci použitou při posledním úspěšném zavedení operačního systému
- Režimy spouštění ve Windows 8 a Windows 10 a Windows 11 (**Vybrat režim lze držením klávesy shift a položky restartovat**)
- Příslušná možnost spuštění se vybere stiskem jedné z kláves **F1-F9**:
	- 1) Enable debugging
	- 2) Enable boot logging
	- 3) Enable low-resolution video
	- 4) Enable Safe Mode
	- 5) Enable Safe Mode with Networking
	- 6) Enable Safe Mode with Command Prompt
	- 7) Disable driver signature enforcment
	- 8) Disable early launch anti-malware protection
	- 9) Disable automatic restart after failure
##### Windows Boot Manager (bootmgr.exe)
- **Primární součástí zavádějícího procesu** ve Windows
- Nachází se v **kořenovém adresáři zaváděcího oddílu**
- Odpovídá za **načtení bootovacího zavaděče OS**
##### OS Windows - Boot Configuration Data (BCD)
- **Nahrazuje** starý "**boot.ini**"
- Obsahuje **konfiguraci pro spouštění Windows**
##### Windows Boot Loader (winload.exe)
- Zodpovídá za **načtení jádra systému** (**ntoskrnl.exe**), **ovladačů** a **dalších komponent OS**
##### Správci spouštění v UNIX-like OS
- V Linuxu se používá systém **runlevelů**, které umožňují **nastavit**, které služby se budou **v daném** **runlevelu** **spouštět**
- V současnosti se používá **správce systému systemd**, který kvůli **zachování kompability podporuje** i **příkazy sysv**
- Po svém spuštění se **proces init zařídí podle souboru** `/etc/inittab`, kde je uvedeno, **do jakého runlevelu má systém zavést**
- **Runlevely**:
	1) `0` (vypnutí systému)
	2) `1` (maintanace mode, spouští se minimum deamonů, pro řešení problémů)
	3) `2` (multiuser, umožňuje zavést GUI)
	4) `3` (U Redhatu výchozí multiuser režim bez GUI, u debianu se nepoužívá)
	5) `4` (Obvykle se nepoužívá, k dispozici pro vlastní řešení)
	6) `5` (U RedHatu se jedná o runlevel 3 s podporou GUI)
	7) `6` (restartování systému)
- Přepnutí do jiného runlevelu příkazem `init {číslo runlevelu}`
- Lepším řešením je **upravit v souboru** `/etc/inittab` číslo runlevelu na řádku `id:{číslo}:initdefault:`
- **Povolení** či **zákaz spouštění služeb při spouštění**:
	- `chkconfig` (CentOS) 
	- `sysv-rc-conf` (Debian)
##### Správci spouštění v UNIX-like OS - systemd
- Používá **paralelní spouštění procesů** a používá **dynamickou správu prostředků**
	- Služby se spouští v případě potřeby
- Nástroj `systemctl` pro zobrazení stavu procesů s volbami:
	1) `start`
	2) `restart`
	3) `status`
	4) `stop`
	5) `enable`
	6) `disable`
	7) `is-enabled`
- Runlevely jsou nahrazeny **targetami**:
	1) `Runlevel 0` <=> `poweroff.target`
	2) `Runlevel 1` <=> `rescue.target`
	3) `Runlevel 3` <=> `multi-user.target`
	4) `Runlevel 5` <=> `graphical.target`
	5) ``Runlevel 6`` <=> `reboot.target`
	6) `Emergency` <=> `emergency.target`
- **Při spouštění systému** se aktivuje `default.target`, který **spustí služby a další položky**, které na nich závisí
- **Zobrazení** default targetu:
	- `systemctl get-default`
- **Nastavení** default targetu:
	- `systemctl set-default {target}`
##### Správci spouštění v UNIX-like OS - Upstart
- **Náhrada** za deamona `/sbin/init` s cílem **zajistit spouštění služeb jen tehdy, kdy je potřeba**, sledovat spuštěné služby a zpracovat události v okamžiku kdy se objeví, **s cílem obejít klasický systém sysvinit** založený na závislostech
- Postupem času byl zastíněn deamonem systemd