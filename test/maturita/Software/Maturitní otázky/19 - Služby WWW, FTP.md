#### 1) Obecná charakteristika služeb WWW a FTP
##### FTP (File Transfer Protocol)
- Pasivní režim
	- Klient navazuje jak na řídící, tak na datové spojení se serverem FTP
- Používá `TCP21/22`
- Je možné použít s **ověření pomocí hesla a uživatelského jména** nebo s **anonymním přístupem**
- Přenos dat i ověřovacích informací probíhá **nešifrovaně**, pro šifrovaný provoz je nutno použít `SFTP` (SSH File Transfer Protocol) nebo `FTPS` (FTP over SSL)
##### WWW (World Wide Web)
- Systém navzájem **propojených hypertextových dokumentů**, které se dají prohlížet internetovým prohlížečem
- Stránky jsou uloženy na webovém serveru, který používá protokol `TCP:80` a s SLL na  `TCP:443`
#### 2) Konfigurace a správa služby WWW v OS Windows a v UNIX-like OS
##### UNIX-Like OS - Konfigurace a správa služby WWW (Server Apache)
- Představuje **robustní a spolehlivou variantu** `FOSS` (Free and Open Source Software) serveru `HTTP`
- Podporuje **provoz více webů** na jednom počítači
- Je vhodné **nainstalovat i proxy server** a **deamona pro web-cache**  **Squid** a vylepšení **SquidGuard**, který provádí přesměrování a nasazení blacklistů
- Adresář pro uložení webových stránek a dalších dokumentů je definován v direktivě `DocumentRoot`, v případě více webů má každý virtuální host svoji direktivu
	- Místo, které slouží jako výchozí pro vyřízení požadavků na server
	- Definici každého virtuálního hosta je třeba přidat do samostatného souboru v adresáři /etc/httpd/conf.d
- Definování portu či adresy a portu se definuje v direktivě `Listen`
- Konfigurační soubor se nachází:
	- `/etc/apache2/apache2.conf` pro ubuntu
	- `/etc/httpd/conf/httpd.conf` pro centos
- Instalace a konfigurace SSL:
	- Balíček `mod_ssl`
	- Doplnění následujících řádků **do konfiguračního souboru virtuálního hosta**
		- `SSLEngine on`
		- `SSLCertificateFile {cesta}`
		- `SSLCertificateKeyFile {cesta}`
##### OS Windows - Konfigurace a správa služby WWW
- Instalace role **Web Server** v **IIS** a přidání funkce **Application Development** pro vytvoření prostředí pro vývoj a hostování webových aplikací
	- Server Manager -> Add roles and features -> role webového serveru a ftp
- Správa serveru pomocí **Windows Administrative Tools** nebo **Internet Information Services** (IIS) 
- Web je ve výchozí konfiguraci uložen v `C:\Inetpub\wwwroot`
- **Certifikát SSL** lze přidat v **IIS**  v položce serveru v **Server Certificates**:
	- Zde lze vytvořit vlastní certifikát
	- Vytvoření vazby webu na protokol https (**Actions** -> **Bindings** -> **nastavit port i na 443**)
	- Pokud je nutné, aby se dalo k webu připojit pouze přes protokol `https`, je nezbytné to nastavit v **IIS\SSL Settings**
		- Stejně tak je možno zajistit připojení pouze ověřených klientů, nastavením v sekci Client certificates -> Require (ověřování identity klientů pomocí klientských certifikátů)
- Nastavení výchozí domovské stránky lze provést v **IIS/Default Document**
- Vytvořit další web lze přidáním složky do `C:\inetpub` a v **IIS Manageru** rozbalit strom serveru -> **Sites** -> **Add Website**, kde jsou tyto parametry:
	- Site Name
	- Physical Path
	- Hostname
- Poté je třeba zajistit správný překlad názvů na IP adresu v konzoli DNS
#### 3) Konfigurace a správa služby FTP v OS Windows a v UNIX-like OS.
##### UNIX-like OS - Konfigurace a správa služby FTP
- Balíček **vsftpd** (Very Secure FTP Deamon)
	- Na straně klienta se používá program ftp
- Server `FTP` se **konfiguruje** v souboru `vsftpd.conf`
1) **Povolení anonymního přístupu do adresáře** `/storage/ftp`:
	- anonymous_enable=YES
	- no_anon_password=YES
	- anon_root=/storage/ftp/ (pokud se tento řádek neuvede, použije se adresář /var/ftp, což je domovský adresář uživatele ftp vytvořeného při instalaci)
2) **Povolení přístupu pouze pro čtení**:
	- write_enable=NO
3) **Pokud bude vypnut anonymní přístup, lze nastavit, aby se místní uživatelé k serveru FTP přihlašovali svými přihlašovacími údaji**:
	- local_enable=YES
4) **Omezení ověřených uživatelů pro přístup pouze ke svým domovským adresářům**:
	- chroot_local_user=YES
	- chroot_list_enable=YES
	- chroot_list_file=/etc/vsftpd/chroot_list
5) **Nastavení uvítací zprávy**:
	- ftpd_banner="ahoj"
- Otestovat FTP server lze prohlížečem `ftp:// {ip adresa serveru}` nebo příkazu `ftp localhost`, stáhnout soubor lze příkazem `get vsftpd {soubor}`
##### OS Windows - Konfigurace a správa služby FTP
1) lze vytvořit v **IIS Manageru** jako **FTP Server s vazbou na konkrétní web** (Sites/Actions/Add FTP Site)
	- Lze u něj použít SSL certifikát
	- Zde se zadá název domény
	- v Sekci FTP Messages lze definovat uvítací zprávu
	- Nastavení SSL v sekci FTP SSL Settings
	- Nastavení izolace uživatelů v sekci FTP User Isolation
2) Nebo vytvořit jako samostaný FTP Server:
	- **IIS** -> **Sites** -> **Actions** -> **Add FTP Site** -> Průvodce (stejné jako s vazbou na web) -> **Binding and SSL Settings** -> **Definice IP Adres** -> **SSL Certifikát** -> **Authentication**:
		- Anonymous (Bez hesla, uživatelské jméno anonymous nebo ftp)
		- Basic (jméno + heslo)
	- -> **Authorization** -> **Allow Access To**:
		- All Users
		- Anonymous Users
		- Specified Roles or user groups
		- Specified users
- V **IIS/Sites/Actions/Set FTP Site Default** lze přepsat **výchozí hodnoty FTP Serveru** jako například:
	- Automatické spuštění
	- Povolení znakové sady UTF-8
	- Časový limit řídícího kanálu
	- Časový limit datového kanálu
	- Maximální počet připojení
- Po konfiguraci je potřeba povolit port `TCP21` a` TCP22` ve firewallu (nebo ověřit výskyt pravidel FTP Traffic-In nebo FTP Traffic-Out) a výskyt pravidla pro pasivní režim FTP (FTP Server Passive), které otvírá rozsah místních portů `TCP 1024-65535`