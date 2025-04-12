#### 1) Správa uživatelů a skupin v OS Windows
##### Správa uživatelů v OS Windows
- **Přihlásit** se do **počítače** nebo do **domény**
- **Ověření identity uživatele** a k zjišťování, k čemu bude **uživatel přistupovat** a **jakou úroveň pověření** vlastní
- Lze také použít pro **audit**
- Místní a doménové uživatelské účty ve Windows
##### Profil uživatele
- **Soubor složek** a **dat obsahujících prostředí plochy** a **nastavení aplikací**
- Ukládají se v něm **použitá síťová připojení**
	- Při přihlášení má uživatel k dispozici namapované jednoty vedoucí ke sdíleným složkám
##### Účty počítačů
- Podobné jako uživatelské účty
- **Ověření** a audit **přistupu** počítače k síti Windows a k **prostředkům domény**
- Každý počítač **musí mít jedinečný účet** počítače
- Lze také použít pro **audit**
##### Správa skupin v OS Windows
- **Množina** či **seznam uživatelských účtů** nebo **účtů počítačů**
- Na rozdíl od **kontejnerů** se do skupiny **neukládají žádné údaje** týkající se **uživatele** či **počítače**
	- Skupina své členy pouze vypíše
- Skupiny se s výhodou používají ke **zjednodušení správy** (zejména přidělování oprávnění a práv)
- Typy skupin:
	1) Skupina se zabezpečením
	2) Distribuční skupina
- Typy a rozsahy skupin podle **rozsahu působnosti** (doména, strom, les)
	1) Místní doménová
	2) Globální
	3) Univerzální
- Pro efektivní používání skupin na přiřazování oprávnění se používá zkratka "**AGDLP**"
	1) Accounts
	2) Global
	3) Domain Local
	4) Permissions
- V případě používání univerzálních skupin se použije zkratka "**AGUDLP**"
##### Skupiny integrované v operačním systému
- **Výchozí integrované skupiny** mají již nastavena určitá **práva** a **oprávnění**:
	- Domain admins
	- Domain users
	- Account operators
	- Backup operators
	- Authenticated users
	- Everyone
##### Zásady skupiny
- **Nejmocnější funkce Active Directory** používané pro **konfiguraci prostředí** účtů **uživatelů** a **počítačů**
- Poskytují **centralizovanou správu** a **konfiguraci OS** a **uživatelů v Active Directory**
##### Možnosti použití zásad skupiny
- Lze uplatnit na **úrovni pracovní stanice**, popřípadě na **různých úrovních**:
	- Místa
	- Domény
	- Organizační jednotky
- Daleko **více možností nastavení** než na úrovní místní
- Při **vlastním nasazení** se zásady skupiny **aplikují v následujícím pořadí**:
	1) Místní zásady skupiny
	2) Zásady skupiny na úrovní místa
	3) Zásady skupiny na úrovni domény
	4) Zásady skupiny na úrovni organizační jednotky
#### 2) Přehled oprávnění ve Windows na úrovni souborového systému a na úrovni sdílení
##### Oprávnění
- **Typ přístupu**, který má **objekt** nebo **atribut objektu přiřazen**
	- Souborům a složkám u souborového systému NTFS, tiskárnám a objektům Active Directory
- **Přehled všech uživatelů a operací**, které mohou tito uživatelé na daném objektu provádět je **uložen v seznamu ACL**
	- V něm jsou tak uvedeni všichni uživatelé a skupiny, kteří mají přístup k objektu
- Lze **přiřadit oprávnění** pro **povolení** nebo **odepření přístupu**:
	- Odepření má vždy přednost
##### Typy oprávnění NTFS
1) **Explicitní oprávnění**:
	- Přiděluje se přímo souboru či složce
2) **Zděděná oprávnění**:
	- Přidělí se složce, rodičovskému objektu nebo kontejneru, a následně se přenáší i na potomky
3) **Efektivní oprávnění**:
	- Výsledná oprávnění
	- Pokud jsou uživatelské členy více skupin, pak se pro přístup ke konkrétnímu objektu aplikují různá oprávnění
	- Výsledkem kombinace oprávnění jsou efektivní oprávnění, která tak zahrnují explicitní a zděděná oprávnění
##### Sdílení složek
- Ke složkám **uloženým na serveru** uživatelé **nepřistupují přímo**, ale pomocí **sdílení složky**
- Doporučuje se **nastavit oprávnění** na **úrovni souborového systému NTFS** ale i **oprávnění pro sdílení**
- **Pro přístup** se používá notace **UNC** ve tvaru `\\název_serveru\název_sdílené_složky`
##### Oprávnění ke sdílení
- Při **nastavování oprávnění** jsou k dispozici **následující oprávnění**:****
	1) Úplné řízení
	2) Změnit
	3) Čist
##### Pokročilé nastavení sdílení
- **Přístup ke sdíleným složkám** a tiskárnám zajišťují **služby Workstation**
	- Server zajišťuje sdílení složek a tiskáren
- **Ve Windows Serveru** je třeba **síťové služby povolit** v sekci `Pokročilé nastavení sdílení v Centru sítí a sdílení`
##### Skryté sdílení
- Aby mohla být **složka** či **disk skryta** musí jejich název ro sdílení **končit znakem** "**$"**
- Ke složce se **přistupuje** pomocí **UNC**
#### 3) Správa uživatelů, skupin a oprávnění v UNIX-like OS
##### Přidávání uživatelských účtů
- Příkaz `useradd` nebo `adduser`
- **Po přidání** uživatelského účtu se **současně provedou tyto operace**:
	- Vytvoří se domovský adresář
	- Do domovského adresáře se nakopírují následující skryté soubory, kde se nachází proměnné prostředí pro relaci tohoto uživatele:
		1) `.bash_logout`
		2) `.bash_profile`
		3) `.bashrc`
	- Dále se vytvoří mail spool (soubor pro ukládání a práci s e-maily)
	- Vytvoří se skupina se stejným jménem
- Do souboru `/etc/passwd` se uloží **veškeré informace o uživatelském účtu** a to **v podobě záznamu** (`username : x : UID : GID : Comment : Home Directory : Default shell`)
	- Kde x  je ochrana účtu heslem (shadowed password), uloženým v souboru `/etc/shadow`.
- **Informace o skupině** se ukládá do souboru `/etc/group`
	- Záznam (`Group name : Group password : GID : Group members`)
		- Znak x v sekci `Group password` označuje, že skupina nepoužívá žádná hesla
##### Úprava uživatelských účtů
- Nástroj `usermod`
	- `usermod --expiredate 2022-10-30 --append --groups root, users --home /tmp --shell /bin/sh {nazev_uzivatele}`
	- Příznaky:
		1) `--expiredate` (datum vypršení účtu)
		2) `--a` (přidání uživatele do dalších skupin)
		3) `--d` nebo `--home` (změnění výchozího umístnění domovského adresáře)
		4) `--shell` (změnění shell uživatele)
- Příkazy `groups {username}` a `id {username}` pro zobrazení skupin, v nichž se uživatel členem
- Další operace:
	1) zákaz účtu uzamknutím hesla
		- `-l` nebo `--lock`
	2) odemknutí hesla
		- `-u` nebo `--unlock`
	3) odstranění uživatelského účtu a všech souborů
		-  `userdel --remove {username}`
##### Správa skupin
- `groupadd {name}` pro **vytvoření** nové skupiny
- `chown` pro **změnu** vlastníka skupiny
- `groupdel {group name}` pro **odstranění** skupiny
##### Oprávnění pro soubory a základní atributy
- **Atributy souborů** lze **zobrazit** příkazem `ls -l` a **atributy jsou ukryty v prvních deseti znacích**:
	- První znak označuje typ souboru:
		1) standardní soubor `-`
		2) adresář `-d`
		3) symbolický odkaz `-l`
		4) zařízení typu znak `-c`:
			- Char device, považuje za data proud bytů, např. terminál
		5) zařízení typu blok `-b` :
			- Block device, které pracuje s daty v blocích, např. úložiště
	- Zbylých devět znaků obsahuje vždy trojici oprávnění (read, write, execute) pro vlastníka souboru, skupinu vlastnící soubor a pro ostatní uživatele
##### Změna oprávnění
- Příkaz `chmod {new_model} file`
	- `{new_model}` je **řetězec, který obsahuje číslo v osmičkové soustavě** nebo **výraz definující nová oprávnění**
	- **Hodnoty oprávnění** pro **převod do osmičkové soustavy**:
		- `r` odpovídá 2^2 (4)
		-  `w` odpovídá 2^1 (2)
		-  `x` odpovídá 2^0 (1)
		- Žádné oprávnění odpovídá hodnotě 0
			- `a` označuje všechny uživatele
			-  `u` označuje konkrétního uživatele
			-  `g` označuje skupinu
			-  `o` označuje ostatní uživatele
				- Přidělení oprávnění pomocí znaku `+`
				- Odebrání oprávnění pomocí znaku `-`
	- Příklady: (udělení oprávnění rwx pro vlastníka, oprávnění r pro skupinu vlastnící soubor a pro ostatní uživatele)
		- `--rwxr--r-- nebo 744 (4+2+1; 4+0+0; 4+0+0;)`
		- `chmod a+rwx, g-wx, o-wx file.txt" nebo "chmod 744 file.txt`
	- **Změna skupiny vlastnící soubor** na jinou skupinu příkazem `chgrp {new_group} {file}`
	- **Změna vlastníka souboru** na jiného vlastníka příkazem `chown {user} {file}`
#### 4) ACL a kvóty v UNIX-like OS
##### ACL v Unix-Like OS
- Umožňují **podrobnější přiřazování oprávnění** k souborům a adresářům než **stadnardní ugo/rwx oprávnění**
	- Přidělit různá oprávnění různým uživatelům
- **ACLs** podporují pouze **souborové systémy připojené** (**mountované**) s **volbou** "**acl**"
	- Ověřit podporu lze příkazem `tune2fs -l {disk} | grep "Default mount options"`:
	- Zakázat ACL lze ve `/etc/fstab` volbou `noacl`
- Dva typy ACL:
	1) Access ACL
		- Lze použít na soubory i adresáře
	2) Default ACL 
		- Lze použít pouze na adresáře
		- Pokud soubory v adresáři s default ACL nemají vlastní ACL, dědí jej z rodičovského adresáře
1) **Ověření** aktuální konfigurace:
	 - `getfactl {soubor}`
2) **Nastavení**:
	- `setfactl -m u:{user}:rw {soubor}`
3) **Přidělení** default ACL pomocí parametru d:
	- `setfacl -m d:o:r {soubor}`
4) **Odebrání** konkrétního oprávnění 
	- `setfactl -x d:o {soubor}`
5) **Odebrání** všech oprávnění:
	- `setfacl -b {soubor}`
6) **Příklad** nastavení ACL na adresář pro uživatele (přiřazení oprávnění read, write a execute):
	- `setfactl -m u:{user}:rwx /home/backups/`
##### Diskové kvóty v UNIX-LIKE OS
- Omezení kapacity disku uživatelům či skupinám, aby nedošlo k zaplnění
- **Softlimit** 
	- Limit na vyčerpání kvóty
- **Hardlimit** 
	- Limit na dosažení kvóty
- **Postup konfigurace** diskových kvót:
	1) Povolení diskových kvót připojením souborového systému s volbami `usrquota` nebo `grpquota` v souboru `/etc/fstab`
	2) Odpojení a zpětné připojení souborových systémů (mount)
	3) Ověření voleb `usrquota` a `grpquota` ve výstupu příkazu `mount`
	4) Inicializace a povolení kvót:
		- `quotacheck` (ověření kvót)
		- `quataon` (povolení kvót)
		- `quataoff` (zákaz kvót)
- Příklad nastavení varování (softlimit) a dosažení kvóty (hardlimit) na vyčerpání kvóty
	- `edquota -u {user}" a pro skupinu "edquota -g {groups}`
- Nastavení grace period "`edquota -t`"
	- Nastavení hodnot "`Block grace period`" a "`Inode grace period`" 
	- Uplatňují se na celý operační systém
- Vytvoření přehledu kvót pro uživatele, skupinu či souborový systém příkazem `repquota -v {cesta k souborovému systému}`