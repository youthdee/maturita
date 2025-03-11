#### 1) Princip hierarchického návrhu sítě a jeho vlastnosti

##### Potřeba škálovatelnosti sítí
- Zaměstnanci potřebují přistupovat k datům mnoha způsoby, kdykoliv, kdekoliv a na libovolném zařízení
- Potřeba bezpečných , spolehlivých a vysoce dostupných sítí, které musí vyhovovat nejen stávajícím, ale i boduoucím požadavkům
- Podnikání organizace se v čase mění, roste počet zaměstnanců a přibývá počet poboček
- Návrh sítě musí být proveden tak, aby síť rostla s organizací
- Síť je škálovatelná vzhledek k měnícím se požadavkům
- Hlavní funkce škálovatelného návrhu sítě:
	- Přidání rozšiřitelných, modulárních síťových prvků (možnost přidání modulu předchází nutnosti upgradu celého zařízení)
	- Nasazení hierarchického, modulárního návrhu sítě (umožňuje rozšíření přidáním nových zařízení bez vlivu na stávající síť)
	- Návrh hierarchického IPv4/IPv6 adresního schématu (pečlivé plánování adresaci v síti předchází nutnosti provádění změn)
	- Segmentace sítě, nasazení IP směrování a firewallu (omezuje šíření broadcastů v síti, na routerech filtrace provozu)
##### Přepínané sítě bez hranic
- Cisco Borderless Network:
	- Síťová architektura, která se přizpůsobí požadavkům
- Sjednocuje pevné (wired) a bezdrátové sítě
- Využívá hierarchické stavby, je škálovatelná a odolná
- Borderless sítě jsou hierarchické, modulární, flexibilní a odolné
- Jejich implemetnace nabízí vlastnosti moderních sítí (škálovatelnost, bezpečnost a spravovatelnost)
- Implementují vrstevný přístup k síťovému návrhu:
	- Access
	- Disribution
	- Core
- Dva základní modely:
	- Třívstvý
	- Douvrstvý
- Volba modelu záleží podle finančních možností a potřeb dané organizace
- Dříve jednoduché L2 sítě (hubs, repeaters, bridges)
- Dnes přepínané, segmentované sítě (switches, routers, APs)

##### Funkce vrstev
- Access:
	- Poskytuje síťový přístup koncovým uživatelům a zařízením
	- Switche (přepínače) této vrstvy jsou propojeny se switchi (přepínači) vrstvy následující
- Distribution:
	- Implementuje směrování, QoS a zabezpečení
	- Sdružuje rozsáhlé síťové rozvody, omezuje L2 broadcastové domény
- Core:
	- Zajišťuje vysokorychlostní, páteřní síťové propojení
	- Zprostředkuje připojení do sítí WAN a Internetu

##### Třívrstvá síť
- Vrstvy Distribution a Core existují oddělelně
- Topologie je rozšířená hvězda (Extended Star)

##### Dvouvrstvá síť
- Vrstvy Distribution a Core jsou sdruženy
- Výhodné řešení v menších, lokalizovaných sítích
- Označováno jako "Collapsed Network Design"

#### 2) Správa VLAN na Cisco switchích

##### Druhy VLAN
- Výchozí (default)
	- Na cisco switchích vždy VLAN 1
	- Nelze ji smazat ani přejmenovat
	- Iniciálně přiřazena všem portům
- Datová (data)
	- Také jako uživatelská VLAN
	- Pro potřeby datových přenosů
- Nativní (native)
	- Rámce této VLAN nejsou na portech v režimu trunk tagovány
	- Doporučeno vyčlenit oddělenou VLAN
- Pro správu (management)
	- Umožňují vzdálenou správu síťových prvků
- Hlasová (voice)
	- Pro připojení IP telefonů
	- Na portu se kombinují s příslušnou datovou VLAN

##### VLAN Trunky
- Umožňují přenos rámců různých VLAN na fyzickém spoji, mohou vzájemně propojit switche (přepínače), směrovače (routery) a servery
- Přenáší tagované rámce dle standardu IEEE 802.1q
	- Uvnitř tagu je uvedeno VLAN ID, do kterého rámec patří
- Hostitelé na různých přepínačích (switchích) mohou být na stejné VLAN
	- Provoz mezi VLANy je vzájemně izolován
- K propojení různých VLAN je třeba směrovač (router)
	- Každá VLAN pak představuje samostatný IP subnet

##### Nativní VLAN a 802.1Q tagování
- Standard 802.1Q definuje nativní VLAN pro trunky, jako výchozí se použije VLAN 1
- Netagované rámce na trunku jsou přiřazeny k nativní VLAN
	- Lze tak na trunk připojit i obyčejné hostitele
- Příkladem netagovaného provozu jsou management rámce, např. mezi dvěma switchi (přepínači)
- Tagovaný rámec s nativním VLAN ID přepínač odmítne, protože rámce nativní VLAN jsou odesílány a přijímány jako netagované

##### Rozsahy VLAN na switchích (přepínačích) Catalyst
- Běžný rozsah VLAN ID od 1 do 1005:
	- Pro malé a střední podniky
	- ID 1 a 1002 až 1005 jsou předvytvořeny a nedají se smazat či upravit
	- Uloženy ve flash paměti
	- VTP synchronizuje databázi VLAN, výměna VLAN mezi přepínači
- Rozšířený rozsah VLAN ID od 1006 až 4094
	- Pro providery a velké podniky
	- Uloženy v provozní konfiguraci
	- Je potřebný transparentní režim VTP
	- Méně funkcí než u běžných VLAN

##### Správa VLAN
- Vytvoření VLAN:
	- Příkaz "vlan {id}" v konfiguračním režimu
	- Příkaz "name {name}" v konfiguračním režimu VLAN
- Přiřazení portu do VLAN (Konfigurační režim rozhraní):
	- Access:
		- Příkaz "switchport mode access" pro explicitní nastavení režimu access 
		- Příkaz "switchport access vlan {id}" pro přiřazení daného portu do VLAN se zadaným ID 
		- Příkaz "mls qos trust cos" pro konfiguraci hlasové VLAN, což umožňuje prioritizovat hlasový provoz v síti
		- Příkaz "switchport voice vlan {id}" pro přiřazení hlasové VLAN portu
	- Trunk:
		- Příkaz "switch port mode trunk" pro explicitní nastavení režimu trunk
		- Příkaz "switchport trunk native vlan {native_vlan_id}" pro nastavení nativní VLAN
		- Příkaz "switchport trunk allowed vlan {vlans}" pro nastavení povolených VLAN
- Ověření konfigurace:
	- Příkaz "show vlan summary" pro zobrazení celkového počtu různých kategorií VLANů
	- Příkaz "show interfaces {port} switchport" pro zobrazení přiřazené VLANy k portu
	- Příkaz "show vlan brief" pro vypsání jednotlivých VLANů a příslušných přístupových portů k nim (porty v režimu trunk nevypisuje)
- Změna přiřazení portu do VLAN:
	- Příkaz "no switchport {access | trunk} vlan" pro odebrání dříve přiřazené VLAN v konfuguračním režimu rozhraní
- Smazání VLAN:
	- Příkaz "no vlan {id}" pro odstranění VLAN se zadaným Id (přiřazený port poté přestane fungovat)

#### 3) Protokol DTP a jeho dopady na bezpečnost sítě
TODO
#### 4) Layer 3 Switching – vlastnosti a způsoby nasazení
TODO