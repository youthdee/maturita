#### 1) Účel, funkce, standardy
##### Účel linkové vrstvy
- Poskytuje vyšší vrstvě (síťové) službu posílání blok dat sousednímu uzlu
- Pracuje s rámci
- Díky portokolům linkové vrstvy nemusí protokoly síťové vrstvy řešit, po jakém druhu přenosového média bude přenos dat probíhat
- Protokoly linkové vrstvy udávají způsob formátování rámce pro přenos po různých přenosových cestách
    - Pro každou přenosovou cestu a použité médium je možné použít jiný protokol
- Při každém průchodu routerem přijímá router rámce z jednoho média. rámce rozpouzdří a po rozhodnutí, kam bude paket odeslán paety opět zapouzdří do nového rámce
- Protokoly linkové vrstvy definují techniky pro umístění rámce na médium a z média, které se označují jako "metody pro řízení přístupu k médiu"
    - Výběr metody přístupu k médiu závisí na topologii sítě a způsobu, jakým uzly sdílí médium
##### Účel fyzické vrstvy
- Zajišťuje přístup k přenosovému médiu, které může být vyhrazené nebo sdílené mezi více uzly
- Zodpovídá za uskutečnění přenosu dat mezi uzly datové sítě
	- Jednosměrně či obousměrně (střídavě či nezávisle)
	- Nezkoumá obsah přenášených dat
- Převádí data rámce linkové vrstvy na signál vhodný pro přenos a naopak
	- Kódování (encoding)
	- Dekódování (decoding)
	- Modulace (modulation)
	- Demodulace (demodulation)
- Druhy fyzických médií:
	- Metalické médium (metallic)
		- Přenáší elektrické signály
	- Optické médium (optical)
		- Přenáší světelné signály
	- Bezdrátové médium (wireless)
		- Přenáší elektromagnetické vlnění

##### Funkce linkové vrstvy
- Přijímá pakety ze síťové vrstvy a zapouzdřuje je do rámců
- Řídí přístup k přenosovému médiu
- Provádí detekci chyb a odmítá vadné rámce
- Přijímá data v podobě rámců z přenosového média a jako pakety je předává síťové vrstvě ke zpracování
##### Funkce fyzické vrstvy
- Rámec -> Kódování -> Modulace
- Modulace -> Dekódování -> Rámec
- Kódování a dekódování:
	- Proces převodu datového proudu do podoby vhodnější pro přenos a naopak
	- Lepší odolnost signálu při přenosu, často plní funkci synchronizace cílového uzlu s uzlem odesílatele
	- Druhy linkových kódů:
		- Dvojúrovňové, trojúrovňové apod.
		- S návratem či bez návratu do nuly
		- Např. RZ, NRZ, NRZI, AMI, CMI
- Modulace a demodulace:
	- Proces převodu zakódovaných dat do tvaru signálu vhodného pro přenos po fyzickém médiu
	- Druhy modulace:
		- Analogové (AM, FM, PM)
		- Digitální (ASK, FSK, PSK)
		- Složené (QPSK, QAM)
		- Speciální (DSSS, OFDM)
##### Standardy linkové vrstvy
- Logical Link Control (LLC):
    - Sousedí se síťovou vrstvou, kde se do rámce vkládá údaj o protokolu síťové vrstvy, který je zapouzdřen v rámci
- Media Access Control (MAC):
    -   Sousedí s fyzickou vrstvou, přidává do rámce adresy (MAC adresy) a upravuje data podle požadavků na přenos signálu po médiu a řídí přenos k médiu a detekuje chyby
    - Ethernet IEEE (802.3):
	    - Určeno pro kabelové sítě (kroucená dvojlinka, optická vlákna)
	    - Využívá metodu CSMA/CD
    - WLAN IEEE (802.11):
	    - Určuje pravidla pro bezdrátové sítě a používá metodu CSMA/CA
    - WPAN IEE (802.15):
	    - Zahrnuje technologie jako Bluetooth, Zigbee pro komunikaci na velmi malé vzdálenosti
	    - Používá různá média k přístupu k médiu (TDMA - Time Division Multiple Access)
##### Standardy fyzické vrstvy
- Definují závazné charakteristiky přístupu k fyzickému médiu (mechanické, elektrické, procesní, časové)
- Vlastnosti závislé na médiu (druh média, konektory, související mechanické a elektrické charakteristiky)
- Vlastnosti nezávislé na médiu (linkový kód, synchronizace, modulace, framing)
- Ethernet (IEEE 802.11):
	- Standard pro kabelové sítě, specifikující přenos dat po měděných kabelech nebo optických vláknech
- Wi-Fi (IEEE 802.11):
	- Standard pro bezdrátové sítě, který určuje jak se přenášejí data vzduchem mezi zařízeními
- Bluetooth (IEEE 802.15.1)
	- Krátkovzdálenostní bezdrátový přenos dat využívající nízkou spotřebu energie
- DSL (Digital Subscriber Line)
	- Technologi pro přenos dat po telefonních linkách, používaná především pro připojení k Internetu
- USB (Universal Serial Bus):
	- Standard pro připojení zařízení k počítači nebo jiným zařízením využívající měděné kabely
- Fiber Optic:
	- Technologie pro přenos dat na velké vzdálenosti s velmi vysokou šířkou pásma pomocí optických vláken
- RS-232 a RS-485:
	- Standardy pro sériovou komunikaci, které definují elektrické signály pro přenos dat mezi zařízeními
#### 2) Přenosové cesty, druhy spojů (linky)
##### SIMPLEX, HLAF DUPLEX, FULL FUPLEX Komunukace
- Komunikace mezi dvěma uzly po lince můe probíhhat třemi způsoby:
    - Simplex (pouze jedním směrem)
    - Half-Duplex (oběma směry, ale ne současně)
    - Full-Duplex (současně oběma směry)

##### Metalická kabeláž
- Výhodou je cena, snadná použitelnost a dobrá vodivost elektrického proudu
- Nevýhodou je omezená délka vedení a citlivost na rušení
- Se vzdáleností signál slábne a mění tvar
- Druhy rušení signálu:
	- Electromagnetic Interference (EMI):
		- Interakce obvodu s elektromagnetickým polem okolí
		- Např. elektromotory, transformátory, rozvodná síť
	- Radio-Frequency Interference (RFI):
		- Interakce obvodu s vysokofrekvenčními vlnami
		- Např. vysílače, mobilní telefony, mikrovlnné trouby, počítače
	- Přeslech (crosstalk):
		- Rušení magentickým polem sousedního vedení
		- Signál se smísí se sousedním signálem
- Ochranou proti rušení je například kovové stínění nebo zakroucení kabelů, případně způsob vedení kabelů, správný výběr
- Druhy metalických kabelů:
	- Unshielded Twisted-Pair (UTP):
		- Tvořeno několika páry měděných drátů, které jsou vzájemně zkroucené
		- Používají se v Ethernetových sítích, telefonních linkách
	- Shielded Twisted-Pair (STP):
		- UTP kabel s ochranným stíněním (kovová fólie nebo opletení), které pomáhá chránit signál
		- Používají se při vysokém riziku rušení, například v průmyslových nebo komunikačních prostředích
	- Souosý (koaxiální) kabel:
		- Skládá se z centrálního vodiče, který je obklopen izolačním materiálem a stíněním, vnější izolací
		- Zastaralá možnost propojení uzlů v LAN
- Druhy konektorů:
	- RJ-11 pro telefonní linku
	- RJ-45 pro Ethernet
	- BNC
	- F pro kabelovou televizi
	- N
##### Optická kabeláž
- Optická vlákna jsou ohebná, přenáší světelné impulsy a jsou extrémně tenká
- Umožňují vlnový multiplex
- Výhodou je velká šířka pásma a malý útlum přenášeného signálu (data lze přenášet na velké vzdálenosti)
- Výhodou je také imunita proti EMI a RFI
- Nevýhodou je nižší mechanická odolnost (náročnější na instalaci), vyšší cena, dražší aktivní prvky (optické transceivery) a speciální nástroje a postupy pro montáž
- Využívají se v podnikových sítích, FTTH, WAN, podmořské kabelové sítě
- Druhy optických vláken:
	- Mnohovidové vlákno:
		- Malý dosah, větší jádro, velký rozptyl
		- LED jako zdroj světla, páteř lokálních sítí, rychlost až 10Gb/s
	- Jednovidové vlákno:
		- Velký dosah (až 100km), malé jádro a rozptyl
		- Laser jako zdroj světla
		- Telefonní hovory, kabelová TV
##### Bezdrátové spoje
- Výhodou jsou náklady na fyzické médium (nulové), zřízení spoje i na větší vzdálenost a mobilita účastnických stanic v síti
- Nevýhodou je omezená disponibilita rádiového pásma, omezená oblast pokrytí, omezená dostupnost přenosového kanálu, nízká odolnost vůči rušení a problematická bezpečnost
- Příklady bezdrátových spojů:
	- Bluetooth:
		- Standard IEEE 802.15.1
		- Frekvence od 2,4 do 2,48 GHz
		- Určeno pro PAN
		- Dosah až 100m
	- Wi-Fi
		- Standard IEEE 802.11
		- Frekvenční pásma:
			- 2,45 GHz (14 kanálů se šířkou 22 MHz, po 5 MHz)
			- 5 GHz

#### 3) Fyzická a logická topologie sítě LAN a WAN
##### Fyzická a logická topologie
- Topologií sítě se rozumí uspořádání, propojení a vztahy mezi jednotlivými prvky v síti
- V LAN a WAN sítích mluvíme o fyzické topologii a logické topologii
##### Fyzická topologie
- Popisuje fyzická připojení prvků v síti a určuje, jakým způsobem jsou propojeny koncová a zprostředkující zařízení v síti
- Nejběžnějšími topologiemi v současných sítích jsou topologie:
    - Point-to-point
    - Star
    - Extended Star
    - Hub and Spoke
    - Mesh
- Dříve používané topologie jako sběrnice (bus) a kruh (ring)
 
##### Logická topologie
- Definuje způsob, jakým se v síti přenášejí jednotlivé rámce od uzlu k uzlu
- Logickou topologii definují protokoly linkové vrstvy
- Logická topologie point-to-point často tvoří virtuální okruh
 
#### 4) Přístupové metody v LAN a WLAN
##### Definice
- V multiaccess LANs (Ethernet, IEEE 802.11) několik uzlů sdílí jeden společný přenosový prostředek (fyzické médium)
    - Může dojít ke stavu, kdy se bude několik stanic najednou pokoušet odesílat data
- Přístupové metody definují pravidla a postupy, které zajišťují, aby se všechny stanice dostaly k přenosovému médiu
 
##### Přístupové metody pro sdílené médium
- Přístup založený na soutěži (contention-based access):
    - Všechny uzly o přístup k médiu soutěží, pokud dojde ke kolizi, vědí jak se mají zachovat
    - Uzel v síti se může pokusit přistoupit k médiu kdykoliv potřebuje odesílat data
    - Nejprve však použije proces CSMA (Carrier Sense Multiple Access), který zjišťuje, zda se na médiu přenáší nějaký signál
        - Pokud tam signál není, pokusí se vysílat data
        - Pokud tam signál je, počká
        - Může se stát, že se pokusí dva uzly vysílat současně. čímž vznikne kolize
        - Pokud dojde ke kolizi, jsou data odeslána oběma uzly poškozena a je třeba je odeslat znovu
- Řízený přístup (controlled access):
    - Každý uzel má přiřazen čas, po který může médium používat
    - CSMA se obvykle používá ve spojení s metodou pro řešení kolizí signálů
    - Mezi nejpoužívanější patří:
        - CSMA/CD
        - CSMA/CA
 
##### Přístupová metoda CSMA/CD (Carrier sense multiple access with collision detection)
- Metoda vícenásobného přístupu s detekcí nosné a detekcí kolize
- Jestliže dojde ke kolizi signálů, přestanou všechny uzly okamžitě vysílat a zkusí to později (po uplynutí náhodně generovaného časového intervalu)
- Tato metoda se používá v half-duplexních ethernetových LAN (zastaralé)
 
##### Přístupová metoda CMSA/CA (Carrier sense multiple access with collision avoidance)
- Metoda vícenásobného přístupu s detekcí nosné a předcházením kolize
- Pokud se na médiu nenachází žádný datový signál a médium je tedy volné, uzel vyšle po médiu upozornění, že hodlá médium použít
- Jakmile obdrží oznámení, že může vysílat, začne posílat data
- Tato metoda je používaná u WLAN technologií standardu 802.11 (bezdrátové sítě)
 
##### Controlled Access (řízený přístup) - Token Passing
- Uzly přistupují v síti k médiu v určitém pořadí
- Vše se řeší používáním tokenu a metoda se nazývá Token Passing
- Každý koncový uzel získá token a umístí rámec na médium, nemůže vysílat žádný jiný uzel, dokud rámec nedorazí a není zpracován cílovým uzlem
- Pak se token uvolní a předá dalšímu uzlu v pořadí
- Linková vrstva je v tomto případě vnímána jako logická kruhová topologie, fyzická topologie tedy může být jiná (např. hvězda)
- Tyto metody jsou méně efektivní
- Využívá se v (zastaralé):
    - FDDI (Fiber Distributed Data Interface):
        - Používá protokol Token Bus (IEEE 802.4)
    - Token Ring (IEEE 802.5)
-