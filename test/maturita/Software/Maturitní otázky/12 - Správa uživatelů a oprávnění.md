#### 1) Správa uživatelů a skupin v OS Windows

##### Správa uživatelů v OS Windows
- Umožňují přihlásit se do počítače nebo do domény
- Slouží k ověření identity uživatele a následně k zjišťování, kčemu bude uživatel přistupovat a jakou úroveň pověření vlastní
- Uživatelský účet lze také použít pro audit
- V soudobých sítích s prvky s nainstalovaných operačním systémem Windows se používají místní a doménové uživatelské účty

##### Správa uživatelů v OS Windows - Profil uživatele
- Soubor složek a dat obsahujících prostředí plochy a nastavení aplikací
- Ukládají se v něm použitá síťová připojení (při přihlášení má uživatel k dispozici namapované jednoty vedoucí ke sdíleným složkám)

##### Správa uživatelů v OS Windows - Účty počítačů
- Podoné jako uživatelské účty
- Používají se pro ověření a audit přistupu počítače k síti Windows a k prostředkům domény
- Každý počítač musí mít jedinečný účet počítače
- Lze také použít pro audit

##### Správa skupin v OS Windows
- Množina či seznam uživatelských účtů nebo účtů počítačů
- Na rozdíl od kontejnerů se do skupiny neukládají žádné údaje týkající se uživatele či pocítače
	- Skupina své členy pouze vypíše
- Skupiny se s výhodou používají ke zjednodušení správy (zejména přidělování oprávnění a práv)
- Typy skupin
	- skupina se zabezpečením
	- distribuční skupina
- Typy a rozsahy skupin podle rozsahu působnosti (doména, strom, les)
	- Místní doménová
	- Globální
	- Univerzální
- Pro efektivní používání skupin na přiřazování oprávnění se používá zkratka "AGDLP"
	- Accounts
	- Global
	- Domain Local
	- Permissions
- V případě používání univerzálních skupin se použije zkratka "AGUDLP"

##### Správa skupin v OS Windows - Skupiny integrované v operačním systému
- Výchozí integrované skupiny mají již nastavena určitá práva a oprávnění:
	- Domain admins
	- Domain users
	- Account operators
	- Backup operators
	- Authenticated users
	- Everyone

##### Správa skupin v OS Windows - Zásady skupiny
- Nejmocnější funkce Active Directory používané pro konfiguraci prostředí účtů uživatelů a počítačů
- Pokytují centralizovanou správu a konfiguraci OS a uživatelů v Active Directory

##### Správa skupin v OS Windows - Možnosti použití zásad skupiny
- Lze uplatnit na úrovni pracovní stanice, popřípadě na různých úrovních (místa, domény nebo organizační jednotky)
- Na úrovni míst, domén či organizačních jednotek je daleko více možností nastavení než na úrovní místní
- Při vlastním nasazení se zásady skupiny aplikakují v následujícím pořadí:
	- Místní zásady skupiny
	- Zásady skupiny na úrovní místa
	- Zásady skupiny na úrovni domény
	- Zásady skupiny na úrovni organizační jednotky

#### 2) Přehled oprávnění ve Windows na úrovni souborového systému a na úrovni sdílení
##### Oprávnění
- Typ přístupu, který má objekt nebo atribut objektu přiřazen
- Nejčastěji se přiřazuje souborům a složkám u souborového systému NTFS, tiskárnám a objektům Active Directory
- Přehled všech uživatelů a operací, které mohou tito uživatelé na daném objektu provádět je uložen v seznamu ACL
	- V něm jsou tak uvedeni všichni užiatelé a skupiny, kteří mají přístup k objektu
- Lze přiřadit oprávnění pro povolení nebo odepření přístupu (odepření má vždy přednost)

##### Typy oprávnění NTFS
- Excplicitní oprávnění
	- přiděluje se přímo souboru či složce
- Zděděná
	- Tato oprávnění se přidělí složce (rodičovskému objektu nebo kontejneru) a následně se přenáší i na potomky
- Edektivní
	- Výsledná oprávnění
	- Pokud jsou uživatelské členy více skupin, pak se pro přístup ke kontkrétnímu objektu aplikují různá oprávnění
	- Výsledkem kombinace oprávnění jsou efektivní oprávnění, která tak zahrnují explicitní a zděděná oprávnění

##### Sdílení složek
- Ke složkám uloženým na serveru uživatelé nepřistupují přímo, ale pomocí sdílení složky
- Doporučuje se nastavit oprávnění na úrovni souborového systému NTFS ale i oprávnění pro sdílení
- Pro přístup se používá notace UNC ve tvaru "\\název_serveru\název_sdílené_složky"

##### Oprávnění ke sdílení
- Při nastavování oprávnění jsou k dispozici následující oprávnění:
	- úplné řízení
	- změnit
	- čist
##### Pokročilé nastavení sdílení
- Přístup ke sdíleným složkám zajišťují služby Workstation (přístup ke sdíleným složkám tiskárnám) a Server (zajišťuje sdílení složek a tiskáren)
- Ve Windows Serveru je třeba síťové služby povolit v sekci "Pokročilé nastavení sdílení v Centru sítí a sdílení"

##### Skryté sdílení
- Aby mohla být složka či disk skryta musí jejich název ro sdílení končit znakem "$"
- Ke složce se přistupuje standardním způsobem (UNC)
- Skryté sdílení lze vytvořit pro libovolnou sdílenou složku
- Existuje i administrativní sdílení, kde jsou sdíleny celé disky
#### 3) Správa uživatelů, skupin a oprávnění v UNIX-like OS

##### Přidávání uživatelských účtů
- Příkaz "useradd" nebo "adduser"
- Po přidání uživatelského účtu se současně provedou tyto operace:
	- Vytvoří se domovský adresář
	- do domevského adresáře se nakopírují následující skryté soubory, kde se nachází proměnné prostředí pro relaci tohoto uživatele:
		- ".bash_logout"
		- ".bash_profile"
		- ".bashrc"
	- Dále se vytvoří mail spool (soubor pro ukládání a práci s e-maily)
	- Vytvoří se skupina se stejným jménem
- do souboru "/etc/passwd" se uloží veškeré informace o uživatelském účtu a to v podobě záznamu (username : x : UID : GID : Comment : Home Directory : Default shell)
	- Kde x  je ochrana účtu heslem (shadowed password), uloženým v souboru "/etc/shadow".
- Informace o skupině se ukládá do souboru "/etc/group"
	- Záznam (Group name : Group password : GID : Group members)
		- Znak x v sekci "Group password" označuje, že skupina nepoužívá žádná hesla
##### Úprava uživatelských účtů
- příkaz "usermod" (usermod --expiredate 2022-10-30 --append --groups root, users --home /tmp --shell /bin/sh test)
	- příznaky:
		- --expiredate (datum vypršení účtu)
		- --aG (přidání uživatele do dalších skupin)
		- --d nebo --home (změnění výchozího umístnění domovského adresáře)
		- --shell (změnění shell uživatele)
- Příkazy "groups {username}" a "id {username}" pro zobrazení skupin, v nichž se uživatel členem
- Další operace:
	- zákaz účtu uzamknutím hesla (-l nebo --lock)
	- odemknutí hesla (-u nebo --unlock)
	- odstranění uživatelského účtu a všech souborů příkazem "userdel --remove {username}"

##### Správa skupin
- příkaz "groupadd {name}" pro vytvoření nové skupiny
- příkaz "chown" pro změnu vlastníka skupiny
- příkaz "groupdel {group name}" pro odstranění skupiny

##### Oprávnění pro soubory a základní atributy
- Atributy souborů lze zobrazit příkazel "ls -l" a atributy jsou ukryty v prvních deseti znacích:
	- První znak označuje typ souboru:
		- standardní soubor "-"
		- adresář "-d"
		- symbolický odkaz "-l"
		- zařízení typu znak "-c" (char device, považuje za data proud bytů, např. terminál) 
		- zařízení typu blok "-b" (block device, které pracuje s daty v blocích, např. úložiště)
	- Zbylých devět znaků obsahuje vždy trojici oprávnění (read, write, execute) pro vlastníka souboru, skupinu vlastnící soubor a pro ostatní uživatele

##### Změna oprávnění
- Příkaz "chmod {new_model} file"
	- {new_model} je řetězec, který obsahuje čílo v osmičkové soustavě nebo výraz definující nová oprávnění
	- Hodnoty oprávnění pro převod do osmičkové soustavy:
		- oprávnění "r" odpovídá 2^2 (4)
		- oprávnění "w" odpovídá 2^1 (2)
		- oprávnění "x" odpovídá 2^0 (1)
		- Žádné oprávnění odpovídá hodnotě 0
	- Znak "a" označuje všechny uživatele
	- Znak "u" označije konkrétního uživatele
	- Znak "g" označuje skupinu
	- Znak "o" označuje ostatní uživatele
	- Přidělení oprávnění pomocí znaku "+"
	- Odebrání oprávnění pomocí znaku "-"
	- Příklady: (udělení oprávnění rwx pro vlastníka, oprávnění r pro skupinu vlastnící soubor a pro ostatní uživatele)
		- --rwxr--r-- nebo 744 (4+2+1; 4+0+0; 4+0+0;)
		- "chmod a+rwx, g-wx, o-wx file.txt" nebo "chmod 744 file.txt"
	- Změna skupiny vlastnící soubor na jinou skupinu příkazem "chgrp {new_group} {file}"
	- Změna vlastníka souboru na jiného vlastníka příkazem "chown {user} {file}"
#### 4) ACL a kvóty v UNIX-like OS
##### ACL v Unix-Like OS
- umožňují podrobnější přiřazování oprávnění k souborům a adresářům než stadnardní ugo/rwx oprávnění
	- Například přidělit různá oprávnění různým uživatelům
- ACL podporují pouze souborové systémy připojené (mountované) v volbou "acl"
	- Ověřit podporu lze příkazem "tune2fs -l {disk} | grep "Default mount options:""
	- Zakázat acl lze ve "/etc/fstab" volbou "noacl"
- Dva typy ACL:
	- access ACL (Lze použít na soubory i adresáře)
	- default ACL (Lze použít pouze na adresáře)
		- pokud soubory v adresáři s default ACL nemají vlastní ACL, dědí jej z rodičovského adresáře
- Ověření aktuální konfigurace ACL příkazem "getfactl {soubor}"
- Nastavení ACL příkazem "setfactl -m u:{user}:rw {soubor}"
- Přidělení default ACL pomocí paremtru d příkazem "setfacl -m d:o:r {soubor}"
- Odebrání konkrétního opravnění příkazem "setfactl -x d:o {soubor}"
- Odebrání všech oprávnění příkazem "setfacl -b {soubor}"
- Příklad nastavení ACL na adresář pro uživatele (přiřazení oprávnění read, write a execute)
	- "setfactl -m u:{user}:rwx /home/backups/"

##### Diskové kvóty v UNIX-LIKE OS
- pomocí diskových kvót se omezuje uživatelům či skupinám kapacita disku, kterou mají k dispozici, aby nedošlo k zaplnění
- Softlimit je limit na vyčerpání kvóty
- Hardlimit je limit na dosažení kvóty
- Postup konfigurace diskových kvót:
	- povolení diskových kvˇot připojením souborového systému s volbami "usrquota" nebo "grpquota" v souboru "/etc/fstab"
	- odpojení a zpětné připojení souborových systémů (mount)
	- ověření voleb "usrquota" a "grpquota" ve výstupu příkazu "mount"
	- inicializace a povolení kvót
		- quotacheck (ověření kvót)
		- quataon (povolení kvót)
		- quataoff (zákaz kvót)
- Příklad nastavení varování (softlimit) a dosažení kvóty (hardlimit) na vyčerpání kvóty
	- "edquota -u {user}" a pro skupinu "edquota -g {groups}"
	- nastavení grace period "edquota -t"
		- Zde nastavovat hodnoty "Block grace period" a "Inode grace period" 
		- Tyto hodnoty se uplatňují na celý operační systém
- Vytvoření přehledu kvót pro uživatel, skupinu či souborový systém příkazem "repquota -v {cesta k souborovému systému}"