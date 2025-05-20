#### 1) Switch – princip činnosti
##### Princip činnosti switche
1) Po zapnutí je MAC tabulka **prázdná**, switch určitou dobu pracuje jako **hub**
2) Záznamy tabulky se tvoří **dle přijatých rámců**, uloží se `MAC` **adresa** odesílatele a **číslo portu**
3) Rámce se následně rozesílají dle `MAC` **tabulky**, podle **cílové** `MAC` **adresy** se vyhledá **číslo portu**
4) Záznamy tabulky po určité době **expirují**, při odpojení portu se položky tabulky vymažou
##### Tabulka MAC adres switche 
1) Uložena v paměti `CAM` (**Content Addresable Memory**)
	- Která slouží pro vyhledávání záznamů vysokou rychlostí
2) Přepínač za běhu zjišťuje, jaké zařízení jsou portům přiřazena, postupně obsah tabulky vytváří
3) Switch užívá `MAC` tabulku pro **efektivní zpracování rámců**, kde určuje **správný výstupní port** dle cílových `MAC` adres
##### Proces zpracování rámce
1) **Learning**:
	1) Switch (přepínač) uloží zdrojovou `MAC` adresu rámce do tabulky `MAC` adres
	2) V případě, že záznam již existuje, aktualizuje se jeho doba platnosti
	3) Když byla `MAC` adresa přiřazena k jinému portu, vytvoří nový záznam
2) **Forwarding**:
	1) V případě unicast adresy switch (přepínač) v tabulce `MAC` adres vyhledá pro danou cílovou `MAC` adresu výstupní port
	2) V případě `multicast`/`broadcast` adresy je rámec rozeslán na všechny aktivní porty kromě portu vstupního
#### 2) Přepínání rámců na switchi, popis, metody
##### Přepínání rámců
- **Klíčový koncept** v oblasti sítí a telekomunikací
- **Různé druhy** switchů pro různé sítě:
	- `LAN`, `WAN`, `PSTN` (Public Service Telephone Network)
- Rozlišení portů podle jejich aktuální úlohy:
	1) Vstupní (`ingress`) port:
		- Místo, kde rámce vstupuje do zařízení
	2) Výstupní (`egress`) port:
		- Místo, kudy rámec opouští zařízení
- Přepínání probíhá na základě **vyhodnocení záhlaví rámce**
	- Podle cílové adresy je možné dohledat výstupní port
##### Metoda Store-and-Forward
1) Nejprve příjme **celý rámec**, **ověří délku** a **kontrolní součet**
2) **Zaznamená** číslo portu odesílatele pokud v tabulce MAC adres příslušný záznam není
3) **Odešle rámec na příslušný port** pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (**flood**)
4) Úplné přijetí rámce před odesláním (**vyšší zpoždění**), umožňuje **vyloučit vadné rámce**
##### Metoda Cut-through
1) **Přijme alespoň cílovou MAC adresu** rámce, zahájí jeho zpracování, příjem rámce pokračuje
2) **Zahájí odeslání rámce na port** pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
3) **Zaznamená číslo portu odesílatele**, nejdříve však po přijetí zdrojové MAC adresy rámce a pokud v tabulce MAC adres příslušný záznam není
- **Varianty** Metody Cut-Trough:
	1) **Fast-forward**
		- Zahájí odesílání rámce ihned po přijetí cílové MAC
		- Nejmenší přenosové zpoždění
		- Typická varianta
	2) **Fragment-free**
		- Zahájí odesílání rámce po přijetí 64 oktetů
		- Nejvíce kolizí nastává právě v této části rámce
		- Kompromis mezi mírou integrity a zpoždění
- Rámec odesílán **ihned po přijetí záhlaví** (**menší zpoždění**), **vadné rámce se tak předávají dále** po síti
#### 3) Virtuální sítě (VLAN) na switchích, - vlastnosti a realizace
##### VLAN - Charakteristika
1) **Segmentace sítě** na existujících fyzických spojích, **organizace sítě** do **menších segmentů** zjednodušuje správu sítě
2) **Organizační flexibilita** v přepínané síti, hostitelé mohou být ve stejné místní síti napříč různými switchi (přepínači)
3) Zařízení ve stejné `VLAN` si mohou zasílat `Ethernet` rámce:
	- Zpravidla mají IP adresy společné `IP` sítě)
4) Pracují na základě logických spojení, nikoliv fyzických, na jednom fyzickém spoji lze předávat rámce různých `VLAN`
##### Příklad nasazení VLAN
1) Počítače různých oddělení ve stejné místní síti
2) Segmentace sítě podle funkce, týmu nebo aplikace
3) Sdílení fyzické infrastruktury s ostatními `VLAN`y
4) Rámce jsou předávány pouze zařízením ve stejné `VLAN`
5) Komunikace mimo `VLAN` vyžaduje směrování
##### Výhody řešení s VLAN
1) **Úspora nákladů** na vybudování síťové infrastruktury, pro `VLAN`y není třeba vytvářet samostatné fyzické spoje
2) Snadné rozdělení sítě na **menší segmenty**, účinné omezení velikosti **broadcastových domén**
3) **Přístupové politiky** lze nastavit podle skupin uživatelů, řízení přístupu pomocí ACL pravidel na routerech
4) **Škálovatelnost síťové infrastruktury**, pro vytvoření nové `VLAN` není třeba pořizovat nové síťové prvky
##### Druhy VLAN
1) **Výchozí** (`default`):
	- Na Cisco switchích vždy VLAN 1
	- Nelze ji smazat ani přejmenovat
	- Iniciálně přiřazena všem portům
2) **Datová** (`data`)
	- Také jako uživatelská VLAN
	- Pro potřeby datových přenosů
3) **Nativní** (`native`)
	- Rámce této VLAN nejsou na portech v režimu trunk tagovány
	- Doporučeno vyčlenit oddělenou VLAN
4) **Pro správu** (`management`)
	- Umožňují vzdálenou správu síťových prvků
5) **Hlasová** (`voice`)
	- Pro připojení IP telefonů
	- Na portu se kombinují s příslušnou datovou VLAN
##### VLAN Trunky
1) Umožňují **přenos rámců různých** `VLAN` na fyzickém spoji, mohou vzájemně **propojit switche** , směrovače (routery) a servery
2) Přenáší **tagované** rámce dle standardu `IEEE 802.1q`
	- Uvnitř tagu je uvedeno `VLAN ID`, do kterého rámec patří
3) Hostitelé na **různých přepínačích** (switchích) mohou být na **stejné** `VLAN`
	- Provoz mezi `VLAN`y je vzájemně izolován
4) K propojení různých VLAN je třeba **směrovač**
	- Každá `VLAN` pak představuje samostatný `IP subnet`
##### Nativní VLAN a 802.1Q tagování
1) Standard `802.1Q` definuje nativní VLAN pro trunky, jako výchozí se použije VLAN 1
2) **Netagované rámce** na trunku jsou přiřazeny k **nativní** `VLAN`
	- Lze tak na trunk připojit i obyčejné hostitele
3) Příkladem **netagovaného provozu** jsou **management rámce**
4) **Tagovaný rámec** s nativním `VLAN ID` přepínač **odmítne**
##### Rozsahy VLAN na switchích (přepínačích) Catalyst
1) **Běžný rozsah** `VLAN ID` **od 1 do 1005**:
	- Pro malé a střední podniky
	- ID 1 a 1002 až 1005 jsou předvytvořeny a nedají se smazat či upravit
	- Uloženy ve flash paměti
	- VTP synchronizuje databázi VLAN, výměna VLAN mezi přepínači
2) **Rozšířený rozsah** `VLAN ID` **od 1006 až 4094**
	- Pro providery a velké podniky
	- Uloženy v provozní konfiguraci
	- Je potřebný transparentní režim VTP
	- Méně funkcí než u běžných VLAN