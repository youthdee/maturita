#### 1) Základní charakteristika a popis rozhraní OS Android a iOS
##### Základní charakteristika 
- **Aplikace** se **píší** a **kompilují** vždy pro **konkrétní operační systém**
- V mobilních zařízeních je vždy **přednainstalována** řada různých aplikací **s cílem poskytnout základní funkce mobilního zařízení**
- Aplikace se stahují ze **zdroje obsahu** (content source)
##### OS Android
- Vyvíjeno firmou **Google**
- Aplikace se instalují z internetového obchodu **Google Play** nebo z **webů poskytovatelů třetí strany** 
	- Programy třetích stran (nebo vlastní) se instalují přímo prostřednictvím souborů .APK (Android Application Package)
	- Tento způsob umožňuje přímou instalaci bez nutnosti používat internetový obchod (sideloading)
- **Aplikace běží v izolovaném prostředí** (sandbox) a mají pouze ta oprávnění, která jim přiřadil uživatel
##### OS Android - Rozhraní
- Jedna z obrazovek je nastavena jako **domovská**
- Systémový pruh (**system bar**) pro **navigaci**:
	- Obsahuje tlačítka jako zpět, domů, nedávné aplikace, nabídka
- Každé zařízení obsahuje **systémové ikony** (Wi-Fi, síla mobilního signálu...) v oznámení:
	- Zde se dále dá nastavit zrušení oznámení, přesunutí do aplikace, upravit jas obrazovky, nastavení...
##### IOS - Rozhraní
- Podobné androidu
- **Bez zástupců**, každá aplikace **reprezentuje sama sebe**
- **Centrum oznámení** v němž se zobrazují všechny oznámení
- Funkce **IOS Spotlight** zobrazuje **návrhy z různých zdrojů**, například z internetu, ze zpráv, ze souborů...
##### IOS
- Vyvíjeno firmou **Apple**
- Aplikace se instalují z internetového obchodu **App Store**
	- Model walled garden (Apple musí nejdříve aplikaci schválit, než ji uvede na App Store)
#### 2) Nejběžnější funkce mobilních zařízení
- Naprostá většina mobilních zařízení má **akcelerometr**, který zjišťuje polohu zařízení a podle toho **otočí obrazovku**
- U některých zařízení se nacházejí **gynoskopy**, které zajišťují **přesnější detekci pohybu**
##### GPS
- **Global Positioning System** dokáže zjistit **přesný čas** a **zeměpisné umístění zařízení** pomocí zpráv zasílaných satelity ve vesmíru a přijímači na zemi
- Pro výpočet polohy potřebuje přijímač GPS alespoň čtyři satelity
	- Polohu určí na základě zaslaných zpráv
- **Systémy IPS** (Interior Positioning Systems) dokáží **určit polohu zařízení triangulací vzdálenosti od jiných zdrojů** radiových signálu (Wi-fi)
##### Wi-Fi Calling
- Namísto mobilní sítě se hlasový hovor **realizuje přes Internet** prostřednictvím místního hotspotu Wi-Fi
##### Platby pomocí NFC payment
- Peněžní transakce pomocí **Premium SMS**:
	- Uživatelé posílají SMS zprávu na speciální telefonní číslo mobilního operátora
	- Tato zpráva obsahuje požadavek na zaplacení určité částky
	- Prodejce je pak informován
- **Přímá platba mobilním zařízením** (**Direct Mobile Billing**):
	- Nejprve se uživatel identifikuje
	- Pak se mu platba zaúčtuje na účet poskytovaný mobilním operátorem
- **Mobilní platby na Internetu**:
	- Webová či samostatná aplikace pro uskutečnění platby
- Bezkontaktní platba pomocí **NFC** (**Near Field Communication**):
	- Přiblížení mobilního telefonu k platebnímu terminálu
##### Virtuální asistenti
- Princip **umělé inteligence** a **strojového učení**, rozpoznávání hlasu
- **Google Now**, **Siri**, **Apple Inteligence**, **Gemini**
#### 3) Možnosti zabezpečení mobilních zařízení
##### Zámek obrazovky a biometrické ověřování
- Možnost provedení určitých **bezpečnostních opatření** poté, co je proveden **určitý počet chybných pokusů** o odemknutí zařízení
	- U OS Android je to 4 - 12 pokusů, pak je nutné odemknout zařízení přes Gmail
	- U IOS lze nastavit bezpečnostní opatření, které po 10 neúspěšných pokusech vymaže všechna data na zařízení (data jsou ale zálohována)
##### Vzdálené zálohování
- **Kopírování dat** pomocí aplikace nebo OS **do cloudového úložiště**
- U většiny OS pro mobilní zařízení je **uživatelský účet svázán s cloudovými službami výrobce**:
	- iCloud pro IOS
	- Google Sync pro OS Android
	- Cloudové služby třetích stran (Dropbox)
- Další možností je nasazení **MDM** (**Mobile Device Management**), což je nástroj, který **automaticky zálohuje** mobilní zařízení uživatelů
##### Aplikace pro zjišťování polohy
- Pokud doje **ke ztrátě** nebo **odcizení mobilního zařízení**, lze využít pro jeho **nalezení aplikace pro nalezení polohy**
- U OS **Android** je to **správce zařízení**
- U **IOS** je to **Find My**
- Při nalezení je možné **provést další operace** (**odeslání zprávy**, **přehrání zvuku**)
- Pokud se **nepodaří zařízení nalézt**, je zde varianta **vymazání dat nebo uzamčení na dálku**
##### Antivirus
- V OS **IOS** **není možné provádět automatické** nebo **plánované kontroly zařízení** (bezpečnostní funkce, která zabraňuje škodlivým programům používat neautorizované prostředky)
- Aplikace v mobilním zařízení **běží v sandboxu** (kód je **izolován** od operačního systému), tím pádem je **velmi obtížné pro záškodný software infikovat zařízení**
	- Škodlivému softwaru lze také zabránit nasazením firewallu
##### Rooting a Jailbreaking
- Obecně jsou OS pro mobilní zařízení **chráněny pomocí řady softwarových omezení**
- U **IOS** může **autorizovaný kód spustit pouze nezměněná kopie OS IOS** 
	- Uživatel má navíc velmi omezený přístup k souborovému systému
- **Omezení** a **ochranu** přidanou do OS **lze odstranit Rootingem** nebo **Jailbreakingem**
	1) Rooting se používá u zářízení s OS Android.
		- Umožňuje získat privilegovaný přístup nebo přístup pod uživatelem root
	2) Jailbreaking se používá u zařízení s OS IOS
		- Umožňuje získat úplný přístup k souborovému systému a k modulům jádra operačního systému
		- Dnes již nemožné
