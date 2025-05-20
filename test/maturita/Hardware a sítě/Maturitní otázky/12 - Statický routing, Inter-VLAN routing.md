#### 1) Princip Routingu
##### Princip Routingu
1) **Směrování (routing):**  
	- Rozhodování kam dál poslat paket na základě cílové IP adresy.
2) **Routovací tabulky:**  
	- Každý router má tabulku, ve které jsou záznamy o tom, kam se má paket s určitým cílem odeslat.
3) **Statický vs. dynamický routing:**
    - **Statický**: Správce ručně nastaví trasy.
    - **Dynamický**: Routery si mezi sebou vyměňují informace a samy určují trasy (pomocí protokolů jako RIP, OSPF, BGP).
4) **Skoky (hops):**  
    - Data často musí projít několika routery = více skoků.
5) **Metoda výběru trasy:**  
    - Na základě metrik jako počet skoků, rychlost linky, zátěž, spolehlivost atd.
##### Druhy cílů IP paketu
1) **Hostitel sám sobě**:
	- Odesílatel je zároveň adresátem paketu
2) **Místní hostitel**:
	- Adresát je ve stejné síti jako odesílatel
3) **Vzdálený hostitel**:
	- Adresát je v jiné síti než odesílatel
##### Výchozí brána
1) Síťový uzel **schopný směrování paketů** (Router, L3 Swtich)
2) Předává pakety určené **uzlům jiných sítí**, u malých sítí rovnou do Internetu
3) Každý uzel místní sítě musí mít **nastavenou výchozí bránu**, staticky nebo pomocí služby DHCP
#### 2) Routovací tabulka
##### Charakteristika Směrovací Tabulky
- Obsahuje pravidla potřebná pro **směrování**, bez; nich nelze komunikovat s uzly jiných sítí
- Pravidla vyjadřují směr dalšího doručování:
	1) **Cílová adresa** a **maska** jako selektor pravidla
	2) **Adresa brány** a **rozhraní** pro předání paketu
	3) **Metrika pro vyjádření priority** pravidla
- Pravidlo `0.0.0.0/0` představuje výchozí bránu pro pakety, pro něž není specifičtější pravidlo
##### Druhy směrovacích pravidel
1) **Místní směry** (Directly-Connected Routes):
	- Odvozeny z aktivních rozhraních routeru (směrovače)
	- Do směrovací tabulky přidány automaticky
2) **Vzdálené směry** (Remote Routes)
	- Mohou být přidány manuálně
	- Je také možná automatická výměna mezi směrovači
3) **Výchozí směr** (Default Route):
	- Routery mohou použít výchozí bránu
#### 3) Charakteristika, konfigurace a možnosti použití statického routingu
##### Charakteristika statického směrování
1) **Ruční nastavení**:
	- Správce sítě ručně definuje cesty k cílovým sítím
2) **Jednoduchost**:
	- Nevyžaduje nasazení žádných směrovacích protokolů
3) **Nízká zátěž procesoru a paměti**:
	- Router neprovádí výpočty jako u dynamického směrování
4) **Vhodné pro malé sítě**:
	- Efektivní u minimálně měnících se topologiích
5) **Nevhodné pro rozsáhlé a dynamické sítě**: 
	- Každá změna sítě vyžaduje ruční úpravy
##### Konfigurace statického směrování
- `show ip route` pro vypsání aktuální směrovací tabulky
- `ip route {cílová síť} {maska sítě} {next-hop IP | výstupní rozhraní}` pro konfiguraci směrovacího pravidla
- `show running config | include ip route` a `show ip route static` pro ověření konfigurace
##### Možnosti použití statického směrování
1) **Malé sítě a SOHO prostředí**:
	- Jednoduchá správa bez nutnosti dynamických protokolů
2) **Zabezpečené a kritické cesty**:
	- Mezi firewally, kde je důležitá kontrola směrování
3) **Záložní trasy**:
	- V kombinaci s dynamickým směrováním jako failover
4) **Point-to-Point spoje**:
	- Nemá smysl využívat dynamického směrování mezi dvěma spoji
#### 4) Inter-VLAN routing, varianty Inter-VLAN routingu
##### Charakteristika Inter-VLAN Routingu
- Uzel v jedné `VLAN` **nemůže přímo komunikovat** s jinou `VLAN`, jedná se o **navzájem izolované místní sítě** operující na spojové vrstvě
- V Případě `IPv4` a `IPv6` lze nasadit **směrování** mezi `VLAN`y
- Existují tři základní scénáře `Inter-VLAN routingu`:
	1) **Legacy**:
		- Router pracuje klasicky a neví nic o `VLAN` infrastruktuře
	2) **Router-on-a-Stick**:
		- Na Router vede `VLAN trunk`, užívá se podrozhraní
	3) **L3 Switching**:
		- Směrování mezi `VLAN`y konfigurováno na `L3` switchi na `SVI` rozhraní
##### Legacy
1) **Výhody**:
	- Jednoduché nasazení
	- Dedikovaný fyzický spoj pro provoz každé `VLAN`
	- Router nemusí podporovat tagovaný provoz
2) **Nevýhody**:
	- Počet fyzických portů routeru a switche musí odpovídat počtu `VLAN`
	- Špatná škálovatelnost v případě rozvoje síťové infrastruktury
##### Router-on-a-Stick
1) **Výhody**:
	- Stačí jeden fyzický spoj pro všechny zúčastněné `VLAN`y
	- Dobrá škálovatelnost v případě rozvoje síťové infrastruktury
2) **Nevýhody**:
	- Jediný fyzický spoj předává rámce všech `VLAN` tam i zpět
	- Selhání fyzického spoje znamená úplnou ztrátu komunikace mezi `VLAN`y
##### L3 Switching
1) **Výhody**:
	- Optimální směrovací výkon
	- Není třeba samostatného routeru
	- Dobrá škálovatelnost v případě rozvoje síťové infrastruktury
2) **Nevýhody**:
	- Selhání `L3` switche znamená úplnou ztrátu komunikace mezi `VLAN`y
	- Vyšší pořizovací náklady