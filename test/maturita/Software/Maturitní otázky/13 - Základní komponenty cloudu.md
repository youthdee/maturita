#### 1) Cloud computing, Modely cloudu, Cloud jako model založený na spotřebě

##### Cloud Computing
- Doručování výpočetních služeb, jako jsou virtuální počítače úložiště, databáze a síťová připojení přes Internet
- Cloudové služby pronikají i do:
	- IoT (Internet of Things)
	- Strojového učení (Machine Learning)
	- Umělé inteligence (AI)
- Jednou z velkých výhod je snadná rozšířitelnost stávající infrastruktury
- U cloudových služeb je odpovědnost za funkčnost infrastruktury rozdělena mezi poskytovatele cloudu a zákazníka:
	- SaaS (Poskytovatel poskytne software, který je poskytovatelem spravován, dále spravuje infrastrukturu...)
	- PaaS (Poskytovatel poskytne infrastrukturu, kde zákazník odpovídá za aplikace, síť...)
	- IaaS (Poskytovatel poskytne síťovou konektivitu a zákazník odpovídá za operační systém, aplikace, síť...)
	- On-premise (Vše řešené zákazníkem, žádný poskytovatel zde není)
##### Modely cloudu - Privátní cloud
- Cloud, který je používaný ve firemním prostředí
- Umožňuje větší kontrolu nad cloudem jako takovým
- Je nákladnější a chybí mu některé výhody
- Může být spravován přímo firmou, nebo nějakou třetí stranou

##### Modely cloudu - Veřejný Cloud
- Spravován, vytvářen a řízen poskytovatelem cloudu třetí strany
- Přístup ke službám a prostředkům cloudu si může zřídit kdokoliv

##### Modely cloudu - Hybridní Cloud
- Kombinace veřejného a privátního cloudu, které jsou mezi sebou navzájem propojeny
- U cloudových služeb je odpovědnost za funkčnost infrastruktury rozdělena mezi poskytovatele cloudu a zákazníka

##### Modely cloudu - Multicloudové řešení
- Firma používá více poskytovatelů cloudu
- Pro správu lze využít například technologie Azure Arc nebo Azure VMWare Solution

##### Cloud jako model založený na spotřebě
- Kapitálové náklady (CapEx)
	- Jednorázové, např stavba nového datacentra, nákup firemních vozidel...
- Provozní náklady (OpEx)
	- Opakované výdaje za poskytování služeb či spotřebu zboží (využívání cloudových služeb, pronájem vozidel...)
- Při využívání cloudu se platí pouze za využívání cloudových prostředků, což přináší řadu výhod:
	- lepší plánování a správa provozních nákladů
	- efektivnější využití infrastruktury
	- lepší škálování podle potřeb firmy
- Výhody modelu založeného na spotřebě:
	- žádné počáteční náklady
	- není třeba kupovat nákladné vybavení
	- v případě potřeby lze snadno přidat další prostředky (případně odebrat nevyužité prostředky)
#### 2) Výhody využívání cloudových služeb

##### Výhody využívání cloudových služeb - Vysoká dostupnost
- Zajištění dostupnosti poskytovatelem vždy, kdy je třeba
- V Azure je dostupnost garantována ve smlouvě SLA (Service-Level Agreement)

##### Výhody využívání cloudových služeb - Škálovatelnost
- schopnost přidat či odebrat prostředky na základě požadavků poptávky
- umožňuje optimalizovat náklady za prostředky
- Vertikální škálování:
	- Přidání hardwaru do stávajícího virtuálního počítače
- Horizontální škálování
	- Přidání dalších celých virtuálních počítačů

##### Výhody využívání cloudových služeb - Spolehlivost
- Schopnost systému se zotavit při výskytu chyby a pokračovat v další činnosti (Cloud je decentralizovaný)

##### Výhody využívání cloudových služeb - Předpověditelnost
- Schopnost předpovědět:
	- Výkon (Budoucí potřeba prostředků pro zajištění odpovídajícího výkonu)
	- Náklady (budoucí náklady díky sledování využití prostředků v reálném čase, monitorování efektivity a dalších dat)

##### Výhody využívání cloudových služeb - zabezpečení a způsob používání cloudu
- Při používání modelů SaaS a IaaS lze zajistit soulad s předpisy a zásadami pro efektivní používání cloudu (governance)
- Z hlediska zabezpečení lze najít vhodné cloudové řešení pro zákazníka
- Poskytovatel cloudu zajišťuje ochranu před útoky z Internetu (např. DDoS)

##### Výhody využívání cloudových služeb - Správa cloudu
- Možnost automatického škálování a nasazování prostředků
- rychlé nasazování prostředků pomocí šablon
- monitorování prostředků a jejich případná automatická náhrada
- automatické zasílání varování na základě nakonfigurovaných parametrů pro sledování výkonu v reálném čase
- Spravovat prostředky cloudu lze pomocí:
	- Webového portálu
	- Příkazového řádku
	- API
	- Powershellu
#### 3) Typy cloudových služeb

##### Typy cloudových služeb - IaaS
- Nejflexibilnější skupina cloudových služeb
- poskytuje maximální kontrolu nad cloudovými prostředky
- poskytovatel cloudu zajišťuje:
	- údržbu
	- síťovou konektivitu
	- fyzické zabezpečení
- jedná se o pronájem hardwaru v datacentru poskytovatele
- zákazník tedy odpovídá za vše ostatní:
	- instalace
	- konfigurace
	- správa systému
	- databáze
	- úložiště
- snadná migrace z on-premise řešení
- vývoj řešení pro testování a vývoj, kde je nutná rychlá replikace

##### Typy cloudových služeb - PaaS
- kompromis mezi Iaas a Saas
- Poskytovatel cloudu spravuje:
	- Infrastrukturu
	- Zabezpečení
	- Konetivitu do Internetu
	- Operační systémy
	- Middleware
	- Nástroje pro vývoj
	- Business intelligence
- Vhodné řešení pro realizaci vývojového prostředí

##### Typy cloudových služeb - SaaS
- Nejkompletnější model poskytování cloudových služeb
- Zákazník si pronajme celou aplikaci (např. elektronickou poštu, finanční software)
- Nejméně flexibilní model
- Zákazník aplikace pouze používá