#### 1) Popis spouštěcí sekvence v OS Windows
##### Spouštěcí sekvence v OS Windows
1) `POST` (Power On Self Test)
2) `BIOS` vyhledá a načte konfiguraci z paměti `CMOS`
3) Zjistí pořadí vyhledávání disků pro zavedení OS (**boot device priority**)
4) Vyhledává diskový oddíl, ze kterého lze zavést OS
5) Spouští počítač z prvního disku s platným zaváděcím sektorem
- Zaváděcí sektor obsahuje `MBR` nebo `GPT`
	- Ty poskytují informace o `VBR` (Volume Boot Record)
		- Který načítá správce spouštění (`bootmgr.exe`)
- OS lze zavést z pevných disků, síťových disků, USB disků a vyměnitelných médií (podle funkcí základní desky)
#### 2) Popis spouštěcí sekvence v UNIX-like OS
##### UNIX-Like OS - Zavádění operačního systému (bootování)
1) Spuštění firmwaru z paměti `EEPROM`
2) Test  hardwaru`POST`
3) Firmware vyhledá zavaděč v `MBR` nebo `EFI` oddílu na prvním disku:
    - `MBR` je záznam `512B` na prvním sektoru disku
        - Obsahuje spustitelný kód a tabulku oddílů s informacemi o každém oddílu
    - U `EFI/UEFI` se načte nastavení s informací o umístění `EFI` oddílu a spouštěcí aplikaci
4) Následně se načte a spustí správce spouštění `GRUB`:
    - Používá konfigurační soubor `/etc/default/grub`
    - Změny lze aktivovat příkazem `update-grub`
    - `GRUB` načítá Kernel a obraz `initrd/initramfs` pro detekci hardwaru a přípravu kořenového souborového systému
5) Po aktivaci souborového systému Kernel spustí správce systému (`init` nebo `systemd` s PID 1)
    - Správce systému řídí ostatní deamony při spouštění i vypínání systému
#### 3) Správci spouštění v OS Windows a UNIX-like OS, možnosti úprav zavádění operačního systému
##### Možnosti zavedení operačního systému - OS Windows
- Do tohoto prostředí se lze dostat držením klávesy shift a tlačítka restartovat
- Příslušná možnost spuštění se vybere stiskem jedné z kláves **F1-F9**:
	- **1) Enable debugging**:
		- Režim ladění pro sledování a analýzu průběhu spouštění systému
	- **2) Enable boot logging**:
		- Vytvoření podrobného protokolu, který zaznamená všechny načítané ovladače a komponenty
	- **3) Enable low-resolution video**:
		- Základní video ovladač v nízkém rozlišení, užitečné pro řešení problémů s grafickou kartou
	- **4) Enable Safe Mode**:
		- Minimální sada ovladačů a služeb
	- **5) Enable Safe Mode with Networking**:
		- Minimální sada ovladačů a služeb s možností přístupu k síti či internetu
	- **6) Enable Safe Mode with Command Prompt**:
		- Minimální sada ovladačů a služeb bez GUI
	- **7) Disable driver signature enforcement**:
		- Instalace a spuštění nepodepsaných ovladačů
	- **8) Disable early launch anti-malware protection**:
		- Deaktivace antivirové ochrany během zavedení
	- **9) Disable automatic restart after failure**:
		- Operační systém se nerestartuje při závažné chybě
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
- Systém **runlevelů**, které umožňují **nastavit**, které služby se budou **v daném** **runlevelu** **spouštět**
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
- Lepším řešením je **upravit v souboru** `/etc/inittab` číslo runlevelu `id:{číslo}:initdefault:`
- **Povolení** či **zákaz spouštění služeb při spouštění**:
	- `chkconfig` (CentOS) 
	- `sysv-rc-conf` (Debian)
##### Správci spouštění v UNIX-like OS - systemd
1) Používá **paralelní spouštění procesů** a používá **dynamickou správu prostředků**
	- Služby se spouští v případě potřeby
2) Nástroj `systemctl` pro zobrazení stavu procesů s volbami:
	1) `start`
	2) `restart`
	3) `status`
	4) `stop`
	5) `enable`
	6) `disable`
	7) `is-enabled`
3) Runlevely jsou nahrazeny targetami:
	1) `Runlevel 0` <=> `poweroff.target`
	2) `Runlevel 1` <=> `rescue.target`
	3) `Runlevel 3` <=> `multi-user.target`
	4) `Runlevel 5` <=> `graphical.target`
	5) ``Runlevel 6`` <=> `reboot.target`
	6) `Emergency` <=> `emergency.target`
4) Při spouštění systému se aktivuje `default.target`, který spustí služby a další položky, které na nich závisí
5) Zobrazení default targetu:
	- `systemctl get-default`
6) Nastavení default targetu:
	- `systemctl set-default {target}`