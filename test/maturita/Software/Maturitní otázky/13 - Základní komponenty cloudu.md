#### 1) Cloud computing, Modely cloudu, Cloud jako model založený na spotřebě
##### Cloud Computing
- **Doručování výpočetních služeb**, jako jsou virtuální počítače, úložiště, databáze a síťová připojení přes Internet
- Cloudové služby **pronikají** do:
	- IoT (Internet of Things)
	- Strojového učení (Machine Learning)
	- Umělé inteligence (AI)
- Výhodou snadná **rozšířitelnost** stávající infrastruktury
- **Odpovědnost** za funkčnost infrastruktury **rozdělena mezi poskytovatele cloudu a zákazníka**:
	- **SaaS**:
		- Poskytovatel poskytne software, který je poskytovatelem spravován, dále spravuje infrastrukturu...
	- **PaaS** :
		- Poskytovatel poskytne infrastrukturu, kde zákazník odpovídá za aplikace, síť...
	- **IaaS**:
		- Poskytovatel poskytne síťovou konektivitu a zákazník odpovídá za operační systém, aplikace, síť...
	- **On-premise**:
		- Vše řešené zákazníkem, žádný poskytovatel zde není
##### Privátní cloud
- Cloud, který je používaný ve **firemním prostředí**
- Umožňuje **větší kontrolu** nad cloudem jako takovým
- **Je nákladnější** a chybí mu některé výhody
- Může být **spravován přímo firmou**, nebo nějakou **třetí stranou**
##### Veřejný Cloud
- **Spravován**, **vytvářen** a **řízen poskytovatelem** cloudu třetí strany
- Přístup ke službám a prostředkům cloudu si může zřídit kdokoliv
##### Hybridní Cloud
- **Kombinace veřejného** a **privátního cloudu**, které jsou mezi sebou **navzájem propojeny**
- U cloudových služeb je **odpovědnost za funkčnost infrastruktury rozdělena mezi poskytovatele cloudu** a **zákazníka**
##### Multi-cloudové řešení
- Firma používá **více poskytovatelů cloudu**
- Pro správu lze využít například **technologie Azure Arc** nebo **Azure VMWare Solution**
##### Cloud jako model založený na spotřebě
- **Kapitálové náklady** (**CapEx**)
	- Jednorázové, např stavba nového datacentra, nákup firemních vozidel...
- **Provozní náklady** (**OpEx**)
	- Opakované výdaje za poskytování služeb či spotřebu zboží (využívání cloudových služeb, pronájem vozidel...)
- **Platí pouze za využívání cloudových prostředků**, což přináší **řadu výhod**:
	1) Lepší plánování a správa provozních nákladů
	2) Efektivnější využití infrastruktury
	3) Lepší škálování podle potřeb firmy
- **Výhody** modelu **založeného na spotřebě**:
	1) Žádné počáteční náklady
	2) Není třeba kupovat nákladné vybavení
	3) V případě potřeby lze snadno přidat další prostředky (případně odebrat nevyužité prostředky)
#### 2) Výhody využívání cloudových služeb
##### Vysoká dostupnost
- **Zajištění dostupnosti poskytovatelem vždy**, **kdy je třeba**
- **V Azure** je dostupnost **garantována ve smlouvě SLA** (**Service-Level Agreement**)
##### Škálovatelnost
- Schopnost **přidat** či **odebrat** prostředky na základě požadavků poptávky
- Umožňuje **optimalizovat náklady** za prostředky
- **Vertikální škálování**:
	- Přidání hardwaru do stávajícího virtuálního počítače
- **Horizontální škálování**
	- Přidání dalších celých virtuálních počítačů
##### Výhody využívání cloudových služeb - Spolehlivost
- **Schopnost systému se zotavit při výskytu chyby** a **pokračovat v další činnosti** (Cloud je **decentralizovaný**)
##### Výhody využívání cloudových služeb - Předpověditelnost
- **Schopnost předpovědět**:
	1) Výkon:
		- Budoucí potřeba prostředků pro zajištění odpovídajícího výkonu
	2) Náklady: 
		- Budoucí náklady díky sledování využití prostředků v reálném čase, monitorování efektivity a dalších dat)
##### Výhody využívání cloudových služeb - zabezpečení a způsob používání cloudu
- Při používání modelů **SaaS** a **IaaS** lze zajistit **soulad s předpisy** a **zásadami** pro efektivní používání cloudu (**governance**)
- Z hlediska **zabezpečení** lze najít **vhodné cloudové řešení** pro zákazníka
- Poskytovatel cloudu zajišťuje ochranu před útoky z Internetu (např. DDoS)
##### Výhody využívání cloudových služeb - Správa cloudu
- Možnost **automatického škálování** a **nasazování prostředků**
- Rychlé **nasazování prostředků pomocí šablon**
- **Monitorování** **prostředků** a jejich případná automatická náhrada
- **Automatické zasílání varování** na základě **nakonfigurovaných parametrů pro sledování výkonu** v reálném čase
- Spravovat prostředky cloudu lze pomocí:
	1) Webového portálu
	2) AzureCLI
	3) REST API
	4) Powershellu
#### 3) Typy cloudových služeb
##### Typy cloudových služeb - IaaS
- **Nejflexibilnější** skupina cloudových služeb, poskytuje maximální kontrolu
- **Poskytovatel cloudu zajišťuje**:
	1) Údržbu
	2) Síťovou konektivitu
	3) Fyzické zabezpečení
- Jedná se o **pronájem hardwaru v datacentru poskytovatele**
- **Zákazník odpovídá**:
	1) Instalace
	2) Konfigurace
	3) Správa systému
	4) Databáze
	5) Úložiště
- Snadná **migrace z on-premise** řešení
- **Vývoj řešení pro testování** a **vývoj**, kde je nutná **rychlá replikace**
##### Typy cloudových služeb - PaaS
- kompromis mezi Iaas a Saas
- **Poskytovatel cloudu spravuje**:
	1) Infrastrukturu
	2) Zabezpečení
	3) Konetivitu do Internetu
	4) Operační systémy
	5) Middleware
	6) Nástroje pro vývoj
	7) Business intelligence
- Vhodné řešení pro **realizaci vývojového prostředí**
##### Typy cloudových služeb - SaaS
- **Nejkompletnější model** poskytování cloudových služeb
- **Zákazník si pronajme celou aplikaci** (např. elektronickou poštu, finanční software)
- Nejméně flexibilní model
- Zákazník aplikace pouze používá