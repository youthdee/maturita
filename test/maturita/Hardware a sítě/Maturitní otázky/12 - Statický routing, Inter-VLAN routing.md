#### 1) Princip Routingu

##### Druhy cílů IP paketu
- Hostitel sám sobě
	- Odesílatel je zároveň adresátem paketu
- Místní hostitel
	- Adresát je ve stejné síti jako odesílatel
- Vzdálený hostitel
	- Adresát je v jiné síti než odesílatel

##### Výchozí brána
- Síťový uzel schopný směrování paketů (Router, L3 Swtich)
- Předává pakety určené uzlům jiných sítí, u malých sítí rovnou do Internetu
- Každý uzel místní sítě musí mít nastavenou výchozí bránu, staticky nebo pomocí služby DHCP, jinak bude tento síťový uzel schopen pracovat pouze v místní síti
#### 2) Routovací tabulka

##### Charakteristika Směrovací Tabulky
- Obsahuje pravidla potřebná pro směrování, bez nich nelze komunikovat s uzly jiných sítí
- Pravidla vyjadřují směr dalšího doručování
	- Cílová adresa a maska jako selektor pravidla
	- Adresa brány a rozhraní pro předání paketu
	- Metrika pro vyjádření priority pravidla
- Pravidlo 0.0.0.0/0 představuje výchozí bránu pro pakety, pro něž není specifičtější pravidlo

##### Druhy směrovacích pravidel
- Místní směry (Directly-Connected Routes):
	- Odvozeny z aktivních rozhraních routeru (směrovače)
	- Do směrovací tabulky přidány automaticky
- Vzdálené směry (Remote Routes)
	- Mohou být přidány manuálně
	- Je také možná automatická výměna mezi směrovači
- Výchozí směr (Routery mohou použít výchozí bránu)

#### 3) Charakteristika, konfigurace a možnosti použití statického routingu
##### Charakteristika statického směrování
- Ruční nastavení (správce sítě ručně definuje cesty k cílovým sítím)
- Jednoduchost (nevyžaduje nasazení žádných směrovacích protokolů)
- Nízká zátěž procesoru a paměti (Router neprovádí výpočty jako u dynamického směrování)
- Vhodné pro malé sítě (efektivní u minimálně měnících se topologiích)
- Nevhodné pro rozsáhlé a dynamické sítě (každá změna sítě vyžaduje ruční úpravy)
##### Konfigurace statického směrování
- Příkaz "show ip route" pro vypsání aktuální směrovací tabulky
- Příkaz "ip route {cílová síť} {maska sítě} {next-hop IP | výstupní rozhraní}"
- Příkaz "show running config | include ip route" a "show ip route static" pro ověření konfigurace

##### Možnosti použití statického směrování
- Malé sítě a SOHO prostředí
	- Jednoduchá správa bez nutnosti dynamických protokolů
- Zabezpečené a kritické cesty
	- Mezi firewally, kde je důležitá kontrola směrování
- Záložní trasy
	- V kombinaci s dynamickým směrováním jako failover
- Point-to-Point spoje
	- Nemá smysl využívat dynamického směrování mezi dvěma spoji
#### 4) Inter-VLAN routing, varianty Inter-VLAN routingu

##### Charakteristika Inter-VLAN Routingu
- Uzel v jedné VLAN nemůže přímo komunikovat s jinou VLAN, jedná se o navzájem izolované místní sítě operující na spojové vrstvě
- V Případě IPv4 a IPv6 lze nasadit směrování mezi VLANy
- Existují tři základní scénáře Inter-VLAN routingu:
	- Legacy (Router pracuje klasicky a neví nic o VLAN infrastruktuře)
	- Router-on-a-Stick (Na Router vede VLAN trunk, užívá se podrozhraní)
	- L3 switching (Směrováí mezi VLANy konfigurováno na L3 switchi na SVI rozhraní)

##### Legacy Inter-VLAN Routing
- Výhody:
	- Jednoduché nasazení
	- Dedikovaný fyzický spoj pro provoz každé VLAN
	- Router nemusí podporovat tagovaný provoz
- Nevýhody:
	- Počet fyzických portů routeru a switche musí odpovídat počtu VLAN
	- Špatná škálovatelnost v případě rozvoje síťové infrastruktury

##### Router-on-a-Stick Inter-VLAN Routing
- Výhody:
	- Stačí jeden fyzický spoj pro všechny zúčastněné VLANy
	- Dobrá škálovatelnost v případě rozvoje síťové infrastruktury
- Nevýhody:
	- Jediný fyzický spoj předává rámce všech VLAN tam i zpět
	- Selhání fyzického spoje znamená úplnou ztrátu komunikace mezi VLANy

##### Inter VLAN Routing na Layer 3 Switchi
- Výhody:
	- Optimální směrovací výkon
	- Není třeba samostatného routeru
	- Dobrá škálovatelnost v případě rozvoje síťové infrastruktury
- Nevýhody:
	- Selhání L3 switche znamená úplnou ztrátu komunikace mezi VLANy
	- Vyšší pořizovací náklady
	
