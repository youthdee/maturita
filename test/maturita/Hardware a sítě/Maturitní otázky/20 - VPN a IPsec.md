#### 1) Účel a výhody použití VPN
##### Vlastnosti sítí VPN
- Poskytují zpravidla zabezpečená `end-to-end` spojení
- Jsou virtuální proto, že umožňují **přenos chráněných dat skrze veřejné sítě** (Internet)
- Zabezpečení dat je řešeno **šifrováním**
##### Výhody sítí VPN
1) **Úspora nákladů**:
	- Nasazení `VPN` umožnil rozvoj vysokorychlostního připojení k Internetu
2) **Bezpečnost**:
	- S použitím moderních šifrovacích standardů poskytují vysokou úroveň zabezpečení datových přenosů
3) **Škálovatelnost**:
	- Skrze Internet lze snadno propojovat nové lokality
4) **Kompatibilita**:
	- `VPN` lze implementovat pomocí mnoha různých přenosových standardů
#### 2)Typy VPN
##### VPN typu Site-to-Site
- Poskytují **transparentní způsob propojení** sítí `LAN`
- Koncové uzly mohou vzájemně komunikovat **nešifrovaně**:
	- Koncová zařízení o `VPN` vůbec nemusí vědět
- **Zapouzdření** a **šifrování provozu** se provádí na `VPN` **bránách** (Gateways)
	- Odesílající brána (Gateway) paket zašifruje adoplní o potřebná záhlaví
	- Přijímající brána paket zbaví přidaných záhlaví a dešifruje jej
- `IPsec VPN`, `GRE over IPsec`, `DMVPN`
##### VPN typu Remote Access
- Umožňují **zabezpečené připojení k firemní síti**
1) Clientless:
	- `SSL` pomocí webového prohlížeče
2) Client-Based:
	- `IPsec VPN` připojení pomocí klienta
##### VPN s využitím SSL/TLS
- Využívají infrastrukturu **veřejného klíče** (PKI) a **certifikáty**, pomocí nich probíhá **autentizace účastníků**
1) **Omezená podpora aplikací**:
	- Pouze webové aplikace a sdílení souborů
2) **Průměrná odolnost autentizace**:
	- Jednocestná či dvoucestná autentizace
3) **Střední či vysoká odolnost šifrování**:
	- Délky klíčů `40-256 bitů`
4) **Nízká složitost připojení**:
	- Vyžaduje pouze webový prohlížeč
5) **Široké možnosti připojení**:
	- Lze připojit jakékoliv zařízení s webovým prohlížečem
##### VPN s využitím IPsec
- **Široká podpora aplikací**:
	- Všechny aplikace užívající `IP`
- **Vysoká odolnost autentizace**:
	- Dvoucestná autentizace se sdíleným klíčem či certifikáty
- **Vysoká odolnost šifrování**:
	- Délky klíčů `56 - 256 bitů`
- **Střední složitost připojení**:
	- Vyžaduje nainstalovanou aplikaci `VPN` klienta
- **Omezené možnosti připojení**:
	- Pouze pro specifická zařízení se specifickou konfigurací
##### Podnikové VPN
- Zřizovány prostřednictvím Internetu
##### VPN poskytovatelů služeb
- Umožňují oddělit provoz různých klientů
##### GRE over IPsec (Generic Routing Encapsulation)
1) **Nezabezpečený** `Site-To-Site` `VPN` **tunelovací protokol**:
	- Samotný nepodporuje autentizaci ani šifrování
2) **Umožňuje zapouzdření různých protokolů**:
	- Včetně `multicast` a `broadcast` provozu
3) **Pro zabezpečení komunikace lze zapouzdřit pomocí** `IPsec`
	- Standardní `IPsec` `VPN` podporuje pouze `unicastový` provoz
	- Umožňuje zabezpečit `multicastovou` komunikaci (např. pro potřeby komunikace dynamických směrovacích protokolů)
4) **Princip zapouzdření**:
	- `Passanger protocol` (přenášený protokol)
		- Je Protokolem datového paketu určeného k zapouzdření pomocí `GRE`
	- `Carrier protocol` (přepravní protokol)
		- Je přepravním protokolem zapouzdřujícím datový paket
	- `Transport protocol` (transportní či přenosový protokol)
		- Protokol, který zajišťuje vlastní přenos zapouzdřeného paketu (např. `IP`)
##### Dynamic Multipoint VPN (DMVPN)
1) **Nabízí flexibilní způsob propojení centrály a poboček**:
	- Zjednodušuje konfiguraci `VPN` umožňuje vznik virtuálních spojů
2) **Základní infrastruktura používá topologii** `Hub-and-Spoke`:
	- Pobočkové brány mají konfiguraci `VPN` spojení s centrálou
3) **Virtuální pobočkové spoje odpovídají topologii** `Full Mesh`:
	- Centrála zprostředkuje konektivitu mezi pobočkovými branami
##### IPsec Virual Tunnel Interface (VTI)
1) **Zjednodušuje konfiguraci** `VPN` **propojující více lokalit**:
	- Místo fyzického rozhraní lze konfigurovat `VTI` rozhraní daného tunelu
2) **Umožňuje odesílání a příjem** `unicast` **a** `multicast` **provozu**:
	- Díky tomu je zajištěna podpora směrovacích protokolů bez nutnosti konfigurovat `GRE`
3) **Podporuje topologii** `Point-to-Point` **nebo** `Hub-and-Spoke`:
	- Tunel lze zřizovat přímo mezi lokalitami nebo skrze centrální router
##### VPN poskytovatelů v využitím MPLS
- Poskytovatelé `WAN` připojení často implementují `MPLS`, což umožňuje oddělit provoz mnoha zákazníků na společné infrastruktuře
- Lze jej nasadit dvěma základními způsoby:
	1) `Layer 3 MPLS VPN`
		- Poskytovatel se zákazníkem spolupracuje na směrování jeho provozu
	2) `Layer 2 MPLS VPN`
		- Poskytovatel se nepodílí na směrování zákaznického provozu, vznikne tak virtuální Ethernet segment skrze WAN infrastrukturu
		- Služba se nazývá Virtual Private LAN Service (`VPLS`)
#### 3) IPsec – Charakteristika
##### Technologie IPsec
1) **Standard** `IETF` **umožňující zabezpečenou komunikaci**:
	- Na `L3` nabízí mechanismy autentizace a /nebo šifrování dat
2) **Provádí vzájemnou autentizaci komunikujících hostitelů**:
	- Zajišťuje protokol Internet Key Exchange (`IKE`) verze 1 či 2
	- `IKE` využívá protokolů `ISAKMP` a `Oakley`
3) **Užívá šifrovacích algoritmů pro zajištění důvěrnosti dat**:
	- Protokol `Diffie-Hellman` pro bezpečné sdílení šifrovacích klíčů
4) **Užívá hashovacích algoritmů pro zajištění integrity dat**:
	- Ověřuje, zda-li nedošlo ke změně obsahu paketů během přenosu
##### Způsob výběru algoritmů IPsec
1) `IPsec` **není vázán na konkrétní šifrovací či hashovací algoritmus**
	- Záleží tedy na dohodě komunikujících hostitelů
2) Volné sloty jsou zaplněny volbami komunikujících stran a vytváří **Security Association** (`SA`)
##### Základní protokoly IPsec
1) **Authentication Header** (`AH`)
	- Integrita paketu a autentizace jeho odesílatele
	- Umožňuje čelit replay útokům, data jsou přenášena otevřeně
2) **Encapsulating Security Payload** (`ESP`)
	- Integrita paketu a důvěrnost dat pomocí autentizace a šifrování
	- Může být kombinováno s `AH` (využívá se zřídka, protože `AH` neumí `NAT`)
##### Zajištění utajení dat (Condifentiality)
- **Míra utajení závisí na síle šifrovacího algoritmu a délce klíče**:
	- Čím delší klíč, tím je výpočetně náročnější útočit hrubou silou
##### Symetrické šifrovací algoritmy pro IPsec
1) **Data Encryption Standard** (`DES`)
	- Zastaralý, klíč o délce `56 bitů`
2) **Triple DES** (`3DES`)
	- 3 samostatné `DES` klíče o délce `56 bitů`
	- Silnější než klasický `DES`, výpočetně náročnější
3) **Advanced Encryption Standard** (`AES`)
	- Délky klíčů `128, 192 - 256 bitů`
4) **Software-Optimized Encryption Algorithm** (`SEAL`)
	- Proudová šifra, klíč o délce `160 bitů`
##### Zajištění integrity dat v IPsec
1) **Využívá se hashovacích algoritmů v kombinaci s autentizací**
	- Samostatná hashovací funkce nestačí, neboť ji zná i útočník
2) **Typy zajištění integrity v IPsec**:
	- Hashed Message Authentication Code (HMAC-X={MD5 | SHA})
		- Hashování pomocí MD5 či SHA, obě strany sdílí ověřovací klíč
		- `MD5`, `SHA-1` a `SHA-256`
##### Metody autentizace v IPsec
1) **Pre-shared Key** (`PSK`)
	- Sdílené heslo, snadné na konfiguraci
	- Musí být stejné na každém hostiteli
	- Nepřísiš škálovatelný způsob
2) **Rivest, Shamir, Adleman** (`RSA`)
	- Autentizace na bázi certifikátů
	- Využívá Public Key Infrastructure
	- Komunikující účastníci musí důvěřovat společné certifikační autoritě
##### Bezpečné ustavení klíče s Diffie-Hellman (DH)
- **Umožňuje účastníkům bezpečné sdílení klíče, funguje i přes veřejný kanál**
	1) **DH groups 1, 2, 5**:
		- Zastaralé, nepoužívat
	2) **DH Groups 14, 15, 16**:
		- Klíče 2048, 3072 a 4096 bitů
	3) **DH Groups 19, 20, 21, 24**:
		- Nabízí Elliptical Curve Cryptography (ECC)
##### Režimy IPsec
1) Transportní režim
2) Tunelový režim