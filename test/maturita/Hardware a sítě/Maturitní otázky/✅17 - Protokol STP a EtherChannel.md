#### 1) Pojem redundantní síť a možné problémy v ní
##### Redundantní síť
1) **Redundance brání výpadkům sítě**
	- Omezením `single point of failure`
	- Instalací duplicitních síťových prvků
	- Konfigurací záložních služeb
2) **Redundantní cesty v síti poskytují alternativní fyzické spoje**
	- V síti `Ethernet` nelze smyčky tolerovat
	- Řešením je protokol `STP` (Spanning Tree Protocol)
##### Problémy v redundantní síti
1) **Smyčky v** `Ethernetové` **síti**:
	- `Ethernetové` rámce cirkulují donekonečna protože jsou switchi stále přeposílány dál (`Broadcast storm`) což může zahltit celou síť
	- Duplikace rámců
	- Nesprávné doručení rámců
2) **Řešením je protokol** `STP` (Spanning Tree Protocol) **a jeho varianty**:
	1) `RSTP` (Rapid STP):
		- Rychlejší konvergence v případě výpadku
	2) `MSTP` (Multiple STP)
		- Umožňuje různé STP instance pro různé VLANy
#### 2) Koncepce a použití STP, druhy STP protokolů
##### Koncept STP (Spanning Tree Protocol)
- Protokol zajišťující **bezesmyčkovou topologii** v `Ethernetové` síti **blokováním redundantních spojů** a ponecháváním jedné aktivní cesty mezi zařízeními
- `STP` volí `Root Bridge`, což je **hlavní switch**, ke kterému se **ostatní zařízení připojují** optimální cestou
- Pokud hlavní cesta selže,` STP` **aktivuje blokované spoje a obnoví provoz**
- Funguje na `L2`
##### Princip činnosti STP
1) **Volba** `Root Bridge`:
	- Zvolen podle nejnižšího `Bridge ID` (BID)
2) **Výpočet nejkratší cesty k** `Root Bridge`:
	- Každý switch spočítá nejlepší cestu k `Root Bridge` pomocí `Path Cost`
	- `Path Cost` je metrika určující výhodnost cesty, čím nižší hodnota, tím lepší cesta
3) **Volba Root portů**:
	- Každý switch kromě `Root Bridge` vybere nejlepší port směrem k `Root Bridge`
4) **Volba Designated portů**:
	- Každý segment má jeden `Designated` port
	- `Designated` port je spojení, které vede k dalšímu segmentu sítě a je aktivní
5) **Blokování redundantních spojů**:
	- Porty, které nejsou `Root` ani `Designated`, jsou blokovány jako `Blocking Ports`
	- Tyto porty nepřeposílají provoz, ale poslouchají `BDPU` rámce a mohou se aktivovat v případě výpadku hlavní cesty
##### STP Stavy portů
1) `Blocking`:
	- Port je blokovaný, neposílá rámce, poslouchá `BDPU` rámce
2) `Listening`:
	- Port je ve stavu čekání na změny v topologii
3) `Learning`:
	- Port se učí `MAC` adresy, ale zatím nepřeposílá rámce
4) `Forwarding`:
	- Plně aktivní port přeposílající provoz
5) `Disabled`:
	- Port je administrativně vypnutý
##### RSTP (Rapid Spanning Tree Protocol)
- Rychlejší verze `STP` s **konvergencí do 6 sekund**
- Nepoužívá `Listening` a `Learning` stavy, ale zavádí `Alternate` a `Backup` porty
##### MSTP (Multiple Spanning Tree Protocol)
- Umožňuje **více instancí** `STP` pro různé `VLAN`y, čímž **zlepšuje výkon** sítě
##### PVST+ (Per-VLAN Spanning Tree)
- **Proprietární protokol Cisco**
- Každá `VLAN` má **vlastní instanci** `STP`, což umožňuje lepší **kontrolu nad provozem**
##### RPVST+ (Rapid Per-VLAN STP)
- Kombinuje `PVST+` a `RSTP`, čímž poskytuje **rychlou konvergenci** pro každou `VLAN`
#### 3) EtherChannel – Popis a využití
##### Charakteristika EtherChannelu
1) Technologie, která umožňuje **sloučit více fyzických** `Ethernetových` **spojů** mezi switchi do **jednoho logického kanálu**
2) Funguje na `L2` vrstvě
3) **Zvyšuje propustnost** a umožňuje **redundanci**:
	- V případě výpadku jednoho spoje stále fungují další spoje
4) Switche a hosté vidí spoj jako **jedno logické spojení**, **nedochází ke smyčkám** jako u běžné redundance, takže **není potřeba protokolu** `STP`
##### Využití Etherchannelu
1) Zvýšení šířky pásma
2) Redundance
3) Zamezení `STP` blokování
4) Vyvážení zátěže (`load-balancing`)
##### PAgP (Port Aggregation Protocol)
- **Cisco proprietární protokol**
- Vyjednává `EtherChannel` **automaticky** mezi **Cisco zařízeními**
- Módy:
	1) `Auto`:
		- Pasivní, čeká na požadavek
	2) `Desirable`:
		- Aktivní, iniciuje sestavení kanálu)
##### LACP (Link Aggregation Control Protocol)
- Standardizovaný protokol dle `IEEE 802.3ad`
- Módy:
	1) `Active`:
		- Aktivně se snaží vytvořit `EtherChannel`
	2) `Passive`:
		- Čeká na požadavek