#### 1) Obecná charakteristika služeb WWW a FTP

##### FTP (File Transfer Protocol)
- Pasivní režim
	- klient navazuje jak na řídící, tak na datové spojení se serverem FTP
- Používá TCP na portu 20 a 21
- FTP je možné použít s ověření pomocí hesla a uživatelského jména nebo s anonymním přístupem
- Přenos dat i ověřovacích informací probíhá nešifrovaně, pro šifrovaný provoz je nutno použít SFTP (SSH File Transfer Protocol) nebo FTPS (FTP over SSL), které zajišťují šifrování přes SSL nebo TLS
##### WWW (World Wide Web)
- Systém navzájem propojených hypertextových dokumentů, které se dají prohlížet internetovým prohlížečem
- Stránky jsou uloženy na webovém serveru, který používá protokol TCP na portu 80 a s SLL na portu 443
- Pro zabezpečení citlivých údajů se používá protokol SSL

#### 2) Konfigurace a správa služby WWW v OS Windows a v UNIX-like OS

##### UNIX-Like OS - Konfigurace a správa služby WWW (Server Apache)
- Webový server Apache představuje robustní a spolehlivou variantu FOSS (Free and Open Source Software) serveru HTTP
- Podporuje provoz více webů na jednom počítači
- Je vhodné nainstalovat i proxy server a deamona pro web-cache s názvem Squid a vylepšení SquidGuard, který provádí přesměrování a nasazení blacklistů
- Adresář pro uložení webových stránek a dalších dokumentů je definován v direktivě DocumentRoot
	- Místo, které slouží jako výchozí pro vyřízení požadavků na server
- V případě podpory pro více webů má každý virtuální host vlastní adresář definovaný v direktivě DocumentRoot
	- Definici každého virtuálního hosta je třeba přidat do samostatného souboru v adresáři /etc/httpd/conf.d
- Pokud mají být jednotlivé weby přístupné z jiných počítačů, je třeba u nich přidat do souboru /etc/host příslušné záznamy
- Definování portu či adresy/portu se definuje v direktivě Listen
- Instalace prostřednictvím příkazů:
	- yum update && yum install httpd (Centos, squid squidGuard pro Squid)
	- apt-get udpate && apt-get install apache2 (ubuntu, squid3 squidguard pro Squid)
- Následně je vhodné nastavit, aby se služba spouštěla při startu (např. systemctl enable {service})
- Ověření příkazem "ps -ef | grep -Ei '(apache|httpd)' | grep -v grep" (kontrola přítomnosti deamona apacke nebo httpd)
- Konfigurační soubor se nachází:
	- v /etc/apache2/apache2.conf pro ubuntu
	- v /etc/httpd/conf/httpd.conf pro centos
- Omezení přístupu k internetové stránce lze definovat pomocí několika metod ověřování (např. uživatelské jméno a heslo)
- Instalace a konfigurace SSL:
	- Balíček mod_ssl
	- Je vhodné vytvořit adresář pro uložení certifikátů
	- Vygenerování certifikátu podepsaného sám sebou a klíče pro jeho ochranu:
		- openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/httpd/ssl-certs/apache.key -out /etc/httpd/ssl-certs/apache.crt
	- Doplnění následujících řádků do konfiguračního souboru virtuálního hosta (nebo do odpovídající části souboru /etc/httpd/conf/httpd.conf)
		- SSLEngine on
		- SSLCertificateFile /etc/httpd/ssl-certs/apache.crt
		- SSLCertificateKeyFile /etc/httpd/ssl-certs/apache.key
	- Poté je třeba server Apache restartovat

##### OS Windows - Konfigurace a správa služby WWW //TODO dodělat z prezentace, je to tam lip popsaný (LESSON 7)
- Instalace role Web Server (IIS) a přidat funkci Application Development pro vytvoření prostředí pro vývoj a hostování webových aplikací
- Server Manager -> Add roles and features -> role webového serveru a ftp
- Správa serveru pomocí Windows Administrative Tools / Internet Information Services (IIS) Manager
- Web je ve výchozí konfiguraci uložen v "C:\Inetpub\wwwroot"
- Certifikát SSL lze přidat v IIS Manageru v položce serveru, při zobrazení funkcí (features view) -> Server Certificates
	- Zde lze vytvořit vlastní certifikát
	- Dále je potřeba vytvořit vazbu webu na protokol https (Actions -> Bindings -> nastavit port i na 443)
		- Pod položkou SSL Certificate se vybere daný SSL certifikát
	- Pokud je nutné, aby se dalo k webu připojit pouze přes protokol https, je nezbytné to nastavit v IIS\SSL Settings
		- Stejně tak je možno zajistit připojení pouze ověřených klientů, nastavením v sekci Client certificates -> Require (ověřování identity klientů pomocí klientských certifikátů)
- Nastavení výchozí domovské stránky lze provést v IIS/Default Document a přesunout vlastní stránku na první místo
- Vytvořit další web lze přidáním složky do "C:\inetpub" a v IIS Manageru rozbalit strom serveru -> Sites -> Add Website, kde jsou tyto parametry:
	- Site Name
	- Physical Path
	- Hostname
- Poté je třeba zajistit správný překlad názvů na IP adresu v konzoli DNS
#### 3) Konfigurace a správa služby FTP v OS Windows a v UNIX-like OS.

##### UNIX-like OS - Konfigurace a správa služby FTP
- Balíček vsftpd (Very Secure FTP Deamon)
- Na straně klienta se používá program ftp
- V Centos je třeba službu spustit a povolit
- V Ubuntu by měl deamon být spuštěn a nastaven tak, aby se zaváděl po startu systému
- Server FTP se konfiguruje v souboru vsftpd.conf
- Povolení anonymního přístupu do adresáře /storage/ftp:
	- anonymous_enable=YES
	- no_anon_password=YES
	- anon_root=/storage/ftp/ (pokud se tento řádek neuvede, použije se adresář /var/ftp, což je domovský adresář uživatele ftp vytvořeného při instalaci)
- Povolení přístupu pouze pro čtení:
	- write_enable=NO
- Pokud bude vypnut anonymní přístup, lze nastavit, aby se místní uživatelé k serveru FTP přihlašovali svými přihlašovacími údaji:
	- local_enable=YES
- Omezení ověřených uživatelů ro přístup pouze ke svým domovským adresářům:
	- chroot_local_user=YES
	- chroot_list_enable=YES
	- chroot_list_file=/etc/vsftpd/chroot_list
- Omezení šířky pásma:
	- anon_max_rate=10240
	- local_max_rate=20480
	- max_per_ip=5
- Omezení datového kanálu na porty TCP v rozsahu 15000 až 15500 (volitlené nastavení portů)
	- pasv_enable=YES
	- pasv_max_port=15000
	- pasv_min_port=15500
- Nastavení uvítací zprávy:
	- ftpd_banner="ahoj"
- Povolení průchodu provozu FTP přes firewall:
	- firewall-cmd --add-service=ftp
	- firewall-cmd --add-port=15000-15500/tcp
- Dále je nutno načíst modul ip_conntrack_ftp:
	- modprobe ip_contntrack_ftp
	- A nastavit jej na trvalé zavádění po každém spuštění systému (v CentOS přidat do souboru /etc/sysconfigPiptables-config řádek IPTABLES_MODULES="ip_contrack_ftp a v Ubuntu přidání řádku "ip_conntrack_ftp" do /etc/modules)
- Otestovat FTP server lze prohlížečem (ftp:// {ip adresa serveru}) nebo příkazu "ftp localhost", stáhnout soubor lze příkazem "get vsftpd {soubor}"

##### OS Windows - Konfigurace a správa služby FTP
- FTP server lze vytvořit v IIS Manageru jako FTP Server s vazbou na konkrétní web (Sites/Actions/Add FTP Site)
	- Lze u něj použít SSL certifikát obdobným způsobem, jako u WWW serveru
	- Zde se zadá název domény (FTP/FTP Authentication/Basic Authentication/Edit)
	- Ve FTP Authorization Rules lze definovat správce
	- V Sekci FTP FIrewall Support zadat ip adresu serveru
	- v Sekci FTP Messages lze definovat uvítací zprávu
	- Nastavení SSL v sekci FTP SSL Settings
	- Nastavení izolace uživatelů v sekci FTP User Isolation
- Nebo vytvořit jako samostaný FTP Server:
	- IIS -> Sites -> Actions -> Add FTP Site -> Průvodce (stejné jako s vazbou na web) -> Binding and SSL Settings -> Definice IP Adres -> SSL Certifikát -> Authentication:
		- Anonymous (Bez hesla, uživatelské jméno anonymous nebo ftp)
		- Basic (jméno + heslo)
	- -> Authorization -> Allow Access To:
		- All Users
		- Anonymous Users
		- Specified Roles or user groups
		- Specified users
- V IIS/Sites/Actions/Set FTP Site Default lze přepsat výchozí hodnoty FTP Serveru jako například:
	- Automatické spuštění
	- Povolení znakové sady UTF-8
	- Časový limit řídícího kanálu
	- Časový limit datového kanálu
	- Maximální počet připojení
- Po konfiguraci je potřeba povolit port 20 a 21 ve firewallu (nebo ověřit výskyt pravidel FTP Traffic-In nebo FTP Traffic-Out) a výskyt pravidla pro pasivní režim FTP (FTP Server Passive), které otvírá rozsah místních portů TCP 1024-65535