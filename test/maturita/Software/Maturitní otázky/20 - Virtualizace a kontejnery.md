#### 1) Virtualizace a kontejnery – definice, základní pojmy, účel

##### Virtualizace - Definice, základní pojmy, účel
- Virtuální počítač je emulace výpočetního systému běžícího na fyzickém počítači (host)
- Operační systém ve virtuálním počítači je označován jako hostovaný (guest operating system)
- Operační systém ve fyzickém počítači je označován jako Host Operating System
- Virtualizace umožňuje jednomu počítači hostovat několik nezávisle běžících počítačů, které se označují jako virtuální počítače
	- Tyto počítače sdílí hardware hostitelského počítače
- Oddělení fyzického hardwaru počítače od jednotlivých instancí virtuálních počítačů provádí virtualizační software
- V případě potřeby je možné uložit obraz virtuálního počítače do souboru a z něj je opět obnovit
- Z virtualizace vychází cloud computing
- Hypervisory Typu 1 a Hypervisory Typu 2
	- Hypervisor typu 1 (nativní) se typicky používá při virtualizaci serveru (datacentra, cloud computing)
		- Běží přímo na hardwaru hostitele a řídí přiřazování systémových prostředků virtuálním počítačům
		- například VMware vSphere/ESXi, Xen, Oracle VM Server
	- Hypervisor typu 2 (hosted) se obvykle používá při virtualizaci na straně klienta
		- Za účelem vytváření a provoz více virtuálních počítačů
		- Například VMware Workstation, Windows Hyper-V, Oracle VirtualBox

##### Kontejnery - Definice, základní pojmy, účel
- Kontejner je balíček obsahující aplikaci a vše potřebné pro běh této aplikace
- Kontejnerizovaná aplikace běží a spravuje se nezávisle na tom, kde je nainstalována
- Kontejnery se na rozdíl od virtuálních počítačů spravují, konfigurují, spouští a zastavují mnohem snáze
- Nejpoužívanější softwarovou platformou je Docker
	- V jehož ekosystému jsou k dispozici desítky standardních kotnejnerů, které je možné stáhnout a použít
#### 2) Virtualizace v OS Windows a v UNIX-like OS

##### OS Windows - Virtualizace

##### UNIX-like OS - Virtualizace
- Balíček qemu, nástroj virsh
- Instalace operačního systému (ze staženého obrazu ISO) na virtuální počítač příkazem "virt-install":
	- Příklad argumentů: (--name, --ram, --vcpus, --cdrom, --os-type,--diskpath)
- Vypsání přehledu všech virtuálních počítačů příkazem "virsh --list all"
- Zjištění informací o virtuálním počítači příkazem "virsh dominfo {name}"
- Úprava nastavení virtuálního počítače příkazem "virsh edit {name}"
- Povolení či zákaz automatického spouštění virtuálního počítače při startu fyzického počítače příkazem "virsh autostart --disable? {name}"
- Zastavení virtuálního počítače příkazem "virsh shutdown {name}"
- Klonování virtuálního počítače (virtuální počítač musí být zastaven) příkazem "virt-clone --original {vm1} --atuo-clone --name {vm2}"

##### Windows OS - Virtualizace obecně
- Na klientských počítačích se obvykle používají virtualizační programy Hypervisor typu 2 (VMWare Workstation, Oracle VirtualBox)
	- Za účelem vytvoření a provozu více virtuálních počítačů na jednom klientském pc
- Na server se obvykle používají virtualizační programy Hypervisor typu 1 (VMWare vSphere/ESXi, Xen, Oracle VM Server) což přináší mnoho výhod:
	- Efektivita využití systémových prostředků
	- Není třeba tolik prostoru
	- Menší spotřeba energie
	- Nižší náklady
	- Rychlejší vybavení a nasazení
	- Maximalizace doby chodu serveru
	- Vylepšení zotavení po havárii (disaster recovery)
	- Podpora starších systémů
##### Windows OS - Microsoft Hyper-V
- Virtualizační systém založený na hypervisoru, který je určen pro počítače s architekturou x64 a je poprvé dostupný ve Windows Serveru 2008
- Hypervisor se instaluje mezi hardware a operační systém a představuje hlavní komponentu, která slouží ke správě virtuálních počítačů
- Virtualizace umožňuje efektivnější využití hardwaru serveru
- Požadavky Hyper-V:
	- 64bitové procesory a BIOS s podporou technologie hardwarově asistované virtualizace (Intel VT nebo AMD-V)
	- Hardware Data Exucution Prevention (DEP)
		- Což je technologie používaná v procesorech pro oddělení oblastí paměti pro uložení instrukcí procesoru a pro uložení dat
		- Intel popisuje jako Executed Disable (XD)
		- AMD popisuje jako No Execute (NS)
- Integrační služby jsou ovladače pro běh operačních systémů ve viruálním prostředí
	- Komponenty pro integraci se instalují z nabídky Akce připojení virtuálního počítače klepnutím na položku Vložit instalační disk pro integrační služby
	- Ruční instalace se provádí spuštěním souboru "%windir%\support\amd64\setup.exe."
- Konsolidace je sloučení několika fyzických serverů do jedoho počítače, kde bude běžet několik virtuálních serverů
	- Nástroj Microsoft System Center Virtual Machine Manager (VMM) uožňuje převod existujících fyzických počítačů na virtuální
	- Tento proces se označuje jako "physical-to-virtual" (P2V) conversion
- Virtuální pevné disky lze definovat dvěma způsoby:
	- Jako virtuální pevné disky o pevné velikosti (disky zaberou na fyzickém pevném disku svojí plnou kapacitu)
	- Jako dynamicky se zvětšující pevné disky
- Snímky (snapshots) jsou obrazy virtuálních počítačů v určitém bodě v čase
	- Do tohoto stavu je možné se vrátit
	- Technologie Hyper-V umožňuje vytvořit až 10 snímků pro každý virtuální počítač
	- Sníkem obsahuje kopii konfiguračního xml souboru, soubory s uloženým stavem, rozdílový disk (.avhd) obsahující rozdíly oproti stavu disku před vytvořením snímku
#### 3) Konfigurace a správa kontejnerů

##### UNIX-Like OS - Konfigurace a správa kontejnerů
- Instalovat Docker lze příkazem "curl -fsSL https://get.docker.com | sh", který stáhne a spustí skript pro přidání repozitáře Dockeru do počítače a nainstaluje balíček
- Spuštění služby a kontrola jejího stavu příkazem "systemctl {start | status} Docker"
- Zobrazení dostupných možností příkazem "docker"
- Získání nápovědy příkazem "docker {COMMAND} --help" (Za COMMAND lze dosadit například ps, kde to vypíše nápovědu jak zobrazit seznam kontejnerů v počítači, COMMAND run zobrazí možnosti, které jsou kdispozici pro manipulaci s kontejnerem)
- Kontrola stavu kontejneru příkazem "sudo docker ps"
- Zastavení kontejneru příkazem "sudo docker stop {name}"
- Odstranění kontejneru příkazem "sudo docker rm {name}"
- Odstranění obrazu použitého v kontejneru příkazem "sudo docker image remove {image name}"
