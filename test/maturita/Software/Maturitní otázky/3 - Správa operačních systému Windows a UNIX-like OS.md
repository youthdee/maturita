#### 1) Možnosti správy operačního systému Windows pomocí systémových nástrojů v grafickém a textovém rozhraní

##### Možnosti správy OS Windows pomocí systémových nástrojů v grafickém rozhraní
1) **Správce úloh**:
	- Sledování operačního systému
	- Spuštění Ctrl+Shift+Esc
	- Procesy, Výkon, Historie Aplikací, Po spuštění, Uživatelé, Detaily
2) **Průzkumník souborů**:
	- Kopírování, přesun a vytváření složek, pohyb po souborovém systému, správa souborů,  složek a podsložek, správa aplikací na úložištích, zobrazení náhledu u některých typů souborů
	- Formátování disku
3) **Tento Počítač**:
	- Přístup k nejrůznějším zařízením a diskům
	- Spuštění přes průzkumník souborů
4) **Možnost Spustit jako správce**:
	- Spouštění a manipulace se soubory či složkami s vyššími oprávněními
	- Nabídka spustit jako správce
5) **Ovládací panely**:
	- Konfigurace operačního systému
	- Systém a zabezpečení, Síť a Internet, Hardware a Zvuk, Programy, Uživatelské účty, Usnadnění přístupu, Hodiny a oblast, Vzhled a přizpůsobení, Bitlocker
6) **Aplikace Nastavení**:
	- Možnosti Nastavení a Konfigurace obrazovky, Možnosti napájení, Systémové informace, výchozí programy, Vzhled a motiv
7) **Nástroje pro správu**:
	- Soubor nástrojů pro sledování a konfiguraci činnosti operačního systému
	- Správa počítače, Prohlížeč událostí, Místní uživatelé a skupiny, sledování výkonu, služba komponent a zdroje dat, služby, správa tisku, diagnostika paměti Windows, Konfigurace systému (MSCONFIG), Registr, Regedit
8) **Microsoft Management Console** (**MMC**):
	- Moduly snap-in, které se přidávají do konzoly
	- Defaultně je konzola prázdná
	- Stav je možné uložit
9) **Správa disků**:
	- Stav disku, přiřazení či změnění mapování disku, přidání disk nebo diskového pole, nastavení diskového oddílu jako aktivní, inicializování disku
##### Možnosti správy OS Windows pomocí systémových nástrojů v textovém rozhraní
	- zkopírovat z otázky 2 - která je uložena zatím lokálně
#### 2) Možnosti správy UNIX-like OS pomocí systémových nástrojů v grafickém a textovém rozhraní
##### Možnosti správy UNIX-Like OS pomocí systémových nástrojů v grafickém rozhraní
1) **Nástroj Disks**:
	- Správa diskových oddílů, připojování či odpojování disků, formátování diskových oddílů, dotazování se na stav disku technologií S.M.A.R.T (Self Monitoring Analysis Reporting Technology)
2) **Nástroj Gnome-keyring**:
	- Zabezpečení a ověření uživatelů
3) **Nastavení systému**:
	- Centrální rozhraní pro správu uživatelů, sítě, zobrazení a zvuku
4) **GNOME System Monitor**:
	- Monitorování procesů, zatížení CPU, RAM a diskových operací
5) **GParted**:
	- Správa diskových oddílů
6) **Nástroj nmtui**:
	- Pro konfiguraci síťových rozhraní, systémového názvu
##### Možnosti správy UNIX-Like OS pomocí systémových nástrojů v textovém rozhraní
1) **Sledování využití prostoru na discích**:
	- Příkaz `df` (disk free)
		- Celkové využití disku v bajtech, celkovou velikost, volný a obsazený prostor a mount point každého úložiště
		- Příznak `-h` pro human-readable formu
		- Častým problémem může být nedostatek inodes:
			- Všechny soubory jsou mapovány na inodes, která obsahují metadata souboru
	- Příkaz `du` (disk usage):
		- Zjištění, které soubory zabírají nejvíce místa
2) **Sledování využití RAM a CPU** - **Nástroj** `top`:
	- Stav systému v reálném čase
	- Nástroj `free` pro sledování RAM a odkládacího prostoru
	- Alternativně nástroj `Htop`, který je více přívětivý
3) **Sledování procesů** (Nástroj `ps` a `pstree`)
	- Vlastník procesu, PID, parent PID, využití CPU, čas spuštění, tty, kumulovaný čas CPU, asociovaný příkaz
	- Správa prostřednictvím signálů:
		- `SIGTERM` (15)
		- `SIGINT` (2)
		- `SIGKILL` (9)
		- `SIGHUP` (1)
		- `SIGTSTP` (20)
		- `SIGSTOP` (19)
		- `SIGCONT` (18)
			- `kill -9 {PID}`
	- Informace o selhání lze najít v `/var/log`
4) **Nástroj pro správu služeb** (**systemctl**):
	- `Enable`
	- `Restart`
	- `Status`
	- `Start`
		-  `journalctl` pro zobrazení chyb v konfiguračních souborech
5) **Základní příkazy pro správu**:
	- `passwd` pro změna hesla
	- `ps` pro správu procesů
	- `kill` pro ukončení procesů
	- `ifconfig` pro zobrazení IP adresních parametrů
	- `iwconfig` pro konfiguraci bezdrátového adaptéru
	- `chmod` pro změnu oprávnění u souborů
	- `chown` pro změnu vlastníka či skupiny
#### 3) Možnosti a konfigurace přístupu v režimu správce pro běžné uživatele, příkaz sudo a jeho konfigurace.
##### Možnosti a konfigurace přístupu v režimu správce pro běžné uživatele
- Nástroj `chattr` **zabraňuje přejmenování**, **přesunu, smazání a úpravě souboru**
	- `chattr +i {file}` - nelze přesunout, přejmenovat, upravit ani smazat a to ani rootem
	- `chattr +a {file}` - lze přidávat pouze další obsah
	- `lsattr {file}` zobrazí speciální oprávnění u daného souboru 
##### Přístup k účtu root
- **Příkaz** `su`:
	- Přesun do domovského adresáře příkazem `su -`
	- Lze použít pouze s heslem, což je bezpečnostní riziko, proto je vhodnější použít příkaz `sudo`, který umožňuje vykonat příkaz jako super user
- Přístup uživatelům k příkazu `sudo` se definuje v `/etc/sudoers` (nástrojem `visudo`)
	1) **Definování cest**:    
	    - Určuje, ve kterých adresářích lze spouštět příkazy pomocí `sudo`
	2) **Obecné pravidlo pro root uživatele**:  
	    - `root ALL=(ALL) ALL`  
	    - Uživatel root může spouštět jakýkoliv příkaz s jakýmikoliv oprávněními.
	3) **Pravidlo pro všechny uživatele**:  
	    - `ALL ALL=(ALL) ALL` 
	    - Každý uživatel může spouštět jakékoliv příkazy s jakýmikoliv oprávněními (což se běžně nenastavuje z bezpečnostních důvodů).
	4) **Omezený přístup pro konkrétního uživatele**:  
	    - `user1 ALL=/bin/yum update`  
	    -  Uživatel user1 smí spustit pouze příkaz yum update jako root.
	5) **Spouštění příkazu bez nutnosti zadávat heslo**:  
	    - `user2 ALL=NOPASSWD:/bin/updatedb`  
	    - User2 může spouštět příkaz updatedb bez nutnosti zadání hesla.
	6) **Pravidlo pro celou skupinu uživatelů**:  
	    - `%admin ALL=(ALL) ALL`
	    - Všichni členové skupiny admin mohou spouštět jakýkoliv příkaz s jakýmikoliv oprávněními.
- **Zobrazení oprávnění**, která má **uživatel přístupné** **pod** `sudo` **příkazem** `sudo -l`
