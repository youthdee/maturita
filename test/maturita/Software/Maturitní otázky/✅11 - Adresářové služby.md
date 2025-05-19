#### 1) Základní charakteristika adresářových služeb, Active Directory, pracovní skupina a doména, role FSMO, globální katalog, úroveň funkčnosti
##### Základní charakteristika adresářových služeb
- Obsahují, spravují a poskytují **přístup k různým informacím v adresáři**
- Používají se pro vyhledávání, správu a uspořádání běžných položek a síťových prvků (svazky, složky, soubory, tiskárny, uživatelé, skupiny, zařízení, telefonní čísla...)
- **Active Directory**
##### Active Directory
- Poskytuje spoustu **síťových služeb**:
	- Je řadičem domény
	- LDAP (Lightweight Directory Access Protocol)
	- Ověřování kerberos a single sign-on authentication
	- Používání názvů založených na službě DNS a další informace týkající se počítačové sítě
	- Centrum pro správu sítě a delegování
- Active Directory **vyžaduje funkční službu DNS**
1) **Logická struktura** Active Directory:
	- Logickými prvky uspořádání Active Directory jsou:
		- Domény
		- Stromy
		- Lesy
	- Vztah důvěrnosti pro povolení uživateli z lokální domény přistupovat do jiné domény
2) **Fyzická struktura** Active Directory:
	- Místo (site):
		- Jedna nebo několik podsítí, které jsou navzájem propojeny
		- Obvykle jsou definovány na základě zeměpisného umístění
	- Řadič domény:
		- Obsahuje kopie údajů týkajících se uživatelských účtů a zabezpečení pro doménu
		- Zároveň definuje hranice domény
- **Active Directory lze spravovat pomocí Snap-In modulů konzoly MMC:**
	- Active Direcoty Users and Computers,
	- Active Directory Domains and Trusts,
	- Active Directory Administrative Center,
	- Active Directory Sites and Services,
	- Group Policy Management Console
##### Pracovní skupina (Workgroup)
- **Jednoduché seskupení počítačů** v lokální síti, kde každý počítač spravuje vlastní uživatelské účty a oprávnění
- Nemá **žádný centrální řadič**, každý počítač si ukládá informace o uživatelských účtech lokálně
##### Doména
- **Centrální správa uživatelů, oprávnění a zásad** díky Group Policy
- Uživatelé se mohou přihlásit na jakýkoliv počítač v doméně pomocí jednoho účtu
- **Lepší škálovatelnost**
##### Active Directory - Role FSMO (Flexible Single Master Operations)
- Vzhledem k tomu, že existují funkce, které může v jednom okamžiku provádět pouze jeden řadič domény, používá Active Directory role FSMO, které se označují také jako operations master roles
- Příklad **FSMO rolí**:
	1) Schema Master 
		-  1 per forest, spravuje aktualizace a změny schématu Active Directory
	2) Domain Naming Master 
		- 1 per forest, Spravuje přidání a odebrání domén z lesu pokud se les vyskytuje v root domain
	3) Primary Domain Controller Emulator 
		- 1 per domain, Primary Domain Controller, v minulosti používán jako hlavní správce domény, podpora kompability, tváří se jako hlavní server pro změny hesel
	4) RID Master
		- 1 per domain, Alokuje pooly UUID pro doménové controllery pro použití při vytváření nových domén
	5) Infrastructure Master
		- 1 per domain, synchronizuje změny vlastnictví skupin mezi více doménami
- Active Directory používá **replikaci multimaster**
	- V doménách typu Windows NT není žádný hlavní řadič domény, který by se dal označit také jako primární řadič domény
##### Active Directory - Globální Katalogy
- **Replikuje údaje** týkající se **každého objektu** ve stromu a v lese
- Standardně se vytváří **automaticky na prvním řadiči v lese**, ale tento katalog může obecně obsahovat **libovolný řadič domény**
##### Active Directory - Úrovně funkčnosti
- V Active Directory mohou být **řadiče** domény, na nichž **běží různé verze OS Windows Server**
- **Úroveň funkčnosti domény** nebo **lesa** závisí na tom, **jaká verze OS WS běží** na řadičích domény v dané doméně či lese
	- Udává, jaké pokročilé funkce budou v doméně či v lese k dispozici
#### 2) Základní objekty Active Directory a jejich charakteristika, zásady skupiny
##### Organizační jednotky (OU)
- **Organizaci objektů** v **doméně** a **minimalizaci potřebného počtu domén**
- Mohou obsahovat uživatele, skupiny, počítače atd.
- Je možno je **vnořovat**, ale doporučeno je vnořovat **minimálně**
##### Objekty Active Directory - Obecně
- **Jednoznačné** a **pojmenované sady atributů či charakteristik**, které **reprezentují konkrétní prvky** v síti 
- Atributy mají přiřazeny **určité hodnoty**, které **příslušný objekt definují**
- Každý objekt Active Directory má přiřazeno **jedinečné 128 bitové číslo** (**GUID**), který se někdy označuje jako **SID** (**Security Identidier**), který objekt jednoznačně identifikuje
##### Uživatelské účty
- Umožňují uživatelům **se přihlásit** do **počítače** a do **domény**
- Slouží k **ověření identity** a následně k zjišťování k čemu **může uživatel přistupovat** a jakou **úroveň pověření vlastní**
- Uživatelský účet je možné rovněž **použít pro audit**
- V soudobých sítích s prvky s nainstalovaným systémem OS Windows se používají **místní** a **doménové** uživatelské účty
##### Profil uživatele
- **Soubor** **složek** a **dat** obsahující **prostředí plochy** a **nastavení aplikací**
- Ukládají se v něm i **použitá síťová připojení**
	- Po přihlášení má uživatel k dispozici namapované jednotky vedoucí ke sdíleným složkám
##### Účty počítačů
- Podobně jako uživatelské účty se používají pro **ověření** a **audit přístupu počítače k síti** Windows a k **prostředkům domény**
- Každý počítač musí mít **jedinečný účet počítače**
- Účet počítače je možné použít pro **audit**
##### Skupiny
- **Množina** či **seznam** **uživatelských účtů** nebo **účtů počítačů**
- Na rozdíl od kontejneru se do skupiny **neukládají žádné údaje týkající se uživatele či počítače** (Skupina své členy pouze vypíše)
- Skupiny se s výhodou používají ke **zjednodušení správy**
	- Zejména k přiřazování práv a oprávnění
- Skupina se **zabezpečením** a **distribuční** skupina
##### Typy a rozsahy skupin
- **Podle rozsahu působnosti** (Doména, Strom, Les) se rozlišují skupiny:
	1) Místní doménová
	2) Globální
	3) Univerzální
##### Používání skupin
- Pro efektivní používání skupin na přiřazování oprávnění se používá zkratka **AGDLP**
	1) Accounts (Uživatelské účty)
	2) Global (Globální účty)
	3) Domain Local (Místní doménové účty)
	4) Permissions (Oprávnění)
- V případě používání **univerzálních skupin** se použije zkratka **AGUDLP**
##### Zásady skupiny
- **Nejmocnější funkce** Active Directory používané pro **konfiguraci prostředí účtů uživatelů** a **počítačů**
- Poskytují **centralizovanou správu** a **konfiguraci operačního systému** a **uživatelů** v prostředí Active Directory
##### Možnosti použití zásad skupiny
- Zásady skupiny lze použít na **úrovni pracovní stanice** (**místně**), případně na **různých úrovních** (**místa**, **domény** nebo **organizační jednotky**) v rámci Active Directory
- Na úrovni **míst**, **domén** či **organizačních jednotek** je daleko **více možností nastavení** než na úrovni místní
- **Při vlastním nasazení** se zásady skupiny aplikují v následujícím pořadí:
	1) Místní zásady skupiny
	2) Zásady skupiny na úrovni místa
	3) Zásady skupiny na úrovni domény
	4) Zásady skupiny na úrovni organizační jednotky
#### 3) Konfigurace a správa služby LDAP v UNIX-like operačních systémech
##### UNIX-Like OS - Chrakteristika Služby LDAP
- Základem LDAP je **záznam**, což je **informace**, kterou lze **jednoznačně identifikovat** pomocí **DN** (**Distinguished Name**)
- Každý záznam **má atribut** a **každému atributu je přiřazena jedna nebo více hodnot**
- Atribut se označuje **prostřednictvím řetězců**
##### UNIX-Like OS - Instalace
- Instalace OpenLDAP: `sudo apt install slapd ldap-utils`
- Spuštění služby LDAP: `systemctl start slapd`
- Povolení průchodu požadavkům přes firewall: `sudo ufw allow ldap`
- Po instalaci serveru LDAP je nutno **nainstalovat na klientská zařízení potřebné knihovny**, které zajistí připojení k serveru LDAP
##### UNIX-Like OS - Konfigurace a správa služby LDAP
1) Většinu **konfigurace zajistí** balíček `ldap-auth-config`:
	- Stačí zadat ID serveru LDAP, název báze vyhledávání LDAP a požadovanou verzi
	- Vytvoří se účet LDAP pro uživatele root a nastaví se heslo
	- Zadané údaje se uloží do `/etc/ldap.conf`
	 - Vytvoření účtu správce a přiřazení hesla příkazem `slappasswd`
2) Vytvoření souboru **LDIF** (ldaprootpasswrd.ldif) používaného pro **přidávání záznamů do adresáře** LDAP
	- Zde je třeba přidat tento obsah:
		- dn: olcDatabase={0}config,cn=config (název konkrétní instance databáze, obvykle se nacházi v souboru /etc/openldap/slapd.d/dn=config)
		- changetype: modify
		- add: olcRootPW
		- olcRootPW: {SSHA}PASSWORD_CREATED (hash získaný při vytvoření účtu správce LDAP)
3) Přidat **záznam lze pomocí URI odkazujícího na server LDAP** a výše zmiňovaný soubor
	- sudo ldapadd -Y EXTERNAL -H ldapi:// -f ldaprootpasswd.ldif
4) Poté je třeba **zkopírovat soubor slapd** do /var/lib/ldap a nastavit mu nutná oprávnění
	- sudo cp /usr/share/openldap-servers/DB_CONFIG.example /var/lib/ldap/DB_CONFIG
	- sudo chown -R ldap;ldap /var/lib/ldap/DB_CONFIG
	- sudo systemctl restart slapd
5) Následuje **import některých základních schémat LDAP** z /etc/openldap/schema
	- sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/cosine.ldif
	- sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/nis.ldif
	- sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/openldap/schema/inetorgperson.ldif
6) Nyní se **přidá doména do databáze LDAP** a vytvoří se **soubor ldapdomain.ldif pro doménu**
7) Tato konfigurace se přidá do databáze příkazem "sudo **ldapmodify** -Y EXTERNAL -H ldapi:/// -f ldapdomain.ldif"