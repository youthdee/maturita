#### 1) Switch – princip činnosti

##### Princip činnosti switche (přepínače)
- Po zapnutí switche (přepínače) je MAC tabulka prázdná, switch (přepínač) určitou dobu pracuje jako hub
- Záznamy tabulky se tvoří dle přijatých rámců, uloží se MAC adresa odesílatele a číslo portu
- Rámce se následně rozesílají dle MAC tabulky, podle cílové MAC adresy se vyhledá číslo portu
- Záznamy tabulky po určité době expirují, při odpojení portu se položky tabulky vymažou

##### Přepínání rámců
- Klíčový koncept v oblasti sítí a telekomunikací
- Různé druhy switchů (přepínačů) pro různé sítě:
	- LAN, WAN, PSTN (Public Service Telephone Network)
- Rozlišení portů podle jejich aktuální úlohy:
	- Vstupní (ingress) port:
		- Místo, kde rámce vstupuje do zařízení
	- Výstupní (egress) port:
		- Místo, kudy rámec opouští zařízení
- Přepínání probíhá na základě vyhodnocení záhlaví rámce
	- Podle cílové adresy je možné dohledat výstupní port

##### Tabulka MAC adres switche (přepínače)
- Uložena v paměti CAM (Content Addresable Memory)
	- Která slouží pro vyhledávání záznamů vysokou rychlostí
- Přepínač za běhu zjišťuje, jaké zařízení jsou portům přiřazena, postupně obsah tabulky vytváří (po zapnutí switche je tabulka prázdná)
- Switch (přepínač) užívá MAC tabulku pro efektivní zpracování rámců, kde určuje správný výstupní port dle cílových MAC adres

##### Proces zpracování rámce
1) Learning
	- Switch (přepínač) uloží zdrojovou MAC adresu rámce do tabulky MAC adres
	- V případě, že záznam již existuje, aktualizuje se jeho doba platnosti
	- Když byla MAC adresa přiřazena k jinému portu, vytvoří nový záznam
2) Forwarding
	- V případě unicast adresy switch (přepínač) v tabulce MAC adres vyhledá pro danou cílovou MAC adresu výstupní port
	- V případě multicast/boradcast adresy je rámec rozeslán na všechny aktivní porty kromě portu vstupního

#### 2) Přepínání rámců na switchi, popis, metody

##### Metoda Store-and-Forward
- Switch (přepínač) nejprve příjme celý rámec, ověří délku a kontrolní součet (nevyhovující rámec vyřadí)
- Switch (přepínač) zaznamená číslo portu odesílatele pokud v tabulce MAC adres příslušný záznam není
- Switch (přepínač) odešle rámec na příslušný port pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
- Úplné přijetí rámce před odesláním (vyšší zpoždění), umožňuje vyloučit vadné rámce

##### Metoda Cut-through
- Switch (přepínač) přijme alespoň cílovou MAC adresu rámce, zahájí jeho zpracování, příjem rámce pokračuje
- Switch (přepínač) zahájí odeslání rámce na port pokud je v tabulce MAC adres příslušný záznam, když není, tak odešle rámec na ostatní aktivní porty (flood)
- Switch (přepínač) zaznamená číslo portu odesílatele, nejdříve však po přijetí zdrojové MAC adresy rámce a pokud v tabulce MAC adres příslušný záznam není
- Varianty Metody Cut-Trough:
	- Fast-forward
		- Zahájí odesílání rámce ihned po přijetí cílové MAC
		- Nejmenší přenosové zpoždění
		- Typická varianta
	- Fragment-free
		- Zahájí odesílání rámce po přijetí 64 oktetů
		- Nejvíce kolizí nastává právě v této části rámce
		- Kompromis mezi mírou integrity a zpoždění
- Rámec odesílán ihned po přijetí záhlaví (menší zpoždění), vadné rámce se tak předávají dále po síti
#### 3) Virtuální sítě (VLAN) na switchích, - vlastnosti a realizace

##### VLAN - Charakteristika
- Segmentace sítě na existujících fyzických spojích, organizace sítě do menších segmentů zjednodušuje správu sítě
- Organizační flexibilita v přepínané síti, hostitelé mohou být ve stejné místní síti napříč různými switchi (přepínači)
- Zařízení ve stejné VLAN si mohou zasílat Ethernet rámce (Zpravidla mají IP adresy společné IP sítě)
- Pracují na základě logických spojení, nikoliv fyzických, na jednom fyzickém spoji lze předávat rámce různých VLAN

##### Příklad nasazení VLAN
- Počítače různých oddělení ve stejné místní síti
- Segmentace sítě podle funkce, týmu nebo aplikace
- Sdílení fyzické infrastruktury s ostatními VLANy
- Rámce jsou předávány pouze zařízením ve stejné VLAN
- Komunikace mimo VLAN vyžaduje směrování

##### Výhody řešení s VLAN
- Úspora nákladů na vybudování síťové infrastruktury, pro VLANy není třeba vytvářet samostatné fyzické spoje
- Snadné rozdělení sítě na menší segmenty, účinné omezení velikosti broadcastových domén
- Přístupové politiky lze nastavit podle skupin uživatelů, řízení přístupu pomocí ACL pravidel na routerech
- Škálovatelnost síťové infrastruktury, pro vytvoření nové VLAN není třeba pořizovat nové síťové prvky

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