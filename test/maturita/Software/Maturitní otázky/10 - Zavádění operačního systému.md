#### 1) Popis spouštěcí sekvence v OS Windows

##### Spouštěcí sekvence v OS Windows
- Po absolvování testu POST (Power On Self Test) vyhledá BIOS a načte nastavení konfigurace uložené v paměti CMOS
	- Jedním z nich je pořadí vyhledávání disků pro zavedení operačního systému (boot device priority), během něhož se vyhledává diskový oddíl, z něhož lze zavést operační systém
	- Systém BIOS spouští počítač z prvního disku, který obsahuje platný zaváděcí sektor
	- Jedná se o sektor obsahující záznam MBR (Master Boot Record)
		- Který obsahuje informace o VBR (Volume Boot Record), který načítá příslušného správce spouštění (V OS Windows to je bootmgr.exe)
- Operační systém lze zavést z pevných disků, síťových disků, USB disků včetně vyměnitelných médií (To vše závisí na funkcích základní desky)
#### 2) Popis spouštěcí sekvence v UNIX-like OS

##### UNIX-Like OS -  Zavádění operačního systému (bootování)
- Po stisku tlačítka pro zapnutí počítače se spustí firmware uložený v paměti EEPROM, který spustí test POST (Power On Self Test), který zkontroluje funkčnost hardwaru počítače
- Následně vyhledá zavaděč, který se nachází v MBR nebo diskovém oddílu EFI na prvním disku a předá mu řízení
	- Master Boot Record (MBR) je záznam o velikosti 512 B, který se nachází na prvním sektoru disku označovaného v BIOSU jako disk, z něhož lze zavést operační systém
		- Obsahuje spustilený kód a tabulku oddílů (partition table), kde se nachází záznamy pro každý diskový oddíl (jeho velikost, počáteční a konečný sektor)
		- Doporučuje se provést zálohu MBR z níž je možné MBR při poškození obnovit
	- Pokud se používá EFI/UEFI, tak načte UEFI své nastavení, z nehož zjistí umístění oddílu EFI (disk a diskový oddíl) a jakou aplikaci má spustit
- V dalším kroku se načte a spustí správnce spouštění (boot manager) GRUB (Grand Unified Boot)
	- U starších distribucí nepodporujících EFI/UEFI ve verzi GRUB legacy se načte a spustí konfigurační soubor /boot/grub/menu.lst
	- V podobě konfiguračního souboru GRUB2 s názvem /etc/default/grub
	- Změny lze možné aktivovat příkazem "update-grub"
	- GRUB načítá Kernel a obraz initrd nebo initramfs, které pomáhají při detekci hardwaru, načítání modulů Kernelu a detekci zařízení nutných pro připojení kořenového souborového systému
- Po aktivaci souborového systému Kernel spustí správce systému a služeb (init nebo systemd s PID 1), které zajistí zobrazení uživatelského rozhraní
	- Jedná se o deamony spravující ostatní deamony jak při spuštění, tak vypínání systému

#### 3) Správci spouštění v OS Windows a UNIX-like OS, možnosti úprav zavádění operačního systému

##### Správci spouštění v UNIX-like OS
- V Linuxu se používá systém runlevelů, které umožňují nastavit, které služby se budou v daném stavu (runlevelu) spouštět
- V současnosti se používá správce systému systemd, který kvůli zachování kompability podporuje i příkazy sysv
- Po svém spuštění se proces init zařídí podle souboru /etc/inittab, kde je zapsáno, do jakého runlevelu má systém zavést
- Runlevely:
	- 0 (vypnutí systému)
	- 1 (maintanace mode, spouští se minimum deamonů, pro řešení problémů)
	- 2 (multiuser, umožňuje zavést GUI)
	- 3 (U Redhatu výchozí multiuser režim bez GUI, u debianu se nepoužívá)
	- 4 (Obvykle se nepoužívá, k dispozici pro vlastní řešení)
	- 5 (U RedHatu se jedná o runlevel 3 s podporou GUI)
	- 6 (restartování systému)
- Přepnout do jiného runlevelu lze příkazem "init {číslo runlevelu}"
- Lepším řešením je upravit v souboru "/etc/inittab" číslo runlevelu na řádku "id:{číslo}:initdefault:"
- Povolení či zákaz spouštění služeb při spouštění se konfiguruje příkazem chkconfig (CentOS) nebo sysv-rc-conf (Debian)
- V Ubuntu 14.04 byl soubor "/etc/inittab" nahrazen "/etc/init/rc-sysinit.conf"

##### Správci spouštění v UNIX-like OS - systemd
- Narozdíl od sysvinit používá paralelní spouštění procesů a používá dynamickou správu prostředků (služby se spouští až v případě potřeby)
- Stav procesů v systému se zobrazí příkazem "systemctl" s volbami:
	- start
	- restart
	- status
	- stop
	- enable
	- disable
	- is-enabled
- Runlevely jsou nahrazeny targetami:
	- Runlevel 0 <=> poweroff.target
	- Runlevel 1 <=> rescue.target
	- Runlevel 3 <=> multi-user.target
	- Runlevel 5 <=> graphical.target
	- Runlevel 6 <=> reboot.target
	- Emergency <=> emergency.target
- Při spouštění systému se aktivuje default.target, který má za úkol spustit služby a další položky, které na nich závisí
- Zobrazení default targetu příkazem "systemctl get-default"
- Nastavení default targetu příkazem "systemctl set-default {target}"

##### Správci spouštění v UNIX-like OS - Upstart
- Náhrada za deamona "/sbin/init" s cílem zajistit spouštění služeb jen tehdy, kdy je potřeba, sledovat spuštěné službya zpracovat události v okamžikum kdy se objeví s cílem obejít klasický systém sysvinit založený na závislostech
- Vyvinut původně pro Ubuntu, používá v Red Hat Enterprise Linux 6.0
- Postupem času byl zastínen deamonem systemd, který se nyní používá v ubuntu
	- Zachovává podporu spouštěcích skriptů SysV
	- zajišťuje režim kompability, kdy pokud pro případ, že u balíčku není k dispozici konfigurační skript Upstart, použije se spouštěcí skript SysV
- Skripty Upsatrt dokáží spustit či zastavit služby na základě více akcí, než spouštěcí skripty SysV (např. Upstart dokáže spustit službu kdykoliv po připojení nového hardwaru)
- Upstart namísto souboru "/etc/inittab" a adresářů spouštějících skriptů SysV používá skripty ".conf" (job definitions) v adresáři "/etc/init", které obsahují:
	- popis procesu
	- runlevely, v nichž by měl být proces spuštěn/zastaven a události, které vyvolají spuštění/zastavení procesu
	- volby
	- příkaz pro spuštění procesu
- Pro uložení změn je třeba upstart restartovat příkazem "initctl reload-configuration"
- Spustit úlohu pomocí Upstart lze příkazem "sudo start {uloha}"

##### Možnosti zavedení operačního systému - OS Windows
- Režimy spouštění ve Windows 7 (Vybrat režim lze klávesou F8 při spouštění počítače):
	- Nouzový režim
		- Diagnostický režim pro řešení problémů s operačním systémem a jeho spouštěním
		- Funkčnost je omezená
	- Nouzový režim se sítí
		- Zavede se Nouzový režim s podporou konektivity do počítačové sítě
	- Nouzový režim s příkazovým řádkem
		- Zavede se operační systém Windows ale v CLI
	- Poslední známá funkční konfigurace
		- Načte konfiguraci použitou při posledním úspěšném zavedení operačního systému
- Režimy spouštění ve Windows 8 a Windows 10 a Windows 11 (Vybrat režim lze držením klávesy shift a položky restartovat)
	- Možnosti spouštění lze zobrazit pod možností Odstranit Potíže -> Rozšířené možnosti -> Nastavení pro spuštění -> Restartovat (Počítač se restartuje a poté zobrazí nabídku Nastavení pro spouštění)
	- Příslušná možnost spuštění se vybere stiskem jedné z kláves F1-F9:
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
- Primární součástí zavádějícího procesu ve Windows
- Nachází se v kořenovém adresáři zaváděcího oddílu
- Odpovídá za načtení bootovacího zavaděče OS

##### OS Windows - Boot Configuration Data (BCD)
- Nahrazuje starý "boot.ini"
- Obsahuje konfiguraci pro spouštění Windows

##### Windows Boot Loader (winload.exe)
- Zodpovídá za načtení jádra systému (ntoskrnl.exe), ovladačů a dalších komponent OS