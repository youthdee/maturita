#### 1) Správa nákladů v Azure, charakteristika nástrojů pro správu nákladů v Azure
##### Správa nákladů v Azure
- Náklady cloudových služeb patří mezi **provozní náklady** (**OpEx**).
- Výši nákladů **ovlivňuje**:
	1) Druh použitých prostředků, jejich konfigurace a oblast (HW konfigurace, oblast)
	2) Využití prostředků během účtovacího období
	3) Správa nevyužitých prostředků (kontraproduktivita)
	4) Zeměpisné umístění (v různých oblastech různé ceny, daně a poplatky)
	5) Síťový provoz (směr do data center zdarma, směr ven zpoplatněn na základě zón)
	6) Typ předplatného (některá předplatná jsou zdarma k nějakému jinému předplatnému)
	7) Azure Marketplace (již hotová řešení)
##### Cenová kalkulačka
- Slouží pro **odhad nákladů** za **poskytnutí prostředků Azure**.
##### Kalkulačka celkových nákladů na vlastnictví (TCO)
- **Porovnání** mezi **náklady na on-premise** a **náklady cloudové infrastruktury**
##### Nástroj pro správu nákladů Azure
- **Rychlá kontrola** nákladů prostředků
- Vytváření **varování** na základě útraty
- Vytvoření **rozpočtů** pro **automatizovanou správu** prostředků
- **Celková analýza nákladů** a **trendy** nákladů do budoucnosti
- **Cost Alerts**:
	- Pohled obsahující přehled všech typů nastavených upozornění ve službě správa nákladů.
##### Typy nákladů
1) **Budget alerts**:
	- Využití prostředků překročí nastavenou hodnotu
2) **Credit alerts**:
	- Blížící se vyčerpání finančních prostředků
3) **Department spending quota alerts**:
	- Překročení kvóty oddělení
##### Budget (rozpočet)
- **Vyhrazená částka** pro **útratu** za služby Azure
- Lze nastavit na **úrovni předplatného**, **skupiny prostředků** nebo **prostředku**, typy služby...
- Při jeho vytvoření se **automaticky vytvoří budget alert**
#### 2) Nástroje a funkce Azure pro správné řízení a zajištění souladu
#####  Azure Blueprints
- Zajištění **standardizace předplatného** cloudových služeb či prostředí pro nasazení
- Pokud je třeba vytvořit nové předplatné, díky **Azure Blueprints** lze použít **stejné nastavení** a **zásady jako u stávajícího**
- **Artifact** je komponenta definující Azure Blueprint, obsahuje další, nepovinné parametry
- Součástí artifactu je i **přiřazení rolí** a **zásad**, **skupina prostředků** a **šablona ARM**.
- Podporují verzování.
#####  Microsoft Purview
- Rodina řešení pro **řízení** a **správu** dat v on-premise, SaaS a multicloud řešeních
- Automatické **objevování** dat, **třídění citlivých dat** a **vytvoření úplného rodokmenu dat** 
	- Zobrazení závislosti mezi nezpracovávanými daty a hotovými daty, popisuje transformace a operace, které nehotové data převádí na hotové data
- Součástí jsou **funkce Microsoft 365**
- Dokáže vytvořit **mapu všech dat**, **identifikovat umístění citlivých dat**, vytvořit **bezpečné prostředí** pro vyhledávání **cenných dat zákazníky**.
- Vytváří **přehledy** o **způsobu uložení** a **využití dat**
- **Správa přístupu** k datům
#####  Azure Policy
- Služba pro **vytvoření**, **přiřazování** a **spravování zásad** pro **řízení** a **auditování prostředků**.
- Pomocí **pravidel firmy** dokáže **vynutit konfiguraci** prostředků, která je **v souladu** se **standardy firmy**.
- **Prověřuje prostředky** a **označuje** ty, které **nejsou v souladu** s již nastavenými zásadami.
- **Zabraňuje vytvoření prostředků**, které **nejsou v souladu** se zásadami firmy.
- Zásady **lze vytvářet na různých úrovních** (prostředek, skupina prostředků, předplatné...)
- Zásady se **dědí** na **podřízené prostředky**
- V některých případech dokáže **Azure Policy nekompatibilní prostředky opravit**
- Používá tzv. **iniciativy** (jednotlivá zásada nebo skupina příbuzných zásad)
##### Zámky prostředků
- **Zabránění nechtěné změně**, nebo **odstranění prostředku**
- Lze je aplikovat na **více úrovních**, **dědičnost**
- Dva typy zámků: 
	1) **Delete** (uživatel může prostředek číst a upravit ale nemůže jej odstranit)
	2) **ReadOnly** (uživatel může prostředek pouze číst)
- Zámky lze **konfigurovat v portálu Azure**, **PowerShellu**, **Azure CLI** a přes **ARM šablony**
- Před prováděním úpravy zamknutého prostředku je potřeba zámek nejprve odstranit
##### Portál Service Trust
- Přístup k různému **obsahu**, **nástrojům** a dalším prostředkům **týkajících se zabezpečení**, **soukromí** a **zajištění souladu**
- Poskytuje **podrobné údaje** o **mechanismu řízení** a **procesech** používaných pro **ochranu cloudových služeb** a **dat zákazníků**.
#### 3) Nástroje a funkce Azure pro správu a nasazování prostředků
##### Nástroje a funkce Azure pro správu:
1) **Portál Azure**:
	- Webové rozhraní pro správu Azure v grafickém rozhraní
2) **Azure Cloud Shell**:
	- Nástroj pro vytváření, konfiguraci a správu prostředků Azure pomocí shellu s podporou Azure PowerShell a Azure CLI - Bash shell
3) **Azure Powershell**:
	- Pracuje s cmdlety, které volají Azure REST API pro další zpracování
4) **Azure CLI** :
	- Funkcemi podobný Azure Powershell s odlišnou syntaxí - používá Bash shell
##### Azure Arc
- Zajištění souladu a **monitorování** v hybridním a multicloudovém prostředí v podobě platformy pro správu za pomoci **ARM** (Azure Resource Manager)
- **Správa** **kompletního** **prostředí**
-  **Zajištění správy virtuálních počítačů** v multicloudových a hybridních řešeních
-  **Správa serverů**, clustery Kubernetes, datové služby Azure, SQL server a virtuální počítače.
##### Azure Resource Manager (ARM)
- Služba pro **nasazení** a **správu služeb Azure**
- **Vytváření**, **akutalizace**, **odstranění**
- Uživatel **odešle** požadavek, ARM jej **příjme**, **ověří** a **odešle příslušné službě** Azure
##### Šablony Azure ARM
- Využívá **koncept Infrastructure as code**, který umožňuje **nasadit infrastrukturu pomocí kódu**.
- Formát **JSON**
- Lze vytvářet **paralelně** např. 50 instancí prostředku.
- Výhody:
	1) Skupinové nasazení
	2) Opakované nasazení
	3) Definování závislostí
	4) Nasazení ve správném pořadí
#### 4) Nástroje pro monitorování prostředí Azure
##### Azure Advisor
- Nástroj pro **vyhodnocení využívání prostředků** Azure
- **Vydává doporučení** týkající se vylepšení spolehlivosti, zabezpečení, výkonu, provozu a minimalizace nákladů s cílem optimalizovat využití prostředků Azure.
- Doporučení jsou k dispozici **v portálu Azure** a přes **API**.
##### Azure Service Health
- Sledování **stavu** nasazených prostředků a **celkový stav služby Azure**.
- Obsahuje tyto tři služby:
	1) **Azure Status**
		- Celkový stav služeb ve všech oblastech, informuje o výpadcích Azure
	2) **Service Health** 
		- Konkrétnější pohled na služby a oblasti Azure, které zákazník používá, informace o výpadcích, plánovaných odstávkách a další informace týkající se stavu služeb Azure
	3) **Resource Health** 
		- Informace o stavu konkrétních prostředků Azure
- Azure Service Health tak podává **celkový** **obraz** o obecném stavu služeb a oblastí v **infrastruktuře Azure** i jednotlivých prostředků včetně možnosti **historie** již vydaných upozornění a kontaktu na podporu.
##### Azure Monitor
-  **Shromažďování**, **analýzu** a **zobrazování dat** včetně **případných reakcí** na výsledky analýzy.
- Dokáže sledovat **Azure**, **on-premise** i **multicloud** prostředky
- Výsledky lze zobrazit v podobě **Azure Monitor Dashboard** nebo vlastních pohledů pomocí dotazů (Power BI, Kusto)
- Ze získaných dat je možné **reagovat v kritických událostech v reálném čase** prostřednictvím upozornění
##### Azure Log Analytics
- Zadávaní **dotazů na data** získaná pomocí **Azure Monitor** včetně možnosti **analýzy dat**.
##### Azure Monitor Alerts
- Automatické **vydávání upozornění při překročení zadané hodnoty** 
	- Podmínka, při které se má upozornění vyvolat
	- Např. vytížení CPU na virtuálním počítači překročí 80%.
- **Provedení akcí**, které **následují po upozornění** se nazývá **action groups**, lze spojit s **jednou nebo více událostmi**.
##### Azure Application Insights
- **Funkce** služby **Azure Monitor** pro **monitoring webových aplikací** běžících v Azure, **on-premise** a různých cloudových prostředích.
- Lze **monitorovat** např. **počty požadavků**, **doby odezvy**, **počty chyb**, **rychlost načtení**, **relace**, **počet uživatelů**.
- Dokáže posílat **syntetické požadavky** za účelem **kontroly stavu aplikace** a **sledování stavu během nízkého vytížení**.