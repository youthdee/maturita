#### 1) Pojem redundantní síť a možné problémy v ní

##### Redundantní síť
- Redundance brání výpadkům sítě
	- Omezením single point of failure
	- Instalací duplicitních síťových prvků
	- Konfigurací záložních služeb
- Redundantní cesty v síti poskytují alternativní fyzické spoje
	- V síti Ethernet nelze smyčky tolerovat
	- Řešením je protokol STP (Spanning Tree Protocol)

##### Problémy v redundantní síti
- Smyčky v Ethernetové síti
	- Ethernetové rámce cirkulují donekonečna protože jsou přepínači (switchi) stále přeposílány dál (Broadcast storm) což může zahltit celou síť
	- Duplikace rámců
	- Nesprávné doručení rámců
- Řešením je protokol STP (Spanning Tree Protocol) a jeho varianty:
	- RSTP (Rapid STP):
		- Rychlejší konvergence v případě výpadku
	- MSTP (Multiple STP)
		- Umožňuje různé STP instance pro různé VLANy


#### 2) Koncepce a použití STP, druhy STP protokolů
##### Koncept STP (Spanning Tree Protocol)
- Protokol zajišťující bezesmyčkovou topologii v Ethernetové síti blokováním redundantních spojů a ponecháváním jedné aktivní cesty mezi zařízeními
- STP volí Root Bridge, což je hlavní switch (přepínač), ke kterému se ostatní zařízení připojují optimální cestou
- Pokud hlavní cesta selže, STP aktivuje blokované spoje a obnoví provoz
- Funguje na L2
##### Princip činnosti STP
1) Volba Root Bridge
	- Zvolen podle nejnižšího Bridge ID (BID)
2) Výpočet nejkratší cesty k Root Bridge
	- Každý switch (přepínač) spočítá nejlepší cestu k Root Bridge pomocí Path Cost
	- Path Cost je metrika určující výhodnost cesty, čím nižší hodnota, tím lepší cesta
3) Volba Root portů
	- Každý switch (přepínač) kromě Root Bridge vybere nejlepší port směrem k Root Bridge
4) Volba Designated portů
	- Každý segment má jeden Designated port
	- Designated port je spojení, které vede k dalšímu segmentu sítě a je aktivní
5) Blokování redundantních spojů
	- Porty, které nejsou Root ani Designated, sjou blokovány jako Blocking Ports
	- Tyto porty nepřeposílají provoz, ale poslouchají BDPU rámce a mohou se aktivovat v případě výpadku hlavní cesty
##### STP Stavy portů
- Blocking
	- Port je blokovaný, neposílá rámce, poslouchá BDPU rámce
- Listening
	- Port je ve stavu čekání na změny v topologii
- Learning
	- Port se učí MAC adresy, ale zatím nepřeposílá rámce
- Forwarding
	- Plně aktivní port přeopílající provoz
- Disabled
	- Port je administrativně vypnutý
##### RSTP (Rapid Spanning Tree Protocol)
- Rychlejší verze STP s konvergencí do 6 sekund
- Nepoužívá Listening a Learning stavy, ale zavádí Alternate a Backup porty
##### MSTP (Multiple Spanning Tree Protocol)
- Umožňuje více instancí STP pro různé VLANy, čímž zlepšuje výkon sítě
##### PVST+ (Per-VLAN Spanning Tree)
- Proprietární protokol Cisco
- Každá VLAN má vlastní instanci STP, což umožňuje lepší kontrolu nad provozem
##### RPVST+ (Rapid Per-VLAN STP)
- Kombinuje PVST+ a RSTP, čímž poskytuje rychlou konvergenci pro každou VLAN
#### 3) EtherChannel – Popis a využití

##### Charakteristika EtherChannelu
- Technologie, která umožňuje sloučit více fyzických Ethernetových spojů mezi switchi (přepínači) do jednoho logického kanálu
- Funguje na L2 vrstvě
- Zvyšuje propustnost a umožňuje redundanci (V případě výpadku jednoho spoje stále fungují další spoje)
- Switche (přepínače) a hosté vidí spoj jako jedno logické spojení, nedochází ke smyčkám jako u běžné redundance, takže není potřeba protokolu STP

##### Využití Etherchannelu
- Zvýšení šířky pásma
- Redundance
- Zamezení STP blokování
- Vyvážení zátěže (load-balancing)

##### PAgP (Port Aggregation Protocol)
- Cisco proprietární protokol
- Vyjednává EtherChannel automaticky mezi Cisco zařízeními
- Módy:
	- Auto (pasivní, čeká na požadavek)
	- Desirable (aktivní, iniciuje sestavení kanálu)
##### LACP (Link Aggregation Control Protocol)
- Standardizovaný protokol dle IEEE 802.3ad
- Módy:
	- Active (aktivně se snaží vytvořit EtherChannel)
	- Passive (čeká na požadavek)