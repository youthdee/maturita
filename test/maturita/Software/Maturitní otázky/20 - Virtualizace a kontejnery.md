#### 1) Virtualizace a kontejnery – definice, základní pojmy, účel
##### Virtualizace - Definice, základní pojmy, účel
- **Virtuální počítač** je **emulace výpočetního systému běžícího na fyzickém počítači** (host)
- Operační systém ve virtuálním počítači je označován jako **hostovaný** (guest operating system)
- Operační systém ve fyzickém počítači je označován jako **Host Operating System**
- Virtualizace umožňuje jednomu počítači **hostovat několik nezávisle běžících virtuálních počítačů**
- Oddělení fyzického hardwaru počítače od jednotlivých instancí virtuálních počítačů provádí **virtualizační software**
- Z virtualizace vychází **cloud computing**
- Hypervisory Typu 1 a Hypervisory Typu 2
	1) Hypervisor typu 1 (nativní) se typicky používá při **virtualizaci serveru** (datacentra, cloud computing)
		- Běží přímo na hardwaru hostitele a řídí přiřazování systémových prostředků virtuálním počítačům
		- VMware vSphere/ESXi, Xen, Oracle VM Server
	2) Hypervisor typu 2 (hosted) se obvykle používá při **virtualizaci na straně klienta**
		- Za účelem vytváření a provoz více virtuálních počítačů
		- VMware Workstation, Windows Hyper-V, Oracle VirtualBox
##### Kontejnery - Definice, základní pojmy, účel
- **Balíček obsahující aplikaci a vše potřebné pro běh této aplikace**
- Kontejnerizovaná aplikace běží a spravuje se nezávisle na tom, **kde je nainstalována**
- Kontejnery se na rozdíl od virtuálních počítačů spravují, konfigurují, spouští a zastavují mnohem snáze
- Nejpoužívanější softwarovou platformou je **Docker**
	- V jehož ekosystému jsou k dispozici desítky standardních kontejnerů, které je možné stáhnout a použít
#### 2) Virtualizace v OS Windows a v UNIX-like OS
##### UNIX-like OS - Virtualizace
- Balíček **qemu**, nástroj **virsh**
- Instalace operačního systému na virtuální počítač příkazem `virt-install`:
	- Příklad argumentů: (--name, --ram, --vcpus, --cdrom, --os-type,--diskpath)
- Vypsání **přehledu všech virtuálních počítačů** příkazem `virsh --list all`
- Zjištění **informací o virtuálním počítači** příkazem `virsh dominfo {name}`
- **Úprava nastavení** virtuálního počítače příkazem `virsh edit {name}`
- **Zastavení** virtuálního počítače příkazem `virsh shutdown {name}`
- **Klonování** virtuálního počítače příkazem `virt-clone --original {vm1} --auto-clone --name {vm2}`
##### Windows OS - Virtualizace obecně
- Na klientských počítačích se používají virtualizační programy **Hypervisor typu 2** (**VMWare Workstation**, **Oracle VirtualBox**)
	- Za účelem vytvoření a provozu více virtuálních počítačů na jednom klientském pc
- Na serveru se obvykle používají virtualizační programy **Hypervisor typu 1** (**VMWare vSphere/ESXi, Xen, Oracle VM Server**) což přináší mnoho výhod:
	1) Efektivita využití systémových prostředků
	2) Menší spotřeba energie
	3) Nižší náklady
	4) Rychlejší vybavení a nasazení
	5) Maximalizace doby chodu serveru
	6) Vylepšení zotavení po havárii
##### Windows OS - Microsoft Hyper-V
- **Virtualizační systém založený na hypervisoru, který je určen pro počítače s architekturou x64**
1) Integrační služby jsou **ovladače pro běh operačních systémů ve virtuálním prostředí**:
	- Komponenty pro integraci se instalují z nabídky Akce připojení virtuálního počítače klepnutím na položku Vložit instalační disk pro integrační služby
2) Konsolidace je **sloučení několika fyzických serverů do jednoho počítače**, kde bude běžet několik virtuálních serverů
	- Nástroj Microsoft System Center Virtual Machine Manager (VMM) umožňuje převod existujících fyzických počítačů na virtuální
3) Virtuální pevné disky lze definovat dvěma způsoby:
	- Jako **virtuální pevné disky** o pevné velikosti
	- Jako **dynamicky se zvětšující** pevné disky
4) Snímky (**snapshots**) jsou **obrazy virtuálních počítačů v určitém bodě v čase**
	- Technologie Hyper-V umožňuje vytvořit až 10 snímků pro každý virtuální počítač
#### 3) Konfigurace a správa kontejnerů
##### UNIX-Like OS - Konfigurace a správa kontejnerů
- Zobrazení dostupných možností příkazem `docker` případně `docker {command} --help`
- Kontrola stavu kontejneru příkazem `sudo docker ps`
- Zastavení kontejneru příkazem `sudo docker stop {name}`
- Odstranění kontejneru příkazem `sudo docker rm {name}`
- Odstranění obrazu použitého v kontejneru příkazem `sudo docker image remove {image name}`
##### Windows - Konfigurace a správa kontejnerů
- Docker
- Windows Containers na Windows Serveru
	- Nepodporuje linuxové kontejnery
	- Nativní `containerd` deamon
	- Běží buď jako **Process Isolation**, nebo jako **Hyper-V Isolation**