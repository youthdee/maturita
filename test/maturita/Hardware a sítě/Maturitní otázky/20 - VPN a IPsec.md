#### 1) Účel a výhody použití VPN

##### Vlastnosti sítí VPN
- Poskytují zpravidla zabezpečená end-to-end spojení
- Jsou virtuální proto, že umožňují přenos chráněných dat skrze veřejné sítě (Internet)
- Zabezpečení dat je řešeno šifrováním
##### Výhody sítí VPN
- Úspora nákladů
	- Nasazení VPN umožnil rozvoj vysokorychlostního připojení k Internetu
- Bezpečnost
	- S použitím moderních šifrovacích standardů poskytují vysokou úroveň zabezpečení datových přenosů
- Škálovatelnost
	- Skrze Internet lze snadno propojovat nové lokality
- Kompatibilita
	- VPN lze implementovat pomocí mnoha různých přenosových standardů
#### 2)Typy VPN

##### VPN typu Site-to-Site
- Poskytují transparentní způsob propojení sítí LAN
- Spojují sítě skrze veřejnou síť (Internet)
	- Jednodušší a levnější způsob oproti pronájmu dedikovaného spoje
- Koncové uzly mohou vzájemně komunikovat nešifrovaně
	- Koncová zařízení o VPN vůbec nemusí vědět
- Zapouzdření a šifrování provozu se provádí na VPN bránách (Gateways)
	- Odesílající brána (Gateway) paket zašifruje adoplní o potřebná záhlaví
	- Přijímající brána paket zbaví přidaných záhlaví a dešifruje jej
- IPsec VPN, GRE over IPsec, Cisco Dynamic Multipoint Virtual Private Network (DMVPN), IPsec Virtual Tunnel Interface (VTI)

##### VPN typu Remote Access
- Umožňují zabezpečené připojení k firemní síti
- Zpravidla aktivovány uživatelem dle potřeby
- Clientless (SSL pomocí webového prohlížeče) a Client-Based (IPsec VPN připojení pomocí klienty)
##### VPN s využitím SSL/TLS
- Využívají infrastrukturu veřejného klíče (PKI) a certifikáty, pomocí nich probíhá autentizace účastníků
- Omezená podpora aplikací  (pouze webové aplikace a sdílení souborů)
- Průměrná odolnost autentizace (jednocestná či dvoucestná autentizace)
- Střední či vysoká odolnost šifrování (Délky klíčů od 40 do 256 bitů)
- Nízká složitost připojení (Vyžaduje pouze webový prohlížeč)
- Široké možnosti připojení (Lze připojit jakékoliv zařízení s webovým prohlížečem)

##### VPN s využitím IPsec
- Široká podpora aplikací (všechny aplikace užívající IP)
- Vysoká odolnost autentizace (dvoucestná autentizace se sdíleným klíčem či certifikáty)
- Vysoká odolnost šifrování (délky klíčů od 56 do 256 bitů)
- Střední složitost připojení (Vyžaduje nainstalovanou aplikaci VPN klienta)
- Omezené možnosti připojení (Pouze pro specifická zařízení se specifickou konfigurací)
##### Podnikové VPN
- Zřizovány prostřednictvím Internetu
##### VPN poskytovatelů služeb
- Umožňují oddělit provoz různých klientů
- L2 MPLS, L3 MPLS, Frame Relay, Asynchronous Transfer Mode (ATM)

##### GRE over IPsec (Generic Routing Encapsulation)
- Nezabezpečený Site-To-Site VPN tunelovací protokol
	- Samotný nepodporuje autentizaci ani šifrování
- Umožňuje zapouzdření různých protokolů (včetně multicast a broadcast provozu)
- Pro zabezpečení komunikace lze zapouzdřít pomocí IPsec
	- Standardní IPsec VPN podporuje pouze unicastový provoz
	- Umožňuje zabezpečit multicastovou komunikaci (např. pro potrřeby komunikace dynamických směrovacích protokolů)
- Princip zapouzdření:
	- Passanger protocol (přenášený protokol)
		- Je Protokolem datového paketu určeného k zapozdření pomocí GRE
	- Carrier protocol (přepravní protokol)
		- GRE je přepravním protokolem zapouzdřujícím datový paket
	- Transport protocol (transportní či přenosový protokol)
		- Protokol, který zajišťuje vlastní přenos zapouzdřeného paketu (např IP)

##### Dynamic Multipoint VPN (DMVPN)
- Nasazení Site-to-Site VPNs v podnikových sítích je většinou problematické, v případě množství poboček to znamená komplexní konfiguraci
- DMVPN nabízí flexibilní způsob propojení centrály a poboček
	- Zjednodušuje konfiguraci VPN  umožňuje vznik virtuálních spojů
- Základní infrastruktura používá topologii Hub-and-Spoke
	- Pobočkové brány mají konfiguraci VPN spojení s centrálou
- Virtuální pobočkové spoje odpovídají topologii Full Mesh
	- Centrála zprostředkuje konektivitu mezi pobočkovými branami
##### IPsec Virual Tunnel Interface (VTI)
- Zjednodušuje koniguraci VPN propojující více lokalit
	- Místo fyzického rozhraní lze konfigurovat VTI rozhraní daného tunelu
- Umožňuje odesílání a příem unicast a multicast provozu
	- Díky tomu je zajištěna podpora směrovacích protokolů bez nutnosti konfigurovat GRE
- Podporuje topologii Point-to-Point nebo Hub-and-Spoke
	- Tunel lze zřizovat přímo mezi lokalitami nebo skrze centrální router

##### VPN poskytovatelů v využitím MPLS
- Poskytovatelé WAN připojení často implementují MPLS, což umožňuje oddělit provoz mnoha zákazníků na společné infrastruktuře
- Lze jej nasadit dvěma základními způsoby:
	- Layer 3 MPLS VPN
		- Poskytovatel sezákazníkem spolupracuje na směrování jeho provozu
	- Layer 2 MPLS VPN
		- Poskytovatel se nepodílí na směrování zákazníckého provozu, vznikne tak virtuální Ethernet segment skrze WAN infrastrukturu
		- Služba se nazývá Virtual Private LAN Service (VPLS)
#### 3) IPsec – Charakteristika

##### Technologie IPsec
- Standard IETF umožňující zabezpečenou komunikaci
	- Na L3 nabízí mechanismy autentizace a /nebo šifrování dat
- Provádí vzájemnou autentizaci komunikujících hostitelů
	- Zajišťuje protokol Internet Key Exchange (IKE) verze 1 či 2
	- IKE využívá protokolů ISAKMP a Oakley
- Užívá šifrovacích algoritmů pro zajištění důvěrnosti dat
	- Protokol Diffie-Hellman pro bezpečné sdílení šifrovacích klíčů
- Užívá hashovacích algoritmů pro zajištění integrity dat
	- Ověřuje, zda-li nedošo ke změně obsahu paketů během přenosu

##### Způsob výběru algoritmů IPsec
- IPsec není vázán na konkrétní šifrovací či hashovací algoritmus
	- Záleží tedy na dohodě komunikujících hostitelů
- Volné sloty jsou zaplněny volbami komunikujících stran a vytváří Security Association (SA)

##### Základní protokoly IPsec
- Authentication Header (AH)
	- Integrita paketu a autentizace jeho odesílatele
	- Umožňuje čelit replay útokům, data jsou přenášena otevřeně
- Encapsulating Security Payload (ESP)
	- Integrita paketu a důvěrnost dat pomocí autentizace a šifrování
	- Může být kombinováno s AH (využívá se zřídka, protože AH neumí NAT)

##### Zajištění utajení dat (Condifentiality)
- Míra utajení závisí na síle šifrovacího algoritmu a délce klíče
	- Čím delší klíč, tím je výpočetně náročnější útočit hrubou silou

##### Symetrické šifrovací algoritmy pro IPsec
- Data Encryption Standard (DES)
	- Zastaralý, klíč o délce 56 bitů
- Triple DES (3DES)
	- 3 samostatné DES klíče o délce 56 bitů
	- Silnější než klasický DES, výpočetně náročnější
- Advanced Encryption Standard (AES)
	- Délky klíčů 128, 192 až 256 bitů
- Software-Optimized Encryption Algorithm (SEAL)
	- Proudová šifra, klíč o délce 160 bitů

##### Zajištění integrity dat v IPsec
- Data mohou být během přenosu veřejnou sítí pozměněna
	- Je třeba použít mechanismus, který po přijetí ověří neporušenost dat
- Využívá se hashovacích algoritmů v kombinaci s autentizací
	- Samostatná hashovací funkce nestačí, neboť ji zná i útočník
- Typy zajištění integrity v IPsec:
	- Hashed Message Authentication Code (HMAC-X={MD5 | SHA})
		- hashování pomocí MD5 či SHA, obě strany sdílí ověřovací klíč
		- Message Digest 5 (MD5)
			- Délka hashe 128 bitů
			- Zastaralé, objeveny vážné slabiny
		- Secure Hash Algorithm (SHA)
			- SHA-1
				- Délka hashe 160 bitů, zastaralé
			- SHA-256
				- Délka hashe 256 bitů

##### Metody autentizace v IPsec
- Pre-shared Key (PSK)
	- Sdílené heslo, snadné na konfiguraci
	- Musí být stejné na každém hostiteli
	- Nepřísiš škálovatelný způsob
- Rivest, Shamir, Adleman (RSA)
	- Autentizace na bázi certifikátů
	- Využívá Public Key Infrastructure
	- Komunikující účastníci musí důvěřovat společné certifikační autoritě

##### Bezpečné ustavení klíče s Diffie-Hellman (DH)
- Umožňuje účastníkům bezpečné sdílení klíče, funguje i přes veřejný kanál
- DH groups 1, 2, 5
	- Zastaralé, nepoužívat
- DH Groups 14, 15, 16
	- Klíče 2048, 3072 a 4096 bitů
- DH Groups 19, 20, 21, 24
	- Nabízí Elliptical Curve Cryptography (ECC)

##### Režimy IPsec
- Transportní režim
- Tunelový režim (liší se dalším zapouzdřením)